---
layout: default
title: "Target 5: Install Shared Packages"
description: "Packages are bundles of source code, tools, and resources that help you to organize and share code"
has-permalinks: true
tutorial:
  id: packages
---

{% capture whats_the_point %}

* Packages are awesome.
* Packages are cool.
* Share your code in packages, with all your friends at school.

{% endcapture %}

{% capture content %}

Now that you're able to create and run a Dart application
and have a basic understanding of DOM programming,
you are ready to leverage code written by other programmers.
Many interesting and useful packages of reusable Dart code
are available at the
<a href="http://pub.dartlang.org/">pub.dartlang.org</a>
repository.

This target shows you how to use `pub`&mdash;a package manager
that comes with Dart&mdash;to
install one of the packages in the repository,
the vector_math package.
You can follow these same steps to install any package hosted at
<a href="http://pub.dartlang.org/">pub.dartlang.org</a>;
just change the package name when you get to that step.
This target also describes some of the resources you can expect to find
in a well-built package.

* [About the pubspec.yaml file](#about-pubspec)
* [Name the package dependencies](#name-dependencies)
* [Install the package dependencies](#install-dependencies)
* [What did you get (and not get)?](#about-packages)
* [Import libraries from a package](#use-package)

##About the pubspec.yaml file {#about-pubspec}

To use an external package,
your application must itself be a package.
Any application with a valid pubspec.yaml file in its top-level directory
is a package and can therefore use external packages.
When you create an application using Dart Editor,
Dart Editor automatically creates a `pubspec.yaml` file.

Start Dart Editor and create a new application with the name `vector_victor`.
Double click pubspec.yaml to view its contents.

![Dart Editor with pubspec.yaml file](images/victor-files.png)

The pubspec.yaml file contains the package specification written in YAML
(visit <a href="http://pub.dartlang.org/doc/pubspec.html">Pubspec Format</a>
for in-depth coverage).
Dart Editor provides a user interface for editing the pubspec.yaml file
so that you don't have to worry about the YAML format.
Or you can click the **Source** tab at the bottom of the Editor pane
to edit the YAML code directly.
Below is the pubspec.yaml file that was
created for the vector_victor application.

![The default pubspec.yaml file specifies name and description](images/pubspec.png)

The package name is required.
All web applications are dependent on the browser package
provided at pub.dartlang.org.

{% comment %}
##...Or put an existing application into a package {#old-app-in-pkg}

If you already have an application
and want it to use an external package,
simply create a pubspec.yaml file in the application's top-level directory.
Your pubspec.yaml file must at least specify the package name.

![The smallest possible pubspec.yaml](images/minimalpubspec.png)

<aside class="alert">
<strong>Tip:</strong> If you are using
Dart Editor to create the pubspec.yaml file,
you might get an error message
when you first create the empty pubspec.yaml file.
This is because Dart Editor runs pub automatically and
is trying to resolve the package specification file,
which at first has nothing in it.
Ignore the message,
add the required name field,
and save the pubspec.yaml file.
</aside>
{% endcomment %}

##Name the package dependencies {#name-dependencies}

To use an external library package,
you need to add the package to your
application's list of _dependencies_
in the pubspec.yaml file.
Each item in the dependencies list
specifies the name, and sometimes the version,
of a package that your application uses.

Let's make the vector_victor application have a dependency 
on the vector_math package,
which is available at pub.dartlang.org.
Click the **Add** button in Dart Editor.

![Click the add button to add a package dependency](images/dependencies-ui.png)

Enter the name of the package in the popup window.

![Enter the package name](images/add-dependency-window.png)

Dart Editor adds the package name to the list.

![The application is now dependent on vector_math](images/after-add.png)

Notice the **Version** field.
`any` means that this application can use
any version of the vector_math package.
You could instead specify a particular version of the package.
When versioning becomes important to your project,
check out
<a href="http://pub.dartlang.org/doc/versioning.html">
Pub's Versioning Philosophy
</a>.

Here's the new pubspec.yaml file:

![Pubspec.yaml file with vector_math dependency](images/pubspec-vectormath.png)

<a href="http://pub.dartlang.org/">pub.dartlang.org</a>
is the primary public repository for Dart packages.
`pub` automatically checks that
website when resolving package dependencies.
To use one of the packages from that site,
you can specify it by its simple name,
as we have done here.

##Install the package dependencies {#install-dependencies}

In Dart Editor, save pubspec.yaml with **File > Save**.
When you save the file,
Dart Editor automatically runs
<a href="http://pub.dartlang.org/doc/pub-install.html">pub install</a>,
which recursively installs the Dart libraries
from the packages in the dependencies list.
You can also select **Pub Install** from the **Tools** menu in Dart Editor.

Pub puts the libraries in a directory called packages
under the application's top-level directory.
Click the wee arrow to expand the packages directory.
There you will find the vector_math directory,
which links to the Dart libraries from the vector_math package.

![Pub Install finds and installs required packages](images/run-pub-install.png)

In addition,
you will notice the unittest directory;
unittest is another package in the repository.
vector_math depends on unittest
(unittest is listed in vector_math's dependencies list)
so pub installs it as well.
Pub install works recursively and installs
all of the required packages
of your application and its dependencies.

Pub install also creates a file called pubspec.lock,
which identifies the specific versions of the packages that were installed.
This helps to provide a stable development environment.
Later you can modify the version constraints and use `pub update`
to update to new versions as needed.

##What did you get (and not get)? {#about-packages}

Besides the Dart libraries,
the vector_math package has other resources that might be useful to you
that do not get installed into your application directory.
Let's take a step back for a moment to look at what
you got and where it came from.

To see the contents of the vector_math package,
visit the
<a href="https://github.com/johnmccutchan/DartVectorMath" target="_blank">
Dart vector math repository
</a>
at GitHub.
Although many files and directories are in the repository,
only one, `lib`, was installed when you ran pub install.

<div>
  <hr>
  <div class="row">
    <div class="span2">
    <img src="images/libraries-folder.png"
         alt="Dart libraries directory"/>
    </div>
    <div class="span7">
      <em>Dart libraries</em>:
      The lib directory contains one or more Dart libraries,
      which can be imported into your Dart programs.
    </div>
  </div>
  <hr>
  <div class="row">
    <div class="span2">
    <img src="images/housekeeping-files.png"
         alt="Housekeeping files"/>
    </div>
    <div class="span7">
      <em>Housekeeping files</em>:
      When using a package written by someone else,
      the README file is a good place to start.
      It should contain important information about the package,
      such as its intent, contents, samples, and instructions.
      The LICENSE file provides copyright and rules-of-use information.
      These files can be found at the package repository.
      They are not installed when you install a package.
    </div>
  </div>
  <hr>
  <div class="row">
    <div class="span2">
    <img src="images/other-folders.png"
         alt="Document, scripts, tests, and other resources"/>
    </div>
    <div class="span7">
      <em>Other resources</em>:
      Along with Dart libraries,
      a package might also contain other resources 
      such as example code, tests, scripts, and documentation.
      If a package contains these resources,
      they should be in the directories as specified in the pub
<a href="http://pub.dartlang.org/doc/package-layout.html">conventions</a>.
    </div>
  </div>
  <hr>
</div>

##Import libraries from a package {#use-package}

Open the vector_math directory by clicking the little arrow.

![Finally, the vector_math library files](images/the-vectormath-library.png)

The directory contains two Dart files,
each of which defines a different library.
As with the SDK libraries,
use the import directive to use code from an installed library.
The Dart SDK libraries are built-in and
are identified with the special dart: prefix.
For external libraries installed by pub,
use the `package:` prefix.

{% prettify dart %}
import 'package:vector_math/vector_math_browser.dart';
{% endprettify %}

Note that you specify the filename, not the library name.

<div class="row">
  <div class="span3">
  <a href="/docs/tutorials/remove-elements/"><i class="icon-chevron-left"> </i> Remove DOM Elements</a>
  </div>
  <div class="span3">
<a href="http://code.google.com/p/dart/issues/entry?template=Tutorial%20feedback"
 target="_blank">
<i class="icon-comment"> </i>
Send feedback
</a>
  </div>
  <div class="span3">
  <a href="/docs/tutorials/web-ui/" class="pull-right">Get Started with Web UI <i class="icon-chevron-right"> </i> </a>
  </div>
</div>

{% endcapture %}

{% include tutorial.html %}
