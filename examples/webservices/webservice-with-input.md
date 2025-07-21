This is an excellent example for demonstrating input parameters, and it also highlights using standard masks (`VXECI`) within a web service, which is very common in Sage X3 development. The error handling with `GERR` and `GMESSAGE` is also standard practice.

Let's integrate this into the web service documentation, focusing on how to define and pass these input parameters.

---

# Creating a Web Service in Sage X3 (Adonix 4GL) with Input Parameters and JSON Output

This document outlines the steps to expose a Sage X3 4GL subprogram as a web service, focusing on defining and passing input parameters, and demonstrating the JSON formatted output within the SOAP response. We will use the provided `XX3DWEXCIN` subprogram, which simulates a "Clock In" transaction.

## Prerequisites

*   **Sage X3 Development Environment:** Access to the Sage X3 client and server.
*   **Knowledge of Sage X3 4GL (Adonix Language):** Understanding of `Subprog`, `Local`, `Variable`, `Value`, `Mask`, and `Gosub`.
*   **Existing Subprogram:** A subprogram in Sage X3 4GL that you wish to expose, designed to accept input parameters (e.g., `XX3DWEXCIN`).
*   **Sage X3 Web Service Configuration:** Your Sage X3 installation must be configured to use the `CAdxWebServiceXmlCC` (or similar) endpoint, which supports JSON marshalling/unmarshalling.

## Step 1: Develop or Verify Your Subprogram

Ensure your 4GL subprogram is correctly developed to accept inputs and return outputs. This example demonstrates calling standard mask actions (`VXECI`'s `DEBUT`, `C_EMPNUM`, `AM_EMPNUM`, `C_FCY`, `OK`) to perform the business logic.

**Example Subprogram (`TRT/SUB/XX3DWEXCIN.src`):**

```adonix
Subprog XX3DWEXCIN(
& I_FCY, I_EMPNUM,
& O_STAT, O_MESSAGE
& )
  Value Char I_FCY()         // Input Parameter: Site (Passed by value)
  Value Decimal I_EMPNUM      // Input Parameter: Employee ID (Passed by value)
  Variable Integer O_STAT     // Output Parameter: Status (Passed by reference)
  Variable Char O_MESSAGE     // Output Parameter: Error message (Passed by reference)

  If !clalev([M:XECI]) : Local Mask VXECI [M:XECI] : Endif

  O_STAT = 1                // Initialize success status
  O_MESSAGE = ""            // Initialize empty message

  Gosub DEBUT From VXECI    // Standard mask initialization

  # --------------------------------------------------------------------------------------------
  # Employee ID - Process input from web service
  # --------------------------------------------------------------------------------------------
  [M:XECI]EMPNUM    = I_EMPNUM  // Assign input to mask field
  Call C_EMPNUM(I_EMPNUM) From VXECI // Call Control (validation) action for EMPNUM
  If GERR > 0                     // Check for global error variable
    Gosub SET_ERROR
    Goto END_WS                 // Jump to end if error
  Endif

  Call AM_EMPNUM(I_EMPNUM) From VXECI // Call After Change (processing) action for EMPNUM
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif
  # --------------------------------------------------------------------------------------------

  # --------------------------------------------------------------------------------------------
  # Site - Process input from web service
  # --------------------------------------------------------------------------------------------
  [M:XECI]FCY       = I_FCY   // Assign input to mask field
  Call C_FCY(I_FCY) From VXECI // Call Control (validation) action for FCY
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif
  # --------------------------------------------------------------------------------------------

  Gosub OK From VXECI       // Call OK (save/commit) action for the mask
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif

$END_WS
End

// Subroutine for setting error status and message
$SET_ERROR
  O_STAT = 0

  If GMESSAGE <> ""
    O_MESSAGE = GMESSAGE // Use Sage X3's global message variable if available
  Else
    O_MESSAGE = "Did not work for unknown reason" // Generic fallback message
  Endif
Return
```

**Key Considerations for Web Service Subprograms with Input Parameters:**

*   **`Value` vs. `Variable`:**
    *   `Value Char I_FCY()`: Indicates `I_FCY` is an **input** parameter passed by value. Changes to `I_FCY` within the subprogram will not affect the caller's value.
    *   `Variable Integer O_STAT`: Indicates `O_STAT` is an **output** (or input/output) parameter passed by reference. Changes to `O_STAT` within the subprogram *will* affect the caller's value.
*   **Mask Integration:** The example correctly uses `Local Mask` and `Gosub/Call From` to interact with standard Sage X3 mask logic. This is crucial for ensuring standard business rules and data integrity are applied.
*   **Error Handling (`GERR`, `GMESSAGE`):** The subprogram checks `GERR` (global error variable) after each mask action. If `GERR` is greater than 0, an error occurred. `GMESSAGE` often contains the detailed error message from Sage X3.
*   **No UI Interaction:** Still avoid `Infbox` or similar UI elements in a production web service. The `Infbox` in the main block is for testing the calling of the web service.

## Step 2: Create a Web Service Definition in Sage X3

This is done through the Sage X3 user interface.

1.  **Navigate to Web Services:**
    *   Go to: **Development > Web services > Classic web services > Web service**.

2.  **Create a New Web Service:**
    *   Click on **"New"** to create a new web service definition.

3.  **Enter General Information:**
    *   **Code:** A unique code for your web service (e.g., `WSXX3EXCIN`).
    *   **Description:** A clear description (e.g., `Employee Clock In Web Service`).
    *   **Service type:** Select `Subprogram`.
    *   **Subprogram:** Enter the exact name of your 4GL subprogram (`XX3DWEXCIN`).
    *   **Module:** Select the module where your subprogram resides (e.g., `TRT`).

4.  **Define Parameters:**
    *   Go to the **"Parameters"** tab.
    *   You need to define each parameter that your `Subprog` expects, mapping them to the correct data types and directions.

    For `Subprog XX3DWEXCIN(I_FCY, I_EMPNUM, O_STAT, O_MESSAGE)`:

    | Parameter Name | Direction     | Type         | Size (Max) | Array (Dim 1) | Array (Dim 2) | Description          |
    | :------------- | :------------ | :----------- | :--------- | :------------ | :------------ | :------------------- |
    | `I_FCY`        | `Input`       | `Alphanum`   | 30         | -             | -             | Site Code            |
    | `I_EMPNUM`     | `Input`       | `Numeric`    | -          | -             | -             | Employee ID          |
    | `O_STAT`       | `Output`      | `Integer`    | -          | -             | -             | Status Code (1=OK)   |
    | `O_MESSAGE`    | `Output`      | `Alphanum`   | 255        | -             | -             | Status Message       |

    *   **Direction:** Carefully choose `Input` for `I_FCY` and `I_EMPNUM`, and `Output` for `O_STAT` and `O_MESSAGE`.
    *   **Type:** `I_EMPNUM` is `Decimal` in 4GL, which typically maps to `Numeric` in X3 web service parameters.
    *   **Size (Max):** Set appropriate lengths for `Alphanum` types.

5.  **Save and Validate:**
    *   Click **"Create"** or **"Save"** and then **"Validation"** (or **"Save"** then **"Validation"** from the left list).

## Step 3: Publish the Web Service

Once validated, publish the web service to make it available.

1.  **Navigate to Publication:**
    *   Go to: **Development > Web services > Classic web services > Publication**.

2.  **Select Your Web Service:**
    *   Enter the **Code** of your web service (e.g., `WSXX3EXCIN`).
    *   Click **"Search"**.

3.  **Publish:**
    *   Select the web service.
    *   Click the **"Publish"** action and confirm.

## Step 4: Test the Web Service (Optional but Recommended)

Use the Sage X3 Web Service Tester to verify functionality.

1.  **Navigate to Web Service Tester:**
    *   Go to: **Development > Web services > Classic web services > Web service tester**.

2.  **Select Your Web Service:**
    *   Enter the **Code** of your web service (e.g., `WSXX3EXCIN`).
    *   Click **"Search"**.

3.  **Provide Input and Test:**
    *   Switch to the **"JSON"** tab.
    *   You will see an `Input` JSON section. Populate it with your test data:

        ```json
        {
          "I_FCY": "NA023",
          "I_EMPNUM": 801
        }
        ```
    *   Click **"Test"**.

4.  **Review Results:**
    *   The "Result JSON" tab will show the response:

        ```json
        {
          "PARAM_STAT": {
            "O_MESSAGE": "OK",
            "O_STAT": "1"
          }
        }
        ```
    *   If there's an error, `O_STAT` would be `0` and `O_MESSAGE` would contain the error details. Note that `PARAM_OUT` is absent since there are no array outputs.

## Step 5: Consume the Web Service from an External System

Now, an external application can call this web service.

*   **Web Service Endpoint (URL):**
    `http://<X3_SERVER_NAME>:<PORT>/soap-gw/<POOL_ALIAS>/<FOLDER_NAME>/CAdxWebServiceXmlCC`
    (e.g., `http://localhost:8124/soap-gw/ADXSQL/SEED/CAdxWebServiceXmlCC`)

*   **Authentication:** Basic authentication with a valid Sage X3 user.

*   **SOAP Request Structure with Input JSON:**

    ```xml
    <soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:wss="http://www.adonix.com/WSS">
        <soapenv:Header/>
        <soapenv:Body>
            <wss:run soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
                <callContext xsi:type="wss:CAdxCallContext">
                    <codeLang xsi:type="xsd:string">ENG</codeLang>
                    <poolAlias xsi:type="xsd:string">ADXSQL</poolAlias>
                    <poolId xsi:type="xsd:string"></poolId>
                    <requestConfig xsi:type="xsd:string"></requestConfig>
                </callContext>
                <publicName xsi:type="xsd:string">WSXX3EXCIN</publicName> <!-- Your web service code -->
                <inputXml xsi:type="xsd:string">
                    <![CDATA[
                    {
                        "I_FCY": "NA023",
                        "I_EMPNUM": 801
                    }
                    ]]>
                </inputXml>
            </wss:run>
        </soapenv:Body>
    </soapenv:Envelope>
    ```
    *   The `inputXml` now contains a JSON object with keys corresponding to your input parameter names (`I_FCY`, `I_EMPNUM`) and their respective values.

*   **SOAP Response Structure (with JSON `resultXml`):**

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" xmlns:wss="http://www.adonix.com/WSS">
        <soapenv:Body>
            <wss:runResponse soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
                <runReturn xsi:type="wss:CAdxResultXml">
                    <messages xsi:type="soapenc:Array" soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" soapenc:arrayType="wss:CAdxMessage[0]"></messages>
                    <resultXml xsi:type="xsd:string">
                        <![CDATA[{
                            "PARAM_STAT": {
                                "O_MESSAGE": "OK",
                                "O_STAT": "1"
                            }
                        }]]>
                    </resultXml>
                    <status xsi:type="xsd:int">1</status>
                    <technicalInfos xsi:type="wss:CAdxTechnicalInfos">
                        <!-- ... (technical info) ... -->
                    </technicalInfos>
                </runReturn>
            </wss:runResponse>
        </soapenv:Body>
    </soapenv:Envelope>
    ```
    *   The `resultXml` contains the JSON output, which in this case, only includes the `PARAM_STAT` block since `O_STAT` and `O_MESSAGE` are the only output parameters.

## Troubleshooting

*   **Input Data Validation:** If the web service returns an error (`O_STAT = 0`, `O_MESSAGE` populated), check the values of `I_FCY` and `I_EMPNUM`. Ensure they are valid and adhere to Sage X3's business rules (e.g., `NA023` must be a valid site, `801` a valid employee ID).
*   **Mask Specific Errors:** When integrating with masks, errors can stem from data integrity, missing mandatory fields (even if not exposed as web service inputs, the mask might require them), or security permissions on the underlying function. Check the X3 server logs for detailed messages.
*   **JSON Input Format:** Double-check that your `inputXml` contains valid JSON. Syntax errors in the JSON (e.g., missing commas, incorrect quotes) will cause the web service call to fail.
*   **Data Types:** Ensure the data types in your input JSON match what the Sage X3 web service expects (`"NA023"` as a string for `Alphanum`, `801` as a number for `Numeric`).

This comprehensive guide should equip you with the knowledge to create and consume Sage X3 web serThis is an excellent example for demonstrating input parameters, and it also highlights using standard masks (`VXECI`) within a web service, which is very common in Sage X3 development. The error handling with `GERR` and `GMESSAGE` is also standard practice.

Let's integrate this into the web service documentation, focusing on how to define and pass these input parameters.

---

# Creating a Web Service in Sage X3 (Adonix 4GL) with Input Parameters and JSON Output

This document outlines the steps to expose a Sage X3 4GL subprogram as a web service, focusing on defining and passing input parameters, and demonstrating the JSON formatted output within the SOAP response. We will use the provided `XX3DWEXCIN` subprogram, which simulates a "Clock In" transaction.

## Prerequisites

*   **Sage X3 Development Environment:** Access to the Sage X3 client and server.
*   **Knowledge of Sage X3 4GL (Adonix Language):** Understanding of `Subprog`, `Local`, `Variable`, `Value`, `Mask`, and `Gosub`.
*   **Existing Subprogram:** A subprogram in Sage X3 4GL that you wish to expose, designed to accept input parameters (e.g., `XX3DWEXCIN`).
*   **Sage X3 Web Service Configuration:** Your Sage X3 installation must be configured to use the `CAdxWebServiceXmlCC` (or similar) endpoint, which supports JSON marshalling/unmarshalling.

## Step 1: Develop or Verify Your Subprogram

Ensure your 4GL subprogram is correctly developed to accept inputs and return outputs. This example demonstrates calling standard mask actions (`VXECI`'s `DEBUT`, `C_EMPNUM`, `AM_EMPNUM`, `C_FCY`, `OK`) to perform the business logic.

**Example Subprogram (`TRT/SUB/XX3DWEXCIN.src`):**

```adonix
Subprog XX3DWEXCIN(
& I_FCY, I_EMPNUM,
& O_STAT, O_MESSAGE
& )
  Value Char I_FCY()         // Input Parameter: Site (Passed by value)
  Value Decimal I_EMPNUM      // Input Parameter: Employee ID (Passed by value)
  Variable Integer O_STAT     // Output Parameter: Status (Passed by reference)
  Variable Char O_MESSAGE     // Output Parameter: Error message (Passed by reference)

  If !clalev([M:XECI]) : Local Mask VXECI [M:XECI] : Endif

  O_STAT = 1                // Initialize success status
  O_MESSAGE = ""            // Initialize empty message

  Gosub DEBUT From VXECI    // Standard mask initialization

  # --------------------------------------------------------------------------------------------
  # Employee ID - Process input from web service
  # --------------------------------------------------------------------------------------------
  [M:XECI]EMPNUM    = I_EMPNUM  // Assign input to mask field
  Call C_EMPNUM(I_EMPNUM) From VXECI // Call Control (validation) action for EMPNUM
  If GERR > 0                     // Check for global error variable
    Gosub SET_ERROR
    Goto END_WS                 // Jump to end if error
  Endif

  Call AM_EMPNUM(I_EMPNUM) From VXECI // Call After Change (processing) action for EMPNUM
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif
  # --------------------------------------------------------------------------------------------

  # --------------------------------------------------------------------------------------------
  # Site - Process input from web service
  # --------------------------------------------------------------------------------------------
  [M:XECI]FCY       = I_FCY   // Assign input to mask field
  Call C_FCY(I_FCY) From VXECI // Call Control (validation) action for FCY
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif
  # --------------------------------------------------------------------------------------------

  Gosub OK From VXECI       // Call OK (save/commit) action for the mask
  If GERR > 0
    Gosub SET_ERROR
    Goto END_WS
  Endif

$END_WS
End

// Subroutine for setting error status and message
$SET_ERROR
  O_STAT = 0

  If GMESSAGE <> ""
    O_MESSAGE = GMESSAGE // Use Sage X3's global message variable if available
  Else
    O_MESSAGE = "Did not work for unknown reason" // Generic fallback message
  Endif
Return
```

**Key Considerations for Web Service Subprograms with Input Parameters:**

*   **`Value` vs. `Variable`:**
    *   `Value Char I_FCY()`: Indicates `I_FCY` is an **input** parameter passed by value. Changes to `I_FCY` within the subprogram will not affect the caller's value.
    *   `Variable Integer O_STAT`: Indicates `O_STAT` is an **output** (or input/output) parameter passed by reference. Changes to `O_STAT` within the subprogram *will* affect the caller's value.
*   **Mask Integration:** The example correctly uses `Local Mask` and `Gosub/Call From` to interact with standard Sage X3 mask logic. This is crucial for ensuring standard business rules and data integrity are applied.
*   **Error Handling (`GERR`, `GMESSAGE`):** The subprogram checks `GERR` (global error variable) after each mask action. If `GERR` is greater than 0, an error occurred. `GMESSAGE` often contains the detailed error message from Sage X3.
*   **No UI Interaction:** Still avoid `Infbox` or similar UI elements in a production web service. The `Infbox` in the main block is for testing the calling of the web service.

## Step 2: Create a Web Service Definition in Sage X3

This is done through the Sage X3 user interface.

1.  **Navigate to Web Services:**
    *   Go to: **Development > Web services > Classic web services > Web service**.

2.  **Create a New Web Service:**
    *   Click on **"New"** to create a new web service definition.

3.  **Enter General Information:**
    *   **Code:** A unique code for your web service (e.g., `WSXX3EXCIN`).
    *   **Description:** A clear description (e.g., `Employee Clock In Web Service`).
    *   **Service type:** Select `Subprogram`.
    *   **Subprogram:** Enter the exact name of your 4GL subprogram (`XX3DWEXCIN`).
    *   **Module:** Select the module where your subprogram resides (e.g., `TRT`).

4.  **Define Parameters:**
    *   Go to the **"Parameters"** tab.
    *   You need to define each parameter that your `Subprog` expects, mapping them to the correct data types and directions.

    For `Subprog XX3DWEXCIN(I_FCY, I_EMPNUM, O_STAT, O_MESSAGE)`:

    | Parameter Name | Direction     | Type         | Size (Max) | Array (Dim 1) | Array (Dim 2) | Description          |
    | :------------- | :------------ | :----------- | :--------- | :------------ | :------------ | :------------------- |
    | `I_FCY`        | `Input`       | `Alphanum`   | 30         | -             | -             | Site Code            |
    | `I_EMPNUM`     | `Input`       | `Numeric`    | -          | -             | -             | Employee ID          |
    | `O_STAT`       | `Output`      | `Integer`    | -          | -             | -             | Status Code (1=OK)   |
    | `O_MESSAGE`    | `Output`      | `Alphanum`   | 255        | -             | -             | Status Message       |

    *   **Direction:** Carefully choose `Input` for `I_FCY` and `I_EMPNUM`, and `Output` for `O_STAT` and `O_MESSAGE`.
    *   **Type:** `I_EMPNUM` is `Decimal` in 4GL, which typically maps to `Numeric` in X3 web service parameters.
    *   **Size (Max):** Set appropriate lengths for `Alphanum` types.

5.  **Save and Validate:**
    *   Click **"Create"** or **"Save"** and then **"Validation"** (or **"Save"** then **"Validation"** from the left list).

## Step 3: Publish the Web Service

Once validated, publish the web service to make it available.

1.  **Navigate to Publication:**
    *   Go to: **Development > Web services > Classic web services > Publication**.

2.  **Select Your Web Service:**
    *   Enter the **Code** of your web service (e.g., `WSXX3EXCIN`).
    *   Click **"Search"**.

3.  **Publish:**
    *   Select the web service.
    *   Click the **"Publish"** action and confirm.

## Step 4: Test the Web Service (Optional but Recommended)

Use the Sage X3 Web Service Tester to verify functionality.

1.  **Navigate to Web Service Tester:**
    *   Go to: **Development > Web services > Classic web services > Web service tester**.

2.  **Select Your Web Service:**
    *   Enter the **Code** of your web service (e.g., `WSXX3EXCIN`).
    *   Click **"Search"**.

3.  **Provide Input and Test:**
    *   Switch to the **"JSON"** tab.
    *   You will see an `Input` JSON section. Populate it with your test data:

        ```json
        {
          "I_FCY": "NA023",
          "I_EMPNUM": 801
        }
        ```
    *   Click **"Test"**.

4.  **Review Results:**
    *   The "Result JSON" tab will show the response:

        ```json
        {
          "PARAM_STAT": {
            "O_MESSAGE": "OK",
            "O_STAT": "1"
          }
        }
        ```
    *   If there's an error, `O_STAT` would be `0` and `O_MESSAGE` would contain the error details. Note that `PARAM_OUT` is absent since there are no array outputs.

## Step 5: Consume the Web Service from an External System

Now, an external application can call this web service.

*   **Web Service Endpoint (URL):**
    `http://<X3_SERVER_NAME>:<PORT>/soap-gw/<POOL_ALIAS>/<FOLDER_NAME>/CAdxWebServiceXmlCC`
    (e.g., `http://localhost:8124/soap-gw/ADXSQL/SEED/CAdxWebServiceXmlCC`)

*   **Authentication:** Basic authentication with a valid Sage X3 user.

*   **SOAP Request Structure with Input JSON:**

    ```xml
    <soapenv:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:wss="http://www.adonix.com/WSS">
        <soapenv:Header/>
        <soapenv:Body>
            <wss:run soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
                <callContext xsi:type="wss:CAdxCallContext">
                    <codeLang xsi:type="xsd:string">ENG</codeLang>
                    <poolAlias xsi:type="xsd:string">ADXSQL</poolAlias>
                    <poolId xsi:type="xsd:string"></poolId>
                    <requestConfig xsi:type="xsd:string"></requestConfig>
                </callContext>
                <publicName xsi:type="xsd:string">WSXX3EXCIN</publicName> <!-- Your web service code -->
                <inputXml xsi:type="xsd:string">
                    <![CDATA[
                    {
                        "I_FCY": "NA023",
                        "I_EMPNUM": 801
                    }
                    ]]>
                </inputXml>
            </wss:run>
        </soapenv:Body>
    </soapenv:Envelope>
    ```
    *   The `inputXml` now contains a JSON object with keys corresponding to your input parameter names (`I_FCY`, `I_EMPNUM`) and their respective values.

*   **SOAP Response Structure (with JSON `resultXml`):**

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" xmlns:wss="http://www.adonix.com/WSS">
        <soapenv:Body>
            <wss:runResponse soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
                <runReturn xsi:type="wss:CAdxResultXml">
                    <messages xsi:type="soapenc:Array" soapenv:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" soapenc:arrayType="wss:CAdxMessage[0]"></messages>
                    <resultXml xsi:type="xsd:string">
                        <![CDATA[{
                            "PARAM_STAT": {
                                "O_MESSAGE": "OK",
                                "O_STAT": "1"
                            }
                        }]]>
                    </resultXml>
                    <status xsi:type="xsd:int">1</status>
                    <technicalInfos xsi:type="wss:CAdxTechnicalInfos">
                        <!-- ... (technical info) ... -->
                    </technicalInfos>
                </runReturn>
            </wss:runResponse>
        </soapenv:Body>
    </soapenv:Envelope>
    ```
    *   The `resultXml` contains the JSON output, which in this case, only includes the `PARAM_STAT` block since `O_STAT` and `O_MESSAGE` are the only output parameters.

## Troubleshooting

*   **Input Data Validation:** If the web service returns an error (`O_STAT = 0`, `O_MESSAGE` populated), check the values of `I_FCY` and `I_EMPNUM`. Ensure they are valid and adhere to Sage X3's business rules (e.g., `NA023` must be a valid site, `801` a valid employee ID).
*   **Mask Specific Errors:** When integrating with masks, errors can stem from data integrity, missing mandatory fields (even if not exposed as web service inputs, the mask might require them), or security permissions on the underlying function. Check the X3 server logs for detailed messages.
*   **JSON Input Format:** Double-check that your `inputXml` contains valid JSON. Syntax errors in the JSON (e.g., missing commas, incorrect quotes) will cause the web service call to fail.
*   **Data Types:** Ensure the data types in your input JSON match what the Sage X3 web service expects (`"NA023"` as a string for `Alphanum`, `801` as a number for `Numeric`).

This comprehensive guide should equip you with the knowledge to create and consume Sage X3 web services with both input and output parameters, leveraging the powerful JSON output capabilities.vices with both input and output parameters, leveraging the powerful JSON output capabilities.
