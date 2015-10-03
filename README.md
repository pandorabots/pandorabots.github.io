# pandorabots.github.io

Welcome to pb-docs, the documentation site for the Pandorabots platform.

pb-docs uses [Jekyll](http://jekyllrb.com)'s wonderful collections feature to
provide markdown based documentation that anyone can update easily.

We're also using [Bootstrap](http://getbootstrap.com) and jQuery to provide
styles and some simple animations.

## Creating new documents

If you are adding content to a collection, simply add a new Markdown (`.md`)
file in one of the collections directories. Make sure to give your new file an
obvious name:

- `_aiml/`
- `_tutorials/`
- `_integrations/`
- `_posts/` (not currently in use)

### Front matter

Jekyll relies of "front matter" sections in your Markdown and HTML files to
determine which layout to use for which document, as well as determining certain
variables local to the page such as title. For example, an AIML reference document
for the category element might have the following front matter:

```
---
layout: aiml
title: category
---
```
When in doubt, just copy an already existing document in the same collection. Here
is a full example of an AIML reference document (`_aiml/category.md`):

```
---
layout: aiml
title: category
---

### &lt;category&gt;

The *category element* delimits a base unit of knowledge in an AIML-based chatbot. In a very broad sense, a single category accepts an input, and returns an output.

All AIML elements (with the exception of the AIML root element and the topic element) must be contained within a category block.

**Usage**

    <category>
    <pattern>HI</pattern>
    <template>Hello world!</template>
    </category>
```

When Jekyll runs, this document will be added to the `_aiml` collection, and a
new HTML will be compiled and saved in the `_site/` directory. You should now see
your item in the sidebar, and be able to visit its page.

### URLs

Each collection has its own path. Each item in the collection is found under the
collection path, by the title supplied in the document's front matter. The URL for
our above document `_aiml/category.md` would be `https://pandorabots.github.io/aiml/category`

## Creating new collections

You can create a new collection by:

1) Add a folder to your root directory with the name of the collection prepended
by an underscore (e.g. `_aiml` or `_tutorials`).  

2) Modify `_config.yml` to configure the folder as a collection:

```
collections:
  ...
  myCollection:
    output: true
    permalink: /myCollection/:path/
```

3) Add your collection to the sidebar (optional, do this in `_includes/sidebar.html`)

```
<div class="site-sidebar">

  ...

  <h4 id="myCollectionCollapseIcon" style="cursor: pointer;">My Collection <i class="fa fa-angle-right"></i></h4>
  <div class="collapse" id="myCollectionCollapse">
    <ul class="list-unstyled">
      {% for element in site.myCollection %}
      <li><a href="{{ site.baseurl }}{{ element.url }}">{{ element.title }}</a></li>
      {% endfor %}
    </ul>
  </div>

  ...

</div>
```

4) Generate a custom JS file for your collection (`js/myCollection.js`):

```
$('#myCollectionCollapseIcon')
  .find('i')
  .removeClass('fa-angle-right')
  .addClass('fa-angle-down');
$('#myCollection').addClass('in');
```

5) Finally, create a new layout (copy another one with the name of your collection),
and change the custom script URL to the one you just created:

```

```


## Deployment

This couldn't be easier. Just commit your changes and push to master.

```
$ git add .
$ git commit -m 'I made a change'
$ git push origin master
```

## File structure

Jekyll generates static sites from Markdown files. When Jekyll runs, it compiles
all of your Markdown files and layout code into HTML files, which can then be
served without any additional interaction with the server. You should familiarize
yourself with the file structure of pb-docs:

- `_aiml/` - contains all AIML element reference documents
- `_includes/` - contains all common HTML components (head, header, sidebar, footer)
- `_integrations/` - integrations documents
- `_layouts/` - layouts for various page types
- `_posts/` - blog posts (not currently in use)
- `_sass/` - only let the designer touch this
- `_site/` - this is where compiled files go (don't touch this)
- `_tutorials/` - tutorials documents
- `css/` - target for compiled SASS (don't touch this)
- `js/` - Javascripts (mostly handles menu collapse)
- `vendor/` - Keep vendor libs here (we don't need bower)
- `.gitignore` - files to be ignored by git
- `_config.yml` - Jekyll site configuration file
- `feed.xml` - XML feed configuration
- `index.html` - home page HTML
- `README.md` - documentation

## Layouts

## Third-party libraries
