[Index](index.html)  [Home](getting-started_home.html)

Escjson

This function replaces characters in a string, which are not allowed to appear in a JSON string, with their respective escape sequence.

# Syntax

The implementation of the **escJson** function follows the [JSON data interchange syntax standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/) (ECMA-404 Standard, 2nd Edition from December 2017).

A string is a sequence of Unicode code points wrapped with quotation marks (**U+0022**). You can place all code points within quotation marks except for code points that must be escaped:

* Quotation mark (**U+0022**)
* Reverse solidus (**U+005C**)
* Control characters from **U+0000** to **U+001F**

# Examples

```
Local Char MYCONSTANT(100),JSONCONSTANT(100)
MYCONSTANT='This is an "example" with back\slashes'
JSONCONSTANT='"myconstant" : "'+escJson(MYCONSTANT)+'"'
# Now JSONCONSTANT contains '"myconstant" : "This is an \"example\" with back\\slashes"'
```

# See also

[unescjson](4gl_unescjson.html)

  

[Index](index.html)  [Home](getting-started_home.html)