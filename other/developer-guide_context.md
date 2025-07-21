[Index](index.html)  [Home](getting-started_home.html)

Context

|  |  |  |
| --- | --- | --- |
| [Definition](#1-definition) | [Context initialization](#2-context-initialization) | [Access to context elements](#3-access-to-context-elements) |

# 1. Definition

In V12, the SAFE X3 engine is able to perform [stateless as well as stateful operations](getting-started_glossary-a-e.html#activity). The same SAFE X3 process is able to reply fast to a new request with a context that might change.

So, storing some default values in the global [V] variable class, even if it is still possible, would considerably limit the flexibility of the engine to serve quickly different requests.

This is why global variables use is now obsolete, and therefore it has to be replaced by a new feature. The new SAFE X3 Context feature has been introduced by the version 7 to replace the old "global variables" mechanism defined in function 'GESAGB', and to introduce various cache mechanisms to facilitate the retrieve of SAFE X3 parameter values in different cases.

The context code holds some context information that is relatively constant and stable, such as the current folder, current language and current user...

The main difference between the global variables defined in V6 and the context is that we can now have several contexts simultaneously: this can be interesting, for instance, if we need temporarily to have access to another set of global variables and parameters when performing an operation that involves several folders or several users.

The context itself is an instance of the class 'WMACONTEXT' (This means that developers cannot create another class named `WMACONTEXT` in the class dictionary). As the name of this class is subject to change in the future, it is better to use the constant `[V]CST_C_NAME_CLASS_CONTEXT`.

This means that declaring a new context pointer would be done by the following instruction:

`Local Instance MY_CONTEXT Using =[V]CST_C_NAME_CLASS_CONTEXT`

When a context pointer is sent to a `Subprog`, the declaration of the parameter to be done will be following the same pattern:

```
Subprog MY_PROG(MY_TEXT, VAR1, VAR2...)
Variable Instance MY_CONTEXT Using =[V]CST_C_NAME_CLASS_CONTEXT
...
```

  
A context is designed to be a container where the developers can put some basic global context information for a Sage X3 session. A context instance is created at the beginning of each Sage X3 session, and it provides access to several type of information :

* Context variables (the previous global variables, organized in chapters).
* Cache for general parameter values.
* Cache for "small tables" such as currencies, units... defined by "buffer classes".
* Parameters linked to the license definition.
* Data and methods to define the rights of a given user per function, companies, and sites.

The data needed to deliver all these services will be lazy loaded. Every time a resource is needed, the context class will load the data if not already stored in the context, otherwise the access will be direct. This is why creating a context is very fast and efficient, because only the data requested in a session will be loaded.

# 2. Context initialization

At connection time, the supervisor creates automatically a default global context instance called '[V]GACTX'. In every class instance, there is also a reference to a context (the global one, or another in some particular cases), and this reference is named 'ACTX'. This means that in an event where `this` is defined, `this.ACTX.USER` will give access to the user code performing the operation the event is called for.

In some cases, it might be interesting to create a dedicated context. This can be done by using the following methods:

## 2.1 Initialization of the whole context

In order to use all context facilities, the context must be initialized first, with the following methods (called by `Fmet` on the instance being created) :

`ACTX_INIT_LAN(AFOLDER, LAN, LOGIN)` returns 0 if OK, otherwise returns an error code.

`ACTX_INIT_LANISO(AFOLDER, LANISO, LOGIN)` returns 0 if OK, otherwise returns an error code.

The parameters are the following:

* `AFOLDER` is the folder code.
* `LAN` is the SAFE X3 language code.
* `LANISO` is the ISO language code.
* `LOGIN` is the SAFE X3 login code.

Example of creating a new context:

```
# Creating a new context on the same folder as the standard one but with another user code and language
Local Integer ERROR_CODE
Local Instance MY_CONTEXT_INSTANCE Using C_WMACONTEXT
  MY_CONTEXT_INSTANCE = NewInstance C_WMACONTEXT AllocGroup Null
  ERROR_CODE = fmet MY_CONTEXT_INSTANCE.ACTX_INIT_LAN(GACTX.FOLDER,"GER","JOHNDOE")
  If ERROR_CODE = 0
    # successful
  Elsif ERROR_CODE < 0
    # warning
  Else
    # error
  Endif
```

## 2.2 Context reinitialization

Context codes are all read-only and are first initialized by the 2 methods mentioned before.  
The initialization will be done in lazy mode and differently depending on the element:

* Using the Initialization Parameter/Formula/Program defined in the parameter dictionary.
* Using the parameter values stored in the global parameter value database.
* Using the corresponding database table for cached values.
* Using the license definition for the licensing data.

Once theyâre initialized, the reassignment of a value is not allowed. However, developers can reinitialize the whole Context codes at any time during a session. This is done by using the following method:

```
# We are here in a method called for a given class, so "This" is available
# This.ACTX is the current instance pointer on the context

Local Integer ERROR_CODE(3)

  ERROR_CODE = fmet this.ACTX.ACTX_RE_INIT()
  Case ERROR_CODE
    When 0 : # successful
    When 3 : # Context code reinitialize error
    When 4 : # Context cache clean error
  Endcase
```

## 2.3 Method for cache cleaning

If for any reason you need to clean the cache without changing the context definition, you have to call the method 'ACLEAN':

```
Local Integer ERROR_CODE

  ERROR_CODE = fmet this.ACTX.ACLEAN()

  Case ERROR_CODE
    When 0 : # successful
    When default : # error (not possible for the moment)
  Endcase
```

## 2.4 Error codes

All the three methods mentioned before can return an error code (status code). This error code gives developers necessary information to decide how the program will be directed after. Here below is the interpretation of the different error codes:

| Code | Signification |
| --- | --- |
| 0 | Successful. |
| -1 | warning : The given language code is not supported, the default language of the folder is applied instead. |
| 1 | error: The given folder not accessible. |
| 2 | error: Incorrect login. |
| 3 | error: Error when initialize Context codes. |
| 4 | error: Cache clean error (not possible for the moment). |

# 3. Access to context elements

As already mentioned above, at execution time, a context instance is created by default at the beginning of each Sage X3 session. This context instance is initialized with the current user, the current folder and the current language. The global variable 'GACTX' gives access to this context instance.

Besides, any functional class instantiated in Sage X3 includes a reference to the context named 'ACTX'. By default, `ACTX` references to `GACTX`, but developers are allowed to create other context instances to be referenced in their classes, and they can initialize the contexts in their own ways. (This will be the case if we need to access to another folder other than the current one, in a copy function for example.)

During the development, it is **strongly recommended** to :

* Use `this.ACTX` rather than `GACTX` to access context elements in the code attached to a class (a method definition). Otherwise, the code will not work if called with different contexts. All the examples given in this wiki page use : 'this.ACTX'.
* Use `GACTX` to access context elements only outside a class.

All the paths that access to the various information stored in the context will start from `GACTX` or from `this.ACTX`.

## 3.1 Context code variables

Context codes are to replace the old global variables defined in the V6 dedicated function (GESAGB). In V12, the new function defining the context codes is the [context dictionary (function GESACTX).](workbench-reference_context-dictionary.html). See the corresponding [documentation](developer-guide_context-global-variables.html).

## 3.2 Access to parameter values

`APARAM` is a child instance of class `ACONTEXT`, it implements a local cache to store the parameter values already accessed to avoid querying the database every time.

See the corresponding [documentation](developer-guide_context-parameters.html) to see the implementation and the eight public methods provided by APARAM cache.

## 3.3 Cached classes

Cached classes are dedicated classes intended to store in the context, values of "small" parameter tables such as currencies, units, language codes...

Refer to the corresponding [documentation](developer-guide_cached-classes.html) to see the implementation and the eight public methods provided by cached classes.

When such a class exists, the data from the corresponding table will be lazy loaded for every line that is requested. This is of course only usable with "small" tables that contains "few" useful data (usually a cache class does not contain all the columns of the table).

## 3.4 License data

The context class contains also a set of methods used to handle the rights granted by the license. See the corresponding [document](developer-guide_license.html) for more details.

## 3.5 Access rights managements

In Sage X3 version 7, the access rights always depend on the function code. The context supplies a set of methods that handle the access rights in a dedicated context cache. Refer to the corresponding [document](developer-guide_access-rights.html) for more details.

## 3.6 Additional context methods

The additional context methods are documented in the following [document](api-guide_api-context-methods.html) (also accessible from the API documentation section).

  

[Index](index.html)  [Home](getting-started_home.html)