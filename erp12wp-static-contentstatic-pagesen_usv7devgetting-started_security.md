[Index](index.html)  [Home](getting-started_home.html)

Security

# Main principles

For Versions 7 and above platform, security is governed by following rules:  
\* Standard web browsers and 'https' protocol are used. The web technology provides a first level insulation between the web server and the workstation.  
\* Passwords are not transferred on the network. The authentication system is based on standards. The following options are available:   
 1. The Windows login that is controlled in an [LDAP directory](administration-reference_ldap.html),   
 2. An [Oauth2 authentication](administration-reference_oauth2.html) (a redirection is done to the authentication server).   
\* The connection between the Sage X3 Web Server and the Sage X3 server is based on [certificates](getting-started_certificate-installation.html) that are created at installation time by a private certificate authority.  
\* Rights managements are done at service level and are based on function profiles associated with the user.  
\* The access of the Sage X3 processes to the server is restricted by a [white list](getting-started_sandbox-configuration-file.html) of authorized directories.  
\* On the Sage X3 Web Server, the processes and/or the services that 'node.js' and 'mongodb' do not require to be root or have administrator privileges.

One of the consequences of this is that the management of passwords that was handled by Sage X3 is now obsolete and no more used; the security rules for passwords are now managed by the security providers (google, LDAP rules) you choose.

**Note:** For simplicity reasons or for autonomous demo servers), a fallback solution based on users and encrypted passwords stored in the Sage X3 Web Server is available, but is not to be used for production environments.

# Security parameters

The syracuse web server has different parameters to tune the security. The configuration is based on a dedicated `security` section in the `nodelocale.js` file.

## HTTP headers

### clickjacking

The server is protected against [clickjacking](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet) by adding the `x-frame-options: DENY` http header.

If for any reason you need to be able to put the site into an iframe, you can do it \*\*\*at your own risk\*\*\* by overriding the default as follows:

```
CODECODE CODEjs
exports.config = {
    security: {
    http: {
        headers: {
                // set 'x-frame-options' to enable embedding into another site via iframe
            // 'x-frame-options': 'allow-from http://other-site',
            'x-frame-options': 'SAMEORIGIN', // default value is 'DENY'
        },
        },
    },
};
```

> **Before U9.0.3**
>
> The header was directly under the `http`as follows:
>
> ```
> CODECODE CODEjs
> exports.config = {
>     security: {
>         http: {
>         // set 'x-frame-options' to enable embedding into another site via iframe
>         // 'x-frame-options': 'allow-from http://other-site',
>         // 'x-frame-options': 'SAMEORIGIN',
>         'x-frame-options': 'DENY' // default value
>     },
>     },
> };
> ```

### XSS and other defense headers

Any headers in the `headers` property will be added in the response. By default, the following are added:

* `x-content-type-options: nosniff`: Prevents Internet Explorer and Google Chrome from [MIME-sniffing](https://blogs.msdn.microsoft.com/ie/2008/09/02/ie8-security-part-vi-beta-2-update/)
* `x-xss-protection: 1; mode=block`: Enables the Cross-site scripting [(XSS) filter](https://blogs.msdn.microsoft.com/ie/2008/07/02/ie8-security-part-iv-the-xss-filter/) built into most recent web browsers
* `content-security-policy: frame-ancestors 'self'`: New standard to prevent clickjacking, will allow your site only.

The `content-security-policy` has many [directives](https://www.w3.org/TR/CSP2/) you can use to control what the browser can render. Among all directives we can mention:

* `default-src`: This directive is used as default for the following more fine grained directives should they not be specified.
* `script-src`: Trust only script sources in the list
* `child-src`: **Deprecated**: Trust only embedded content in the list. This directive will control what can be loaded in an iframe or web-workers.
* `frame-src`: Trust only embedded content in the list. This directive will control what can be loaded in an iframe. If `frame-src` is not specified it defaults to `child-src` which defaults to `default-src` if not present.
* `worker-src`: Trust only web workers in the list. If `worker-src` is not specified it defaults to `script-src` which defaults to `default-src` if not present.
* `frame-ancestors`: Similar to the `x-frame-options` header but if both exists the w3c spec mention that the `frame-ancestors` must be used.

**Note on child-src, frame-src and worker-src**

The directive `frame-src` was deprecated by CSP version 2 but has recently been undeprecated in favour to `child-src`.  
The web standard defines `frame-src` and `worker-src` to be used in the future. In conclusion, it's best so specify `frame-src` and `worker-src` since these allow more fine grained control when using up to date browsers. Still setting `child-src`to be there as a fallback for old browsers

These directives can be modified as sub-properties of `content-security-policy` as follows:

```
CODECODE CODEjs
exports.config = {
    security: {
        http: {
            headers: {
                "content-security-policy": {
                    "frame-src": ["'self'", "www.w3schools.com"]
                },
            },
    },
    },
};
```

  
[HTML5 rocks](http://www.html5rocks.com/en/) provides a good [tutorial](http://www.html5rocks.com/en/tutorials/security/content-security-policy/)

Debugging `content-security-policy`issues. While hardening the security configuration it may happen to many resources get blocked and make the system unusable. To avoid this, it is possible to only report potential violations but not block them effectively.  
To report violations, set the property `content-security-policy-report-only` instead of `content-security-policy`.

The above configuration would look like:

```
CODECODE CODEjs
exports.config = {
    security: {
        http: {
            headers: {
                "content-security-policy-report-only": {
                    "frame-src": ["'self'", "www.w3schools.com"]
                },
            },
    },
    },
};
```

  
It is also possible to set both `content-security-policy` and `content-security-policy-report-only`. This will block access to resources as defined in `content-security-policy` while only reporting additional violations caused by directives put in `content-security-policy-report-only` without blocking them.

**`content-security-policy-report-only` will only report access violations but not block them in any way so it's very important to replace it with `content-security-policy` once the configuration was successfully tested**

## Content security

The user interface can include some external contents by using iframe. Including such contents may corrupt the security of the site, but by adding the `sandbox` attribute to the iframe HTML tags we can reduce the risk.

### iframe sandbox

HTML vignettes support 3 levels (`low`, `medium`, `high`) of security.   
Per default, these levels define the [sandbox attribute](http://www.w3schools.com/tags/att_iframe_sandbox.asp) as follows:

* `low`: `"allow-same-origin allow-forms allow-popups allow-scripts"`
* `medium`: `"allow-forms allow-scripts"`
* `high`: `""`

As of today, the medium level is selected per default to compute the sandbox attribute.

### Customizing the sandbox attribute

You can change the default authorization of the 3 levels by editing the `security` section in `nodelocal.js`.  
Each of the 3 levels can consist of one or more of the supported elements of the sandbox attribute:  
\* allow-forms Enables form submission  
\* allow-pointer-lock Enables pointer APIs (for example pointer position)  
\* allow-popups Enables popups  
\* allow-same-origin Allows the iframe content to be treated as being from the same origin  
\* allow-scripts Enables scripts  
\* allow-top-navigation Allows the iframe content to navigate its top-level browsing context

**Examples**

```
CODECODE CODEjs
exports.config = {
    security: {
        client: {
        iframe: {
        sandbox: {
            // low: null, // if null no sandbox attribute will be added (not recommended)
            // medium: null, // if null no sandbox attribute will be added (not recommended)
            low: "allow-same-origin allow-forms allow-popups allow-scripts",
            medium: "allow-same-origin allow-forms allow-scripts",
            high: ""
        }
        }
    },
    },
};
```

  
**Be aware that there is a difference in setting a sandbox level to null or setting it to "" (empty)**  
\* **null**: Do not put the sandbox attribute. This means there is no restriction at all and **everything is allowed**.  
\* **""**: Put the sandbox attribute with no additional elements. This means **nothing is allowed**.

**It's highly recommended to not set any of the security levels to null.** In case of doing so please make sure to at least restrict access to resources by setting the `content-security-policy` accordingly.

In general, combining the `sandbox` attribute and the `frame-src` and `child-src` directive of the `content-security-policy` provide a better control of what can be rendered in the browser.

### Examples

#### Example 1 - Control web page gadgets

**Setup**

**Create 2 external links with the following url:**

1. <http://www.w3schools.com/tags/demo_iframe_sandbox_origin.htm>
2. <http://www.w3schools.com/tags/demo_iframe_sandbox_form.htm>

**Create a new landing page**

**Add a web gadgets for both external links above**

**Test**

By default your 2 gadgets are displayed and you can submit the form data.

For web gadgets, the `medium` level is used, so in the `nodelocale.js` file, change the `security.client.iframe.sandbox.medium` property as follows:

```
CODECODE CODEjs
medium: "allow-same-origin allow-scripts",
```

  
Restart the server and now you no longer able to submit the form data.

Do the same by removing `allow-same-origin`, now the `demo_iframe_sandbox_origin` page cannot load the book list with the ajax request.

Finally, edit the `security.http.headers` property to add a `content-security-policy` header as follows:

```
CODECODE CODEjs
exports.config = {
    security: {
        http: {
        headers: {
            "content-security-policy": {
            "frame-src": ["'self'"]
        },
        },
    },
    },
};
```

  
Restart the server and now none of the iframes are rendered.

#### Example 2 - Block external resources except pendo.io

Edit the `security.http.headers` property to add a `content-security-policy` header as follows:

```
CODECODE CODEjs
exports.config = {
    security: {
        http: {
        headers: {
        "content-security-policy": {
            "default-src": ["'self'", "'unsafe-inline'"],
            "connect-src": ["'self'", "ws:", "wss:"],
            "script-src": ["'self'", "'unsafe-inline'", "'unsafe-eval'", "cdn.pendo.io", "app.pendo.io"],
            "img-src": ["'self'", "data:", "app.pendo.io"],
            "child-src": ["self"], // Compatibility for older browsers
            "frame-src": ["'self'"]
        }
        },
    },
    },
};
```

  
Restart the server and now no external resources like images or scripts will be downloaded by the browser except for pendo.io

## Manage allowed protocol and encryption algorithm

### Configuration

As an administrator and for security purposes, it is important to be able to set allowed or forbidden protocols and encryption algorithms.  
  
The configuration of the options used to create a TLS server can be managed by editing the `security` section in the `nodelocal.js` file. This configuration ensures that the TLS V1.2 protocol is used and forbids RC4 and CBC encryption.

#### Example - nodelocal configuration for TLS

Edit the `security.tls` property to add `renegotiation` and `context` parameters as follows:

```
CODECODE CODEjs
const constants = require('constants');

exports.config = {
    security: {
        tls: {
         // For up to date recommendations on TLS security
        // see https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet#Server_Protocol_and_Cipher_Configuration
            renegotiation: {
                    limit: 3, // default 3
                    window: 600 // default 600 (10 minutes)
                    },
            context: {
                           // Cipher suite accepted
                ciphers: 'EDH+aRSA+AESGCM:EDH+aRSA+AES:EECDH+aRSA+AESGCM:EECDH+aRSA+AES:-SHA' +
                ':ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:RSA+AESGCM:RSA+AES+SHA256:RSA+AES+SHA' +
                ':DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA' +
                ':!aNULL:!eNULL:!LOW:!MD5:!EXP:!PSK:!DSS:!RC4:!SEED:!ECDSA:!ADH:!IDEA',
                           // Use the server's cipher suite preferences instead of the client's one (recommended)
                           honorCipherOrder: true,
                           // Rejected protocols known as unsecured (SSL V2, V3, TLS V1.0, V1.1)
                           secureOptions: constants.SSL_OP_NO_SSLv2 | constants.SSL_OP_NO_SSLv3 | constants.SSL_OP_NO_TLSv1 | constants.SSL_OP_NO_TLSv1_1
                       }
                 }
            },
        };
```

  
Note: It is important to declare the constants at the beginning of the file. Do not put a chain, this would false the result.

### Verifying the expected behavior

Here are several tests you can run to ensure that the TLS security level meets the requirements.  
These tests consider that an HTTPS server is running on port 8126. The standard port of an HTTPS server is 443.

#### Example 1 - Test TLS v1.0 protocol

```
CODECODE CODEsh
$ openssl s_client -tls1 -connect localhost:8126
CONNECTED(00000204)

no peer certificate available

No client certificate CA names sent

SSL handshake has read 0 bytes and written 0 bytes

New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1
    Cipher    : 0000
    Session-ID:
    Session-ID-ctx:
    Master-Key:
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1529961360
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)

20556:error:1409E0E5:SSL routines:ssl3_write_bytes:ssl handshake failure:s3_pkt.c:659:
```

#### Example 2 - Test RC4 cipher suites

```
CODECODE CODEsh

$ openssl s_client -cipher ECDHE-RSA-RC4-SHA:ECDHE-ECDSA-RC4-SHA:ECDH-RSA-RC4-SHA:ECDH-ECDSA-RC4-SHA:RC4-SHA:RC4-MD5:PSK-RC4-SHA -connect localhost:8126
CONNECTED(00000220)

no peer certificate available

No client certificate CA names sent

SSL handshake has read 7 bytes and written 150 bytes

New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : 0000
    Session-ID:
    Session-ID-ctx:
    Master-Key:
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1529961371
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)

10480:error:14077410:SSL routines:SSL23_GET_SERVER_HELLO:sslv3 alert handshake failure:s23_clnt.c:802:
```

#### Example 3 - Test CBC cipher suites

```
CODECODE CODEsh
$ openssl s_client -cipher SRP-DSS-AES-256-CBC-SHA:SRP-RSA-AES-256-CBC-SHA:SRP-AES-256-CBC-SHA:PSK-AES256-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:SRP-RSA-AES-128-CBC-SHA:SRP-AES-128-CBC-SHA:IDEA-CBC-SHA:PSK-AES128-CBC-SHA:ECDHE-RSA-DES-CBC3-SHA:ECDHE-ECDSA-DES-CBC3-SHA:SRP-DSS-3DES-EDE-CBC-SHA:SRP-RSA-3DES-EDE-CBC-SHA:SRP-3DES-EDE-CBC-SHA:EDH-RSA-DES-CBC3-SHA:EDH-DSS-DES-CBC3-SHA:DH-RSA-DES-CBC3-SHA:DH-DSS-DES-CBC3-SHA:ECDH-RSA-DES-CBC3-SHA:ECDH-ECDSA-DES-CBC3-SHA:DES-CBC3-SHA:PSK-3DES-EDE-CBC-SHA -connect localhost:8126
CONNECTED(00000218)

no peer certificate available

No client certificate CA names sent

SSL handshake has read 7 bytes and written 158 bytes

New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : 0000
    Session-ID:
    Session-ID-ctx:
    Master-Key:
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1529961383
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)

16904:error:14077410:SSL routines:SSL23_GET_SERVER_HELLO:sslv3 alert handshake failure:s23_clnt.c:802:
```

#### Example 4 - Test including an accepted cipher (ECDHE-RSA-AES256-GCM-SHA384)

```
CODECODE CODEsh
$ openssl s_client -cipher RC4-SHA:RC4-MD5:DES-CBC3-SHA:ECDHE-RSA-AES256-GCM-SHA384 -connect localhost:8126
CONNECTED(00000208)

Certificate chain
 0 s:/CN=....
   i:/C=....
 1 s:/C=....
   i:/C=...

Server certificate
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
subject=/CN=....
issuer=/C=....

No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: ECDH, P-256, 256 bits

SSL handshake has read 2368 bytes and written 272 bytes

New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: ....
    Session-ID-ctx:
    Master-Key: .....
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:....

    Start Time: 1529961397
    Timeout   : 300 (sec)
    Verify return code: 19 (self signed certificate in certificate chain)

depth=1 C = ....
verify error:num=19:self signed certificate in certificate chain
read:errno=10093
```

#### Example 5 - Test with default connect

```
CODECODE CODEsh
$ openssl s_client -connect localhost:8126
CONNECTED(00000134)

Certificate chain
 0 s:/CN=....
   i:/C=....
 1 s:/C=....
   i:/C=...

Server certificate
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
subject=/CN=....
issuer=/C=....

No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: ECDH, P-256, 256 bits

SSL handshake has read 2368 bytes and written 434 bytes

New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: ....
    Session-ID-ctx:
    Master-Key: .....
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:....

    Start Time: 1529961553
    Timeout   : 300 (sec)
    Verify return code: 19 (self signed certificate in certificate chain)

depth=1 C = ....
verify error:num=19:self signed certificate in certificate chain
read:errno=10093
```

  

[Index](index.html)  [Home](getting-started_home.html)