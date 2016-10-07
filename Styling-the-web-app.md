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
* Move the file that you want to change from the plugin to your grails-app folder

## Create custom layout file
    cd yourOrg-hub/grails-app/views/layout
    cp genric.gsp yourOrg.gsp

## Edit config file
There are two mechanisms for configuring the web app:
* external config file (properties file) - default location: `/data/appName/conf/appName-config.properties`
* internal Grails config file at: `/grails-app/conf/Config.groovy`

External config values will take precedence over those in Config.groovy. The ala-demo uses the external config file and this is the recommended way of setting config values.

Change the following vars (in either external or internal file):

    skin.layout = 'generic'
    skin.orgNameLong = 'Generic Data Portal'
to

    skin.layout = 'yourOrg'
    skin.orgNameLong = 'Your Org Name'

You may want to point the app at a local version of `biocache-service` by adding/editing the line:

    biocache.baseUrl = "http://yourOrg.org/biocache-service"


**Note:** if using external properties file, then omit the quote characters around string values.

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

##Grails tag##

Format : `<g:tag_name option=”value_of_option” />`

The documentation of a tag name : http://docs.grails.org/latest/ref/Tags/tag_name.html

Here is a non-exhaustive list of Grails tags with explanations : 
***
>message 

>Use for the internationalization, the code properties will be in the message.properties file : 

>http://docs.grails.org/latest/ref/Tags/message.html
***
>link

>Anchor that creates a HTML link. More information on this page :

>http://docs.grails.org/latest/ref/Tags/link.html
***
>if/else

>The logical if/else tag :

>http://docs.grails.org/latest/ref/Tags/if.html
>http://docs.grails.org/latest/ref/Tags/else.html
***
>actionSubmitImage

>Generates a submit action with input type =”image” :

>http://docs.grails.org/latest/ref/Tags/actionSubmitImage.html
***
>actionSubmit

>Anchor that will create a button with a submit action. 
>In the action part, you will be able to change the action of the button (eg: delete, sumbit, etc.) and you can have several submit actions in one form :

>http://docs.grails.org/latest/ref/Tags/actionSubmit.html
***
>select

>Generates a select field in a form :

>http://docs.grails.org/latest/ref/Tags/select.html
***
>checkbox

>Creates a checkbox field in a form :

>http://docs.grails.org/latest/ref/Tags/checkBox.html
***
>hiddenField

>Adds a hidden field on your form :

>http://docs.grails.org/latest/ref/Tags/hiddenField.html
***
>textArea

>Creates and fills a text area field on a form :

>http://docs.grails.org/latest/ref/Tags/textField.html
***
>form

>Anchor that creates and manages a form that submits to a controller :

>http://docs.grails.org/latest/ref/Tags/form.html 
***
>textField

>Creates and fills a text field of a form : 

>http://docs.grails.org/latest/ref/Tags/textField.html
***

##Bootstrap 3 : tips##

 Add the module bootstrap3 in your `applicationRessource.groovy` file using these commands : 

    bootstrap3 {
		resource url: [dir: 'bootstrap3/js', file: 'bootstrap.js', disposition: 'head']
		resource url: [dir: 'bootstrap3/css', file: 'bootstrap.css', attrs: [media: 'screen, projection, print']]
		resource url: [dir: 'bootstrap3/css', file: 'bootstrap-theme.css', attrs: [media: 'screen, projection, print']]
	}


 Download Bootstrap3 : `http://getbootstrap.com/getting-started/#download`

 Add this folder in the `web-app` folder 

 Add bootstrap3 to your `require module` tag in your layout file

 You need to upgrade JQuery 1.8 to JQuery 1.11


 **Be careful : Some functions are depreciated.** 

 **For example : .live() need to be change to the .on()**


 On the Config file, you need to add the /bootstrap3/ folder to have access to image

        grails.resources.adhoc.patterns = ['/img/**', '/images/*', '/data/*', '/css/*', '/js/**', '/plugins/**', '/bootstrap3/css/**', '/bootstrap3/js/**', '/bootstrap3/fonts/**']

        grails.resources.adhoc.includes = ['/img/**', '/images/*', '/data/*', '/css/*', '/js/**', '/plugins/**', '/bootstrap3/css/**', '/bootstrap3/js/**', '/bootstrap3/fonts/**']


## Custom internationalisation (i18n)

See the separate wiki page: [[Internationalization (i18n)|Internationalization-(i18n)]]

## Examples

There are a number of custom skinned web apps in the [AtlasOfLivingAustralia](https://github.com/AtlasOfLivingAustralia?query=-hub) Github repo that you can refer to for ideas/help with skinning your copy of generic-hub:

* [ala-hub](https://github.com/AtlasOfLivingAustralia/ala-hub)
* [ozcam-hub](https://github.com/AtlasOfLivingAustralia/ozcam-hub)
* [obis-hub](https://github.com/AtlasOfLivingAustralia/obis-hub)
* [avh-hub](https://github.com/AtlasOfLivingAustralia/avh-hub)
* [appd-hub](https://github.com/AtlasOfLivingAustralia/appd-hub)