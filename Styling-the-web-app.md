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