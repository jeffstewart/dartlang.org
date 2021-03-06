# Dart Website (dartlang.org)

[![Build Status](https://drone.io/github.com/dart-lang/dartlang.org/status.png)](https://drone.io/github.com/dart-lang/dartlang.org/latest)

The www.dartlang.org site. Built with Jekyll (https://github.com/mojombo/jekyll)
and hosted on App Engine.

File issues and bugs here: http://dartbug.com/new

Fork and submit patches here: https://github.com/dart-lang/dartlang.org

## Orientation

<dl>
  <dt> ./src </dt>
  <dd> Contains all the working files. </dd>

  <dt> ./src/appengine </dt>
  <dd> Contains app engine configuration files. </dd>

  <dt> ./src/site </dt>
  <dd> Documents, HTML files, images, etc.
  You will work out of here normally. </dd>

  <dt> ./build </dt>
  <dd> Generated by Jekyll, to be deployed to server.
  This directory is transient, can be deleted. </dd>
</dl>

## Configuring your system

* Ensure you have Ruby 1.9.3 or greater.
  * You can use **brew** (if you're on a Mac).
* Ensure you have Python 2.7.
  * On a Mac? You might want the binary install of Python at http://www.python.org/download/releases/2.7.3/
* Open a new Terminal.
* Run `sudo gem install bundler`.
* Run `sudo bundle install` from the root of your dartlang project.
* Download and install the App Engine launcher: https://developers.google.com/appengine/downloads
  * Tell App Engine to use Python 2.7 if it's not.
    * It will say, in the log "you're using 2.6".
    * On a Mac?
      * Go to Preferences, and enter the direct path to the Python 2.7 binary,
      which you downloaded from http://www.python.org/download/releases/2.7.3/.
        * The full path is `/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7`.

### Tips for Windows

* Install Python and Ruby using Windows installers.
* Install ruby dev kit for Windows.
* Run `gem install bundler`.
* Run `bundle install` from the root of your dartlang project.


## Development

* Make sure you are in the root of this project.
* Run the server: `make server`
* Your web browser opens to http://localhost:8080.
  * You may need to reload once.
* Edit, create docs as normal.
* If you're making changes to the Sass (SCSS) files, you can regenerate the CSS
  by running `make compass` from the root of the repository on the command line.

### Windows development tips

You probably won't have **make** available on the command line by default.

* To just get up and running, run `jekyll` from the `src/site` folder.  
* This starts up the Jekyll webserver and generates into build/static.
* If Jekyll does not generate output, you need to type `chcp 65001` at the 
  command prompt to change the code page to UTF-8. (Jekyll fails silently 
  if this is not done.)
* To **clean**, simply delete the contents of build/static and restart `jekyll`.


## Deploying the site

* Run `make clean && make deploy`.
  * This builds the site and places everything into build/.
  * This command also uses the current branch for the app engine version name.
  * This command will then deploy the site.
* You will probably need to grab a unique password from your Google Account settings.
  * Save this into the App Engine Launcher during the first deployment.

## Regenerating Dartisans playlists

Did you just run a Dartisans? Good for you! Here's what you need to do:

1. Update the description to be present tense (instead of future),
   and remove the link to the moderator page.
1. Ensure the episode is added to the Dartisans playlist, owned by
   Google Developers channel.
1. Sort the playlist by date.
1. Ensure your episode explicitly sets a Recorded On date.
1. Format your episode's title like this: "Dartisans ep. XX: Subtitle Here"
1. Pick a great image thumbnail. Don't use the static Dart logo.
1. Now run `make dartisansplaylist`
1. Test it, commit, and go!

## Updating the book

The files under docs/dart-up-and-running/contents are autogenerated
from the DocBook files for _Dart: Up and Running._
Here's how to update these files.

First, prepare:

* Make sure dart (the Dart VM) is in your PATH.

    > which dart
    /Users/me/dart/dart-sdk/bin/dart

* Make sure xsltproc is in your PATH.

    > which xsltproc
    /usr/bin/xsltproc

* Find a copy of the latest .xml files that make up dart-up-and-running.
  For example:

    > ls ~/Spot/dartbook/GIT-HUB/dart-up-and-running-book
    LICENSE   bookinfo.xml  ch02.xml  ch05.xml  figs
    README.md ch00.xml  ch03.xml  code    foreword.xml
    book.xml  ch01.xml  ch04.xml  colo.xml

Now you're ready. From the top directory of this repo,
run the following command, specifying the directory that contains ch*.xml:

    make book BOOK_XML_DIR=<dir-with-xml-files>

Example:

    make book BOOK_XML_DIR=~/Spot/dartbook/GIT-HUB/dart-up-and-running-book

Wait 4-5 minutes for results.

*Very* carefully check the diffs, paying special attention to the headers
at the top. Rerun the `make book` command if you aren't sure of the
changes.

(Yes, different runs of `make book` can have different results, even
when the .xml files haven't changed. The problem I've noticed has been
misnaming files or skipping them in the navigation. Reported as
dartbug.com/8128.)
