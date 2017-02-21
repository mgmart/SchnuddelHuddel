+++
date = "2017-02-19T16:55:28+01:00"
title = "Switching from Wordpress to Hugo"
Tags = ["hugo","wordpress"]
description = "How and why I switched to hugo"
categories = ["tools"]
banner = "images/hugo-logo.png"
draft = false
url = "/switching-from-wordpress-to-hugo/"
+++

I used Wordpress for about 10 years. In those ten years I produced 72
posts. Most of these posts were
about [audaxes](https://en.wikipedia.org/wiki/Randonneuring) or travels I
made. During the travels I made my posts with the Wordpress iOS client
application. Which was sometimes a hassle because pictures weren't uploaded
reliably and I ended up with missing pictures in my posts.

Also the amount of vulnerabilities either in php or in Wordpress
increased. Those weren't patched as frequently as I' liked. And furthermore the
load of attacks specially on Wordpress components increased over the time.

This post is not a cookbook, there are enough out there for the different parts
needed. It's more a report with links to the pages which helped me during the
process.

# Why Hugo

There are many static site generators out there. The thing most of the
generators have in common is that they are based on some frameworks and you end
up installing runtimes and frameworks before you can begin to work with the
generator itself.

[Hugo](http://gohugo.io) is a single executable and works out of the box. There
are also some themes available to give you a jump start.

# The steps

After I'd decided to go away from Wordpress I did some research on the options.
During this research I became aware that I could also migrate the existing
comments over to static system by using [disqus](https://disqus.com). This is
task I completed a few days before the migration.

## Using disqus for comments

I did migrate the existing comments to disqus by using
the [Wordpress plugin](https://wordpress.org/plugins/disqus-comment-system/)
which is provided by disqus itself. Within the plugin there is enough
information provided to get the migration step quickly done.

After the migration and with the plugin loaded, Wordpress comments are
fully substituted by disqus. From that moment one could switch to a static site
generator at any time.

## Convert the existing posts

To convert posts and pages over to hugo, there exists also
a [plugin](https://github.com/SchumacherFM/wordpress-to-hugo-exporter). I tried
it out but got no sufficient result. But hugo itself has an jekyll importer
built in. So I went with
a [plugin](https://wordpress.org/plugins/jekyll-exporter/) which exports
everything necessary to jekyll and imported the jekyll files to hugo.

The result worked out of the box. Only some images were nested in ugly html
which I converted to markdown by
some [emacs](https://www.gnu.org/software/emacs/) keyboard macros which were
made in seconds. I kept the images in their directory structure which was
provided by Wordpress. Although for new posts I took the hugo approach and put
the images into the static directory.

## Stage everything locally

With my content ready in markdown I was ready to built up my site locally. Hugo
has a server built in which allows to see instantly any changes made to content
or configuration. I picked the
nice [Icarus theme](http://themes.gohugo.io/theme/hugo-icarus/) to work with. It has
disqus support, categories and it matches somehow the theme I used with
Wordpress.

The only caveat here is, be careful with the use of disqus locally. I ended up
with pages located at `http://localhost:1313` cluttering my disqus
dashboard. The hugo documentation helps with this. In the section [Conditional
Loading of Disqus Comments](https://gohugo.io/extras/comments/) it is explained
how to change the responsible partial.

## Bring it to the server

After everything was running fine locally, the next step was to bring it to the
server. My Wordpress installation was running on Apache. This Apache server does
serve some other things like my [trac](https://trac.edgewall.org) installation
and my [WebDAV](http://www.webdav.org) so I went with this and applied only the
needed configuration and stripped all the php things because they were not
needed anymore.

### Commit only source files

Simply copying the generated files to server would not have suited my workflow
because in this case I would not have been able to post from an iOS device. An
better approach for me was to store only the source files in a git repository
and to build everything on the server itself. Ideally after each push to the
server. This can easily be done by making use
of [git-hooks](https://git-scm.com/book/gr/v2/Customizing-Git-Git-Hooks). In
this case a receive-hook for which I found a great example
from [Bradley Falzon](https://bradleyf.id.au/nix/git-push-deploy-hugo/).


## Posting from iOS

Having this all setup the only things which are needed to create new posts or
edit existing posts are: an editor and a git client. Those are also available
for iOS, of course. I tried out [Git2Go](http://git2go.com) but it worked not
reliable for me and [Working Copy](https://workingcopyapp.com), which is great
for me. As an editor I had already [Byword](https://bywordapp.com) installed but
as I learned that [Editorial](http://omz-software.com/editorial/) has support
for Working Copy I switched over.
