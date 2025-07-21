Creating a Sage X3 Classic Web Service (SOAP + JSON)
===================================================

This guide walks you through publishing a 4GL (Adonix) subprogram as a classic
web service that returns its payload as JSON embedded in the SOAP envelope.
The example uses subprogram `XX3DWLSUSR`, which delivers a filtered list of
users.

--------------------------------------------------
1 . Prerequisites
--------------------------------------------------

- Sage X3 server and client with the classic SOAP gateway (`CAdxWebServiceXmlCC`)
  enabled
- Adonix 4GL development rights in the target folder
- Basic familiarity with:
  - 4GL development (`Subprog`, `Local`, `Variable`, I/O loops)
  - Web-service functional authorisations in Sage X3
- A connection pool (for example `ADXSQL`) that the web service can use

--------------------------------------------------
2 . Write (or review) the subprogram
--------------------------------------------------

Keep subprograms used by web services stateless and UI-less.

```adonix
# TRT/SUB/XX3DWLSUSR.src
Local Integer  C_MAX : C_MAX = 100   # maximum array size

Subprog XX3DWLSUSR(O_USER, O_NAME, O_MESSAGE, O_STAT)

    Variable Char    O_USER(C_MAX)(1)    # 1-D array of logins
    Variable Char    O_NAME(C_MAX)(1)    # 1-D array of names
    Variable Char    O_MESSAGE
    Variable Integer O_STAT

    #--------------------------------------------------------------------
    # Open the user table only once per call
    #--------------------------------------------------------------------
    If !clalev([F:YAUS])
        Local File AUTILIS [F:YAUS]
    Endif

    #--------------------------------------------------------------------
    # Business rule: pick users where XX3DYUSR = 2
    #--------------------------------------------------------------------
    Filter [F:YAUS] Where [F:YAUS]XX3DYUSR = 2

    Local Integer i : i = 0
    For [F:YAUS]
        If i >= C_MAX  : Break : Endif   # never overflow

        O_USER(i) = [F:YAUS]LOGIN
        O_NAME(i) = [F:YAUS]NOMUSR
        i += 1
    Next

    Filter [F:YAUS]      # clear filter

    O_MESSAGE = "OK"
    O_STAT    = 1        # 1 = success

End
```

Best practices

- Never call `Infbox`, `Gmsg`, `Input`, etc. – web services run headless.
- Use constants for array bounds (`C_MAX`) and guard every loop.
- Return operation status in simple scalar parameters (`O_MESSAGE`, `O_STAT`).
- Use `Trace` statements (optionally conditional on `!GWEBSERV`) when you need
  server-side diagnostics.

--------------------------------------------------
3 . Create the web-service definition
--------------------------------------------------

Menu: `Development > Web services > Classic web services > Web service`

1. General tab
   - Code      : `WSXX3DUSERLIST`
   - Description: `Users where XX3DYUSR = 2`
   - Service type: `Subprogram`
   - Subprogram : `XX3DWLSUSR` (folder TRT)

2. Parameters tab

| Name       | Dir | Type      | Size | Dim 1 | Dim 2 | Comment            |
|------------|-----|-----------|------|-------|-------|--------------------|
| O_USER     | Out | Alphanum  | 30   | 100   | –     | Login list         |
| O_NAME     | Out | Alphanum  | 30   | 100   | –     | User names         |
| O_MESSAGE  | Out | Alphanum  | 30   | –     | –     | Status text        |
| O_STAT     | Out | Integer   | –    | –     | –     | Status code (1 =OK)|

Save, then Validate.

JSON mapping cheatsheet

- A 1-D Alphanum array appears as a JSON array of simple values:
  `"O_USER": ["AE011", "AE012", …]`
- Scalars declared in the `STAT` group (`O_MESSAGE`, `O_STAT`, `O_RET`) are
  automatically packed into an object called `PARAM_STAT`.
- All other outputs are grouped into `PARAM_OUT`.

--------------------------------------------------
4 . Publish the service
--------------------------------------------------

Menu: `Development > Web services > Classic web services > Publication`

- Search for `WSXX3DUSERLIST`, choose it, then click `Publish`.

--------------------------------------------------
5 . Quick test inside X3
--------------------------------------------------

Menu: `Development > Web services > Classic web services > Web service tester`

- Enter `WSXX3DUSERLIST`, click `Search`.
- On the `JSON` tab press `Test`.
- The response will resemble:

```json
{
  "PARAM_OUT": [
    { "O_USER": "AE011", "O_NAME": "Adam Evans" },
    { "O_USER": "AE012", "O_NAME": "Anna Ellis" }
  ],
  "PARAM_STAT": {
    "O_MESSAGE": "OK",
    "O_STAT": "1"
  }
}
```

--------------------------------------------------
6 . Call the service from an external client
--------------------------------------------------

Endpoint template
`http://<SERVER>:<PORT>/soap-gw/<POOL_ALIAS>/<FOLDER>/CAdxWebServiceXmlCC`

Example
`http://x3srv:8124/soap-gw/ADXSQL/SEED/CAdxWebServiceXmlCC`

Minimal SOAP request (no inputs):

```xml
<soapenv:Envelope
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
	xmlns:wss="http://www.adonix.com/WSS">
soapenv:Header/
soapenv:Body

	<wss:run soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
		<callContext xsi:type="wss:CAdxCallContext">
			<codeLang xsi:type="xsd:string">ENG</codeLang>
			<poolAlias xsi:type="xsd:string">POOL_NAME</poolAlias>
			<poolId xsi:type="xsd:string"></poolId>
			<requestConfig xsi:type="xsd:string">adxwss.optreturn=JSON&adxwss.beautify=true</requestConfig>
		</callContext>
		<publicName xsi:type="xsd:string">WSXX3DUSERLIST</publicName>
		<inputXml xsi:type="xsd:string">
{}
</inputXml>
	</wss:run>
</soapenv:Body>undefined</soapenv:Envelope>
```

Parsing the response

1. Read the SOAP envelope.
2. Extract the contents of `<resultXml>`.
3. Parse that string as JSON.

--------------------------------------------------
7 . Troubleshooting checklist
--------------------------------------------------

- Web service not found → Does `publicName` match the **Code** in X3?
- HTTP 401 or 403 → User lacks “Web service authorisation” or bad credentials.
- Empty arrays → Parameter types or dimensions do not match your 4GL code.
- “Malformed JSON” → Did you strip the wrapping `<![CDATA[ … ]]>` before
  feeding the string to your JSON parser?
- Business errors → Check `O_STAT`/`O_MESSAGE` first, then
  `ADXTRACE*.log` on the server (enable `<trace>true</trace>` in
  `requestConfig` if necessary).

You now have a repeatable pattern for wrapping any 4GL subprogram behind a
classic Sage X3 web service that speaks JSON—ready for Postman, Python, .NET,
or any modern integration platform.
