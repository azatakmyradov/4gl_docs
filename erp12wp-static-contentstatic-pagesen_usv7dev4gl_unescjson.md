[Index](index.html)  [Home](getting-started_home.html)

Unescjson

This function restores an escaped JSON string to its original state. It replaces the escape sequences within the string with the respective character they represent.

# Syntax

The implementation of the **UnescJson** function follows the [JSON data interchange syntax standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/) (ECMA-404 Standard, 2nd Edition from December 2017).

A string is a sequence of Unicode code points wrapped with quotation marks (**U+0022**). You can place all code points within quotation marks except for code points that must be escaped:

* Quotation mark (**U+0022**)
* Reverse solidus (**U+005C**)
* Control characters from **U+0000** to **U+001F**

# Examples

```
Local Char JSONCONSTANT(100), MYCONSTANT(100)
JSONCONSTANT='This is an \"example\" with back\\slashes'
MYCONSTANT=unescJson(JSONCONSTANT)
# Now MYCONSTANT contains 'This is an "example" with back\slashes'
```

# See also

[escjson](4gl_escjson.html)

  

[Index](index.html)  [Home](getting-started_home.html)