# XWiki Macro: Display in Frame

## Purpose

This macro is very similar to the "Display Macro".
The code has been copied and extended, to have a span with class "DisplayInFrame", and with an onclick event to open the displayed page.

## Display Macro

* macro: https://extensions.xwiki.org/xwiki/bin/view/Extension/Display%20Macro
* sources: https://github.com/xwiki/xwiki-platform/blob/master/xwiki-platform-core/xwiki-platform-display/xwiki-platform-display-macro/src/

## Build

Preparation:

   sudo apt-get install maven
   mkdir -p ~/.m2
   vi ~/.m2/settings.xml # insert the content of https://dev.xwiki.org/xwiki/bin/view/Community/Building/#HInstallingMaven


This package does not have valid tests yet:

    cd xwiki-macro-DisplayInFrame
    mvn install  -Dmaven.test.skip=true

## Deploy

on the server:

    cd ~/tomcat/webapps/ROOT/WEB-INF/lib
    cp /tmp/DisplayInFrame-13.10.9.jar .
    # restart the tomcat
    ~/bin/restart.sh

## CSS

As a user with advanced permissions, create a page, and add an object of class StyleSheetExtension.

* Use this extension: on this wiki
* Parse Content: Yes
* Caching Policy: Long
* Content Type: CSS

Code:

```
span.DisplayInFrame {
  display: block;
  border: 1rem solid lightgreen;
  cursor: pointer;
}
```