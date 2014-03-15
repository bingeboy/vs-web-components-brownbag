#Imports

The HTML Imports specification is the normative description of this part of Web Components.

Custom elements can be loaded from external files using the link tag:

```
<link rel="import" href="goodies.html">
```
The DOM of this document is available to script through the import property. Documents which are retrieved cross-origin use CORs to determine that the definitions are designed to run cross-site.

