

#Make a web component custom element

###Example
Making a new element named vs-swatch which must have a - per draft spec.
```
var Swatch = document.registerElement('vs-swatch');
document.body.appendChild(new Swatch());
document.getElementsByTagName("vs-swatch")[0].setAttribute("color", "red")
```
