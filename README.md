# Website

This repository contains the North End Makerspace website.

## Building and Running

This website is built using [GitHub Pages](https://docs.github.com/en/pages) and [Jekyll](https://jekyllrb.com/).

With [Ruby](https://www.ruby-lang.org/en/) installed<sup>[1]</sup>, run:

```sh
bundle install
bundle exec jekyll serve
```

Your local test server will be at [http://localhost:4000](http://localhost:4000).

<sup>[1]</sup>This project contains a [Development Container](https://containers.dev/) configuration at `.devcontainer/devcontainer.json`, which can be used to simplify project setup.

## Contributing

### Add or Edit a Page

1. Add a `.html` or `.md` page to [`src/`](./src/) or a subdirectory with the following content:
   ```
   ---
   layout: base
   title: An Example Page
   description: "An example description-- put it in quotes if it's got a single quote and put a backslach in front of double quotes or other special characters (which is called \"escaping\" the text)"
   ---
   # Your content

   [..]
   ```
   These will become pages on the website. For example, the file at [`src/about.html`](./src/about.html) becomes [https://northendmakers.org/about/](https://northendmakers.org/about/).
2. To create a blog post, create a file inside [`src/_posts`](./src/_posts) named `YYYY-MM-DD-page-slug.md` with the following content:
   ```
   ---
   layout: post
   title: An Exciting Post
   description: A sentence or two summarizing your post.
   author: Your Name Here
   ---
   ## Your content

   Consider starting at heading level 2-- your page title is added under heading level 1 by `layout: post`.

   [..]
   ```
   By convention, images for these posts should be grouped together under `src/_images/YYYY-MM-DD-page-slug/*`.
3. Directories under [`src/`](./src/) that start with an underscore (e.g. [`src/_layouts`](./src/_layouts), or [`src/_images`](./src/_images)) are special and do not automatically become pages.

### Adding an Image

1. Copy your image to [`src/_images/`](./src/_images/).
2. Link to your image in your page:
   ```
   {% picture _images/example.png alt="A placeholder example description" %}
   ```
3. Take a look at [`src/_images/README.md`](./src/_images/README.md) for more info.

### Advanced Editing

This website is a regular Jekyll website, so you can refer to the [Jekyll documentation](https://jekyllrb.com/docs/) to learn more about the [YAML frontmatter](https://jekyllrb.com/docs/front-matter/) at the top of every page, the [Liquid templating system](https://jekyllrb.com/docs/liquid/) (i.e. the things in `{{ .. }}`, `{% .. %}`, etc.), the [`_layouts` folder](https://jekyllrb.com/docs/layouts/), and more.
