# Templates

The content of the <template> element is parsed by the parser, but it is inert: scripts aren't processed, images aren't downloaded, and so on. The <template> element is not rendered.
The content property holds the template in document fragment.

```
<template id="commentTemplate">
    <div>
        <img src="">
        <div class="comment-text"></div>
    </div>
</template>
<script>
function addComment(imageUrl, text) {
  var t = document.querySelector("#commentTemplate");
  var comment = t.content.cloneNode(true);
  // Populate content.
  comment.querySelector('img').src = imageUrl;
  comment.querySelector('.comment-text').textContent = text;
  document.body.appendChild(comment);
}
</script>
```
