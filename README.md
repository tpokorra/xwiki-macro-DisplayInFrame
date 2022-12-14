# XWiki Macro: Display in Frame

## Purpose

This macro is very similar to the "Display Macro".
The code has been copied and extended, to have a div with class "DisplayInFrame", and with an onclick event to open the displayed page.

## Display Macro

* macro: https://extensions.xwiki.org/xwiki/bin/view/Extension/Display%20Macro
* sources: https://github.com/xwiki/xwiki-platform/blob/master/xwiki-platform-core/xwiki-platform-display/xwiki-platform-display-macro/src/

## Build

Preparation:

    sudo apt-get install maven
    mkdir -p ~/.m2
    vi ~/.m2/settings.xml # insert the content of https://dev.xwiki.org/xwiki/bin/view/Community/Building/#HInstallingMaven

Update for new XWiki release:

    edit the file pom.xml!

This package does not have valid tests yet:

    cd xwiki-macro-DisplayInFrame
    mvn install  -Dmaven.test.skip=true
    # see the result in target/DisplayInFrame-13.10.9.jar

## Deploy

on the server:

    cd ~/tomcat/webapps/ROOT/WEB-INF/lib
    cp /tmp/DisplayInFrame-13.10.9.jar .
    # restart the tomcat
    ~/bin/restart.sh

## CSS & Javascript

As a user with advanced permissions, create a page, and add an object of class StyleSheetExtension.

* Use this extension: on this wiki
* Parse Content: Yes
* Caching Policy: Long
* Content Type: CSS

Code:

```
div.DisplayInFrame {
  display: block;
  border: 1rem solid lightgreen;
  cursor: pointer;
}
```

Also add an object of class JavaScriptExtension.

* Use this extension: on this wiki
* Parse Content: Yes
* Caching Policy: Long

Code:

```
var coll = document.getElementsByClassName("DisplayInFrame");
var i;

for (i = 0; i < coll.length; i++) {
  coll[i].addEventListener("click", function(e) {
    if (e.target.tagName === "DIV") {
      window.open(this.getAttribute('href'));
    }
  });
}
```