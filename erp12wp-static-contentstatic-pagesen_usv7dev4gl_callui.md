[Index](index.html)  [Home](getting-started_home.html)

Callui

`Callui` is used to execute a pre-determined action on the web client.

**This function is only usable in Classic pages related code and is deprecated for code running in version 7 mode.**

# Syntax

Callui `RETURN` = "" With `ACTION`, `PARAM_LIST`

Where:

* `RETURN` is a string variable that contains the information returned by the call.
* `ACTION` is a character string that contains the action definition with the following syntax:

  + "UIAction=" + chr$(1) + "action\_value"
* `PARAM_LIST` is a list of `PARAM_ID` separated by the character ','.
* `PARAM_ID` is a character string (its length is limited to 250 characters) with the following syntax:

  + "UiParam=" + chr$(1) + "param\_value"

# Examples

```
# Example 1: open a browser tab and navigate to Sage official web site
Local Char RETOUR(250)
Callui RETVALUE="" With     "UIAction=" + chr$(1) + "OpenFile",
&                           "UILocalDir=" + chr$(1) + "HTTP",
&                           "UILocalFile=" + chr$(1) + "www.sage.com"

# Example 2: open a browser tab and navigate to secured Google web site
Callui RETVALUE="" With     "UIAction=" + chr$(1) + "OpenFile",
&                           "UILocalDir=" + chr$(1) + "HTTPS",
&                           "UILocalFile=" + chr$(1) + "www.google.com"

# Example 3: open a browser tab and navigate to an url corresponding to a 
# sub-file of the current folder under the mount point address of the 
# application server
Callui RETVALUE="" With     "UIAction=" + chr$(1) + "OpenFile",
&                           "UILocalDir=" + chr$(1) + "HTTPS",
&                           "UILocalFile=" + chr$(1) + "GEN/SYR/FR-FR/FENJ/",
&                           "UILocalFile=" + chr$(2) + "OAMK.json",
&                           "UIAdxPubSubFile=" + chr$(1) + "3"

# Example 4: open a browser tab and navigate to an url corresponding to a 
# sub-file of the âX3_ROOTâ folder under the mount point address of the 
# application server
Callui RETVALUE="" With     "UIAction=" + chr$(1) + "OpenFile",
&                           "UILocalDir=" + chr$(1) + "HTTPS",
&                           "UILocalFile=" + chr$(1) + "GEN\FRA\LIB\localize.json",
&                           "UIAdxPubSubFile=" + chr$(1) + "2"
```

# Description

Callui is used to launch one of the following actions on the web client:

* open a browser tab on the client browser and prompt a word wide web URL passed in the `UILocalFile` parameter.
* open a browser tab on the client browser and prompt the URL to a sub-file of the "X3\_PUB" folder of an application server. The `UILocalFile` parameter contains the relative URL and the `UIAdxPubSubFile` parameter must be set to 2 or 3 (see detail below).

A single action can be specified at a time.

On completion, a code specifies that the action has been correctly carried out or not.

# UIAction parameter

This parameter is used to identify the action to be launched on the client.   
  
The available actions are as follows:

| Action | Description |
| --- | --- |
| OpenFile | Open a browser tab on the client browser and prompt a web URL |

# UIParam parameters

They are used to specify the parameters of an action.

The list of parameters is the following:

| Parameters | Mandatory | Description |
| --- | --- | --- |
| UILocalFile | Yes | Full or relative URL, depending if `UIAdxPubSubFile` parameter is set or not.  For a full URL, value must not contain the prefix "http://" or "https://".   Parameter value cannot exceed 240 characters. |
| UILocalDir | Yes | Contains the protocol name: HTTP or HTTPS.  Regardless the value for this parameter (i.e. HTTP or HTTPS), if parameter `UIAdxPubSubFile` is set, the full URL is automatically computed, based on the current session protocol. |
| UIAdxPubSubFile | No | If this parameter is set, UILocalfile parameter must contain a relative URL based on :   * subdirectory âX3\_ROOT" under the mount point address of the application server if `UIAdxPubSubFile` =2 * subdirectory corresponding to the current folder name under the mount point address of the application server if `UIAdxPubSubFile` =3 |
| UIWindowFeatures | No | If this parameter is set, a standalone browser is opended instead of a new browser tab. Width and height of the browser window are defined in pixels : `"UIWindowFeatures=" + chr$(1) + "width=300,height=300"` |
| UIWindowTimeOut | No | If `UIWindowFeatures` is set, this parameter force the auto close of the standalone browser after a specified number of milliseconds has elapsed : `"UIWindowTimeOut=" + chr$(1) + "10000"`. |

# Return

This parameter is used to identify the variable that will contain the information on the return of the instruction.  
The instruction returns the name of the action, followed by the status code.

The status code takes one of the following values:  
\* 1 : the action unfolded as planned   
  
\* 0 : an error occurred during the action.

# Associated errors

none

# Associated keywords

none

  

[Index](index.html)  [Home](getting-started_home.html)