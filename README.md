# pandorabots.github.io

Welcome to the Pandorabots documentation site! Here you'll find instructions on
how to update and maintain the site.

## Technology colophon

- [Jekyll](https://jekyllrb.com/) - static site generator
- [Github pages](https://pages.github.com/) - host w/automatic build
- [Bootstrap](http://getbootstrap.com/) - frontend framework
- [Font Awesome](https://fortawesome.github.io/Font-Awesome/) - icons
- [Google Fonts](https://www.google.com/fonts) - Open Sans and Comfortaa fonts

## Local setup

From the command line:

```
$ git clone https://github.com/pandorabots/pandorabots.github.io.git
$ cd pandorabots.github.io
$ jekyll serve
```

This will open the Jekyll development server at
[localhost:4000](http://localhost:4000). It will also watch your files, so that
you don't have to rebuild/restart every time you make a change.

## Adding content

The site's content is driven by Jekyll collections, which allow you to group
similar content together under a common namespace. The concept is similar to the
posts that make up a blog, except that we aren't so concerned with displaying
our content ordered by date published.

Jekyll collections are stored in folders that have the name of the collection,
plus an underscore prefix. Inside, create a markdown file (.md) for your new
piece of content. So for a new "article", go into the _articles directory and
create a file called "my-article.md".

This will create a new page accessible at
http://pandorabots.github.io/articles/my-article (the title of the file
determines the URL).

Each content file needs to have "Front matter" section to define some properties
for the content. This section is delimited by three hyphens before and after,
and should contain at least the layout and title properties for the content:


Example (_articles/my-article.md)

```
---
layout: default
title: My Article
___

Here is my article!
```

The title will appear in the sidebar index, and the layout
will determine how the header, footer, sidebar etc. are laid out. **Use
"default" as the layout for all content except for AIML references for which you
should use the "aiml" layout.**

> You can also use HTML in content files. Just make sure to save the file as
**.html** instead of **.md**.

## Adding a new collection

Open up _config.yml to see your Jekyll site configuration. At the bottom is the configuration for collections - simply follow the format
to create a new collection, and add a folder with the name of your
collection prefixed with an underscore.

See _includes/sidebar.html for examples of how to add a collection to the navigation.

Finally, you'll want to copy-paste one of the click handlers in js/app.js to handle the collapse of your
new collection in the sidebar. Go to the bottom, duplicate one of the click handlers, and replace all instances of the old
collection's name with your new collection.

## CSS

The site's styles are 99% Bootstrap with some customizations made in css/style.css.

## Deployment

Deployment is handled by Github pages. You just have to push your code
to master, and Github will build the Jekyll site for you!
