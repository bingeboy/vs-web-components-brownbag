vs-web-components-brownbag
==========================

###Intro 

#####Web Components - Getting back to meaningful markup

[Web Components Spec](http://w3c.github.io/webcomponents/explainer/) _NOTE Web Components spec is still in draft. It appears to be replacing the HTMLElementElement which has been shelved._

#####Four key topics

* [Templates](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/templates.md), which define chunks of markup that are inert but can be activated for use later.
* [Shadow DOM](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/shadow-dom.md), which encapsulates a DOM subtree for more reliable composition of user interface elements.
* [Custom Elements](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/custom-element.md), which let authors define their own elements, with new tag names and new script interfaces.
* [Imports](https://github.com/bingeboy/vs-web-components-brownbag/blob/master/imports.md), which defines how templates and custom elements are packaged and loaded as a resource.

So we can create fully encapsulated, customized web components!

##Why would I do that? This sounds like new front end hipster madness. I'm trolling stack overflow.

Originally with the web we had these great simple tags that had inherent abilities.

We want to have tags that do what you need without customization.

####Examples

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



### The POLYMER-PROJECT Hottest Thing Since The \<blink\> Tag

Polymer is a library created by Google that uses polyfills in order to bring these custom web component to the latest versions of virtually all browsers.


### Applications of web components for Victoria's Secret

We will be able to build much of our module functionality right into the dom.

Imagine \<product\> tags, and \<bra\>, \<bikini\> tags extended from it.



### Running list of urls for talk
* http://w3c.github.io/webcomponents/explainer/
* http://www.html5rocks.com/en/tutorials/webcomponents/customelements/
* https://github.com/eduardolundgren/video-camera-element
* http://www.polymer-project.org/docs/start/getting-the-code.html

