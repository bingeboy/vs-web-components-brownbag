vs-web-components-brownbag
==========================

Office Brown Bag

###Intro 

#####Web Components - Getting back to meaningful markup

[Spec](http://w3c.github.io/webcomponents/explainer/) NOTE Web Components spec is still in draft. It appears to be replacing the HTMLElementElement which has been shelved.

#####Four key components

* [Templates](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/templates.md), which define chunks of markup that are inert but can be activated for use later.
* [Custom Elements](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/custom-element.md), which let authors define their own elements, with new tag names and new script interfaces.
* [Shadow DOM](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/shadow-dom.md), which encapsulates a DOM subtree for more reliable composition of user interface elements.
* [Imports](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/imports.md), which defines how templates and custom elements are packaged and loaded as a resource.


##Why would I do that? This sounds like new front end hipsters madness. I'm trolling stack overflow.


##### Custom Element myth
"Sorry <randomtag>! You're non-standard and inherit from HTMLUnknownElement." - Professional Internet Troll.

```
// "tabs" is not a valid custom element name
document.createElement('tabs').__proto__ === HTMLUnknownElement.prototype

// "x-tabs" is a valid custom element name
document.createElement('x-tabs').__proto__ == HTMLElement.prototype
```

##### LifeCycle Callbacks
* createdCallback	- an instance of the element is created
* attachedCallback -	an instance was inserted into the document
* detachedCallback	- an instance was removed from the document
* attributeChangedCallback(attrName, oldVal, newVal)	- an attribute was added, removed, or updated

```
var proto = Object.create(HTMLElement.prototype);

proto.createdCallback = function() {...};
proto.attachedCallback = function() {...};

var XFoo = document.registerElement('x-foo', {prototype: proto});
```
####Demo

#####Markup
```
var XFooProto = Object.create(HTMLElement.prototype);

XFooProto.createdCallback = function() {
  this.innerHTML = "<b>I'm an x-foo-with-markup!</b>";
};

var XFoo = document.registerElement('x-foo-with-markup', {prototype: XFooProto});
```

#####Shadow Dom
```
var XFooProto = Object.create(HTMLElement.prototype);

XFooProto.createdCallback = function() {
  // 1. Attach a shadow root on the element.
  var shadow = this.createShadowRoot();

  // 2. Fill it with markup goodness.
  shadow.innerHTML = "<b>I'm in the element's Shadow DOM!</b>";
};

var XFoo = document.registerElement('x-foo-shadowdom', {prototype: XFooProto})
```
##### Templates
```
<template id="sdtemplate">
  <style>
    p { color: orange; }
  </style>
  <p>I'm in Shadow DOM. My markup was stamped from a &lt;template&gt;.</p>
</template>

<script>
var proto = Object.create(HTMLElement.prototype, {
  createdCallback: {
    value: function() {
      var t = document.querySelector('#sdtemplate');
      var clone = document.importNode(t.content, true);
      this.createShadowRoot().appendChild(clone);
    }
  }
});
document.registerElement('x-foo-from-template', {prototype: proto});
</script>
```

##### CSS
```
<style>
  app-panel {
    display: flex;
  }
  [is="x-item"] {
    transition: opacity 400ms ease-in-out;
    opacity: 0.3;
    flex: 1;
    text-align: center;
    border-radius: 50%;
  }
  [is="x-item"]:hover {
    opacity: 1.0;
    background: rgb(255, 0, 255);
    color: white;
  }
  app-panel > [is="x-item"] {
    padding: 5px;
    list-style: none;
    margin: 0 7px;
  }
</style>

<app-panel>
  <li is="x-item">Do</li>
  <li is="x-item">Re</li>
  <li is="x-item">Mi</li>
</app-panel>
```
#### FOUT Mitigation Built In

```
<style>
  x-foo {
    opacity: 1;
    transition: opacity 300ms;
  }
  x-foo:unresolved {
    opacity: 0;
  }
</style>

```

```
<style>
  /* apply a dashed border to all unresolved elements */
  :unresolved {
    border: 1px dashed red;
    display: inline-block;
  }
  /* x-panel's that are unresolved are red */
  x-panel:unresolved {
    color: red;
  }
  /* once the definition of x-panel is registered, it becomes green */
  x-panel {
    color: green;
    display: block;
    padding: 5px;
    display: block;
  }
</style>

<panel>
  I'm black because :unresolved doesn't apply to "panel".
  It's not a valid custom element name.
</panel>

<x-panel>I'm red because I match x-panel:unresolved.</x-panel>
```

### Browser Support Check
```
function supportsCustomElements() {
  return 'registerElement' in document;
}

if (supportsCustomElements()) {
  // Good to go!
} else {
  // Use other libraries to create components.
}
```



### The POLYMER-PROJECT Hottest Thing Since The <blink/> Tag

Polymer is a library that uses the latest web technologies to let you create custom HTML elements.





### Running list of urls for talk
* http://w3c.github.io/webcomponents/explainer/
* http://www.html5rocks.com/en/tutorials/webcomponents/customelements/
* https://github.com/eduardolundgren/video-camera-element
* http://www.polymer-project.org/docs/start/getting-the-code.html

