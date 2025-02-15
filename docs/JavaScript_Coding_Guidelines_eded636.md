<!-- loioeded636b85584cd586b1fe231d2b5dac -->

| loio |
| -----|
| eded636b85584cd586b1fe231d2b5dac |

<div id="loio">

view on: [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/eded636b85584cd586b1fe231d2b5dac) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/eded636b85584cd586b1fe231d2b5dac)</div>

## JavaScript Coding Guidelines

Provides an overview of the guidelines for JavaScript coding for OpenUI5 with regard to code formatting, naming conventions, and creating classes.

For JavaScript, the following **general** guidelines apply:

-   Do **not** use global JavaScript variables; organize all global objects in an `sap.*` namespace structure. The module `sap/base/util/ObjectPath` assists in doing so. For more information, see [JavaScript Namespaces](JavaScript_Namespaces_5a978fe.md) and [API Reference: `jQuery.sap.getObject`](https://openui5.hana.ondemand.com/#/api/jQuery.sap/methods/jQuery.sap.getObject). 

    This also means: Do **not** use undeclared variables. When using global variables introduced by other libraries, declare the use in a special global comment: `/*global JSZip, OpenAjax */`.

-   Do **not** access internal \(private\) members of other objects.

-   Do **not** use `console.log()`

-   Use `window.document.getElementById("<someId>")` instead of `jQuery("#<someId>")` when `<someId>` is not a known string; certain characters in IDs need to be escaped for jQuery to work correctly.

-   Keep modifications of jQuery and other embedded Open Source to a minimum and document them clearly with the term *SAP modification*. Such modifications may **not** alter the standard behavior of the used library in a way that breaks other libraries


***

### Code Formatting

For any code becoming part of OpenUI5, an ESLint check needs to run successfully, see [Tools](Tools_41de83f.md). The following list contains the most important formatting rules:

-   Add a semicolon after each statement, even if optional

-   No spaces before and after round braces \(function calls, function parameters\), but…

-   …use spaces after `if/else/for/while/do/switch/try/catch/finally`, around curly braces, around operators and after commas

-   Opening curly brace \(functions, for, if-else, switch\) is on the same line

-   Use "===" and "!==" instead of "==" and "!="; see the ESLint docu for special cases where "==" is allowed

-   The code should therefore look like this:

    ``` js
    
    function outer(c, d) {
            var e = c * d;
            if (e === 0) {
                e++;
            }
            for (var i = 0; i < e; i++) {
                // do nothing
            }
    
            function inner(a, b) {
                return (e * a) + b;
            }
    
            return inner(0, 1);
        }
    
    ```


***

### Naming Conventions

We strongly recommend to use the Hungarian notation where name prefixes indicate the type for variables and object field names. But do **not** use the Hungarian notation for API method parameters: The documentation specifies the type in this case.

When using the Hungarian notation, use the prefixes highlighted below and continue with an uppercase letter \(camelCase\):


<table>
<tr>
<th>

Sample



</th>
<th>

Type



</th>
</tr>
<tr>
<td>

**s**Id



</td>
<td>

string



</td>
</tr>
<tr>
<td>

**o**DomRef



</td>
<td>

object



</td>
</tr>
<tr>
<td>

**$**DomRef



</td>
<td>

jQuery object



</td>
</tr>
<tr>
<td>

**i**Count



</td>
<td>

int



</td>
</tr>
<tr>
<td>

**m**Parameters



</td>
<td>

map / assoc. array



</td>
</tr>
<tr>
<td>

**a**Entries



</td>
<td>

array



</td>
</tr>
<tr>
<td>

**d**Today



</td>
<td>

date



</td>
</tr>
<tr>
<td>

**f**Decimal



</td>
<td>

float



</td>
</tr>
<tr>
<td>

**b**Enabled



</td>
<td>

boolean



</td>
</tr>
<tr>
<td>

**r**Pattern



</td>
<td>

RegExp



</td>
</tr>
<tr>
<td>

**fn**Function



</td>
<td>

function



</td>
</tr>
<tr>
<td>

**v**Variant



</td>
<td>

variant types



</td>
</tr>
<tr>
<td>

**p**Dialog



</td>
<td>

promise



</td>
</tr>
</table>

Use CamelCase for class names, starting with an uppercase letter. HTML element IDs starting with `sap-ui-` are reserved for OpenUI5. DOM attribute names starting with `data-sap-ui-` as well as URL parameter names starting with `sap-` and `sap-ui-` are reserved for OpenUI5.

The following IDs are currently used:


<table>
<tr>
<th>

ID



</th>
<th>

Description



</th>
</tr>
<tr>
<td>

`sap-ui-bootstrap`



</td>
<td>

ID of the bootstrap script tag



</td>
</tr>
<tr>
<td>

`sap-ui-library-*`



</td>
<td>

Prefix for UI libraries script tags



</td>
</tr>
<tr>
<td>

`sap-ui-theme-*`



</td>
<td>

Prefix for theme stylesheets link tags



</td>
</tr>
<tr>
<td>

`sap-ui-highlightrect`



</td>
<td>

ID of the highlight rect for controls in TestSuite



</td>
</tr>
<tr>
<td>

`sap-ui-blindlayer-*`



</td>
<td>

ID for `BlockLayer`



</td>
</tr>
<tr>
<td>

`sap-ui-static`



</td>
<td>

ID of the static popup area of UI5



</td>
</tr>
<tr>
<td>

`sap-ui-TraceWindowRoot`



</td>
<td>

ID of the `TraceWindowRoot`



</td>
</tr>
<tr>
<td>

`sap-ui-xmldata`



</td>
<td>

ID of the `XML Data Island`



</td>
</tr>
</table>

***

### Creating Classes

For the creation of classes, the following rules and guidelines apply:

-   Initialize and describe instance fields in the constructor function: `this._bReady = false; // ready to handle requests`

-   Define instance methods as members of the prototype of the constructor function: `MyClass.prototype.doSomething = function(){...`

-   Define static members \(fields and functions\) as members of the constructor function object itself: `MyClass.doSomething = function(){...`

-   Start the name of private members with an underscore: `this._bFinalized`

-   Combine constructor + methods + statics in a single JS source file named and located after the qualified name of the class; this is a precondition for class loading

-   Static classes do not have a constructor but an object literal; there is no pattern for inheritance of such classes. If inheritance is needed, use a normal class and create a singleton in the class.

-   Do not use `SuperClass.extend(…)` for subclasses. If no base class exists, the prototype is automatically initialized by JavaScript as an empty object literal and must not be assigned manually. Consider inheriting from `sap/ui/base/Object`

-   Subclasses call \(or apply\) the constructor of their base class: `SuperClass.apply(this, arguments);`


For more information, see [Example for Defining a Class](Example_for_Defining_a_Class_f6fba4c.md).

-   **[JavaScript Namespaces](JavaScript_Namespaces_5a978fe.md "OpenUI5 modules such as
		classes, components, and controls, should use a consistent qualified naming scheme. Each
		module should reside in a unique namespace.")**  
OpenUI5 modules such as classes, components, and controls, should use a consistent qualified naming scheme. Each module should reside in a unique namespace.
-   **[Example for Defining a Class](Example_for_Defining_a_Class_f6fba4c.md "Full example of a class definition, including JSDoc")**  
Full example of a class definition, including JSDoc

