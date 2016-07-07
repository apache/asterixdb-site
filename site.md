---
title: Editing this website
---

<!-- Major credit to the Apache Flink guys for writing a great doc in a similar vein for their website
that happens to use more or less the same tooling as AsterixDB's. Much of this doc is based on it. -->

* TOC
{:toc}

---

## Prerequisites

### Jekyll.
This website is written using a static website generator called [Jekyll](https://github.com/jekyll/jekyll). To work with editing this website you will need to install it.
In short, Jekyll uses a combination of templated HTML files and Markdown to compile the final site.
Generally, the content itself lies within the Markdown files, and the HTML is for layout.
A full tutorial about how to use Jekyll is out of the scope of this document, but, for our purposes, only Markdown will be edited.

### Checking out the website sources

The website is managed using `git`. Clone the site as usual

    ➤ git clone -b asf-site https://git-wip-us.apache.org/repos/asf/asterixdb-site.git

and `cd` into the clone

    ➤ cd asterixdb-site

You will notice lots of Markdown files and HTML templates in the repository root. The compiled content of the website itself is served from the `content/` folder in this repository. That is to say, that the actual content of the website itself, as well as its sources are stored in the same repository. Additionally, the main branch on this repository is `asf-site` and not `master`

Gerrit is used to submit code reviews for the website just as it is with the main codebase. The main difference the site is not strictly subject to code reviews.

Then, you likely will want to check out to make your own topic branch as to not work directly on the "live" branch, like so:

    ➤ git checkout -b YOU/site

And perform the git-gerrit init on this branch

    ➤ git gerrit init -u ssh://YOU@asterix-gerrit.ics.uci.edu:29418/ -p incubator-asterixdb-site


## Making a change to the site

The general overview is as follows:

- Make edits and check the output of `jekyll build`
- Commit the change and propose it for review
- Either wait for a review, or submit the change

### Editing and viewing the change.

For whichever section of the site you want to edit, go ahead and do so with the text editor of your choice. Then, to see what your change looks like, in the repository root, execute:

    ➤ jekyll serve --watch

This sets up a small integrated web server and compiles the site dynamically as it is edited. Once you are satisfied with how the site looks, go ahead and commit your changes with git.

Once you have made your commit, push it to Gerrit for review:

    ➤ git gerrit submit -b asf-site

For longer edits you might need to update your local `asf-site` mirror, and then merge that onto your working branch. This will prevent your branch from falling too far out of date, and ensure that your code review proposals will merge successfully with `master`. Similar to the way this is done for code changes you can use

    ➤ git gerrit update -b asf-site

to do this.

### Submitting the change to the live site

When the submitted review is committed in Gerrit, pull it and overwrite your current asf-site branch:

    ➤ git fetch gerrit

Then, push the exact commit from the Gerrit web interface to the ASF git repository. Do this with care! ASF git doesn't allow hard resets on branches, so whatever you push here is final.

    ➤ git push origin (SHA1 of submitted commit):asf-site

## Troubleshooting

If jekyll produces an error message like this one:

    ➤ jekyll serve --watch
    Configuration file: /.../asterixdb-site/_config.yml
    You are missing a library required for syntax highlighting. Please run:
    $ [sudo] gem install pygments
    jekyll 3.1.2 | Error:  uninitialized constant Kramdown::Converter::PygmentsHtml::FatalException

  this might fix it:

    ➤ sudo gem install pygments.rb

