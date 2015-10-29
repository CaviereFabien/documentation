Grails uses the standard Java way of [providing internationalisation](http://grails.org/doc/latest/guide/i18n.html) - using messages.properties and the [g:message taglib](http://grails.org/doc/latest/ref/Tags/message.html) for use in GSP pages. Language detection can be triggered by the browser providing a **locale** value or by providing an additional request parameter called **lang**. E.g. add `?lang=es` to a request URL.

The client webapp (e.g. generic-hub) inherits some internationalisation properties from the **biocache-hubs** plugin, which in turn, inherits further properties from **biocache-service** (via a [webservice call](biocache.ala.org.au/ws/facets/i18n). Custom i18n properties can be added/overrided by including the appropriate messages file. A complete list of the i18n codes (and English) translations can be seen at: 

[http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties](http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties)

## i18n properties files
Grails i18n files are found in:

    /grails-app/i18n

and follow the Java naming convention of `messages_xx_XX.properties`. The ALA is keen to get contributions for non-English translations, either via pull requests to biocache-hubs project or by sending us a patch file or individual properties files.

**Note:** If you want to contribute in the i18n project, please visit the page of the project: [https://crowdin.com/project/ala-i18n/](https://crowdin.com/project/ala-i18n/) and request your participation to one of managers.

## How to include language selector in your project:

[http://grails.org/plugin/lang-selector](http://grails.org/plugin/lang-selector).

In this page you have the instructions to do the correctly configuration in your module.
Now, we are going to suppose that you have to install and configurate this plugin in generic-hub.

1) You have to include in the BuildConfig.grrovy in the sections of plugins this code:
runtime ":lang-selector:0.3"

