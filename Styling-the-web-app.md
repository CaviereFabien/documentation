## Overview
This page will cover the process of providing custom styling for the [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) Grails web application. You should have a reasonable level of knowledge of HTML and CSS as well as a basic understanding of [Grails](http://grails.org) and [Bootstrap](http://getbootstrap.com/2.3.2). Helpful links:
* [Grails documentation](http://grails.org/doc/2.3.x/guide/)
* [Bootstrap CSS framework](http://getbootstrap.com/2.3.2/getting-started.html)

The basic steps are:
* Fork the [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) project and rename it to reflect your organisation
* Copy the `generic.gsp` layout file to a new file (e.g. `yourOrg.gsp`)
* Edit `Config.groovy` to use the new layout file
* Edit `yourOrg.gsp` file 
* Create custom CSS (and optional JS) files
* Add custom i18n 

## Fork and rename

* Go to [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) page and click the "Fork" button in the top right corner of the page. Select your repository and click OK. 
* To rename the project, click the "Settings" icon on the right side and edit the project name (e.g. `yourOrg-hub`.
* Clone/checkout the project to your local PC

## Create custom layout file
    cd yourOrg-hub/grails-app/views/layout
    cp genric.gsp yourOrg.gsp

## Edit config file
    cd yourOrg-hub/grails-app/conf
Edit `Config.groovy` in your text editor and modify the line:

    skin.layout = 'generic'
    skin.orgNameLong = 'Generic Data Portal'
to

    skin.layout = 'yourOrg'
    skin.orgNameLong = 'Your Org Name'
You may want to point the app at a local version of `biocache-service` by adding/editing the line:

    biocache.baseUrl=http://yourOrg.org/biocache-service

## Edit layout

The layout file is a **GSP** file, which is similar to the Java **JSP** file format, with some minor differences (see Grails docs). Grails uses the [SiteMesh](https://github.com/sitemesh/sitemesh2) library to provide common HTML component to pages. The generic-hub (~ biocache-hubs plugin) uses the **Bootstrap** CSS framework, so there are some HTML elements that are required to be present for all pages to render properly.
* details to come

## Add custom CSS and JS files

Grails provides a mechanism to manage static resources (CSS, JS and images), called the [Resources plugin](http://grails-plugins.github.io/grails-resources/), and we recommend using this feature. 

Resources are declared in the file `yourOrg-hub/grails-app/conf/ApplicationResources.groovy`, with related files being managed as **modules**. Modules can `dependOn` other modules, which provides a way of making sure dependent files appear before the calling file (e.g. a jQuery plugin will `dependOn` jQuery and thus jQuery will be printed to the page before the plugin). 

The layout file contains a require tag that states which modules are required for all pages that use that particular layout file. E.g.

     <r:require modules="bootstrap2, hubCore" />

To add a new module, simply add a reference to the module:

    <r:require modules="bootstrap2, hubCore, youOrg" />

and then add that module to `ApplicationResources.groovy`:

    yourOrg {
        dependsOn 'bootstrap2', 'hubCore' //
        resource url: [dir:'css', file:'yourOrg.css']
        resource url: [dir:'js', file:'yourOrg.js']
    }

## Custom internationalisation (i18n)

See the separate wiki page: [Internationalization](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Internationalization)

## Examples

There are a number of custom skinned web apps in the [AtlasOfLivingAustralia](https://github.com/AtlasOfLivingAustralia?query=-hub) Github repo that you can refer to for ideas/help with skinning your copy of generic-hub:

* [ala-hub](https://github.com/AtlasOfLivingAustralia/ala-hub)
* [ozcam-hub](https://github.com/AtlasOfLivingAustralia/ozcam-hub)
* [obis-hub](https://github.com/AtlasOfLivingAustralia/obis-hub)
* [avh-hub](https://github.com/AtlasOfLivingAustralia/avh-hub)
* [appd-hub](https://github.com/AtlasOfLivingAustralia/appd-hub)
