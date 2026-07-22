# Images how-to

Files in this folder are not automatically included in the generated site.

To include them, link to an image like so:

```md
<!-- Be sure to add an `alt` attribute for accessibility! -->
{% picture _images/example.png alt="A placeholder example description" %}

<!-- Float the image left or right with a CSS class: -->
{% picture _images/example.png alt="A placeholder example description" class="float-left-50" %}
{% picture _images/example.png alt="A placeholder example description" class="float-right-50" %}
```

We're using [`jekyll_picture_tag`](https://github.com/rbuchberger/jekyll_picture_tag) to generate multiple resolutions and formats for each image. This will generate an optimized version of the image in several different resolutions.
