Grails uses the standard Java way of [providing internationalisation](http://grails.org/doc/latest/guide/i18n.html) - using messages.properties and the [g:message taglib](http://grails.org/doc/latest/ref/Tags/message.html) for use in GSP pages. Language detection can be triggered by the browser providing a **locale** value or by providing an additional request parameter called **lang**. E.g. add `?lang=es` to a request URL.

The client webapp (e.g. generic-hub) inherits some internationalisation properties from the **biocache-hubs** plugin, which in turn, inherits further properties from **biocache-service** (via a [webservice call](biocache.ala.org.au/ws/facets/i18n). Custom i18n properties can be added/overrided by including the appropriate messages file. A complete list of the i18n codes (and English) translations can be seen at: 

[http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties](http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties)

## i18n properties files
Grails i18n files are found in:

    /grails-app/i18n

and follow the Java naming convention of `messages_xx_XX.properties`. The ALA is keen to get contributions for non-English translations, either via pull requests to biocache-hubs project or by sending us a patch file or individual properties files.

