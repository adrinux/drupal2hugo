# History
tl:dr Several people have contributed to this project - do look at the forks on github/commit history

This is a fork of https://github.com/skwashd/drupal2hugo
Which was a fork https://github.com/danapsimer/drupal2hugo
Which was forked from https://bitbucket.org/rickb777/drupal2hugo

# Changes in this fork
1. Renamed drupal62hugo to highlight Drupal 6 compatibility vs Rick Beaton's original which has seen further work since it was forked by @danapsimer


#
Original readme below
#

# Notice
This is a fork of https://bitbucket.org/rickb777/drupal2hugo

There have been a few folks who have forked this repo and that is fine but I just want credit to go where it belongs.  Also, this tool, IMHO, requires customization for most Drupal sites because it does not take into account the additional pieces that modules add to the data model.  Chances are you are using some modules like CCK, for example, and depending on the types of fields you are using, this tool may require some customization.

Think of this tool as a starting point for automating your site migration.  I think it would be pretty futile to try to create a one-size-fits-all migration tool.

# Fork Note
This fork has changes that do two things:

1. Make the drupal DB reading routines work with a Drupal 6 schema.
2. Add the ability to specify an "emvideoField" option that will extract any emvideo type CCK field data an generate a shortcode usage after the Summary like so: 
  ```
  #!
  
  {{< <provider> <videoId> >}}
  ```
3. Make it build nicely with **go get**


# Drupal2Hugo

Drupal2Hugo provides a basic converter to export a Drupal website to text files in [Hugo](http://gohugo.io/) format. 
It will do a lot of the work for you, but some manual intervention will still be needed.

* For each Drupal node, a corresponding text file is written containing the metadata (front matter)
  and the node body content.

* If the Drupal node has a summary, it is retained as a comment after the front matter. It will require
  manual editing to mark the body so that the summary produced by Hugo matches that in Drupal.

* The Drupal markup is assumed to be Markdown or (a subset of) HTML. The body content is transferred verbatim
  and will only work properly if Markdown or HTML have been used.

* All other Drupal content fields are lost. In particular, note that pictures and other multimedia content
  need to be dealt with manually, although the links to them in the body content will be retained.

This is experimental. YMMV.

## Quick start

Idealy, there would already be a selection of pre-build binaries for you, but there aren't. So you need to build
from source, which is quite easy.

Of course, start by installing Go, [setting up paths](http://golang.org/doc/code.html), etc. Then:

    go get github.com/fale/drupal2hugo

There should be a new binary for your computer architecture called `bin/drupal2hugo`.

    Usage of drupal2hugo:
      -V=false: Version information
      -db="": Drupal database name - required
      -driver="mysql": SQL driver
      -pass="": Drupal password (you will be prompted for the password if this is absent)
      -prefix="drp_": Drupal table prefix
      -user="": Drupal user (defaults to be the same as the Drupal database name)
      -v=false: Verbose

Example usage:

    drupal2hugo -db mydrupal -user drupaluser -pass password

A new `content` folder should be produced containing the Markdown files for importing into your Hugo project.

Each page may contain hyperlinks to other pages within its prose. These should preferably be domain-relative links 
(such as "/post/latest-ideas"). If they are Drupal node links like "/node/247", they will be broken links after
export. At the moment, you have to fix these manually.

## Licence

MIT Licence.
