# Polymer Example Setup

Taken from [http://www.polymer-project.org/docs/polymer/polymer.html](http://www.polymer-project.org/docs/polymer/polymer.html)

1. Create element template

```
<polymer-element name="tag-name" constructor="TagName">
  <template>
    <!-- shadow DOM here -->
  </template>
  <script>Polymer('tag-name');</script>
</polymer-element>
```

or with pure JS

```
<script>
  Polymer('name-tag', {nameColor: 'red'});
  var el = document.createElement('div');
  el.innerHTML = '\
    <polymer-element name="name-tag" attributes="name">\
      <template>\
        Hello <span style="color:{{nameColor}}">{{name}}</span>\
      </template>\
    </polymer-element>';
  // The custom elements polyfill can't see the <polymer-element>
  // unless you put it in the DOM.
  document.body.appendChild(el);    
</script>

<name-tag name="John"></name-tag>
```

2. Publish a property name to make it part of the public api.

This example shows 3 public properties foo, bar, baz
```
<polymer-element name="x-foo" attributes="foo bar baz">
  <script> 
    Polymer('x-foo');
  </script>
</polymer-element>
```

Gives the element attributes acess to run the methods.
```
<x-foo name="Joe"></x-foo>
```

3. Link the element to the page. (Also need polymer)
```
<link rel="import" href="path/to/x-dep.html">
```
4. Then call your tag
```
<amazing-tag name="best tag ever"></a>
```

