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

In this page you have the instructions to do the correctly configuration of lang-selector plugin in your module.
Now, we are going to suppose that you want to install and configurate this plugin in generic-hub.

1) You have to include in the section of plugins of BuildConfig.grrovy this code:

    runtime ":lang-selector:0.3"

 2) After this, you can add the tag to your gsp. For example, you can include it in the header sections of /grails-app/views/laouts/generic.gsp to see the lang selector in all views of your generic-hub module. 

    <ul class="nav pull-right">
       <li class="dropdown">
           <a class="dropdown-toggle" data-toggle="dropdown" href="#">Language<b class="caret"></b></a>
           <ul class="dropdown-menu">
               <li><langs:selector langs="ca"/></li>
               <li><langs:selector langs="en"/></li>
               <li><langs:selector langs="es"/></li>
           </ul>
       </li>
    </ul>

3) Optionally you can add this property to the /grails-app/conf/Config.groovy to tell the plugin which flag display for the language:

    com.mfelix.grails.plugins.langSelector.lang.flags = ["es":"es",
                                                     "en":"gb",
                                                     "fr":"fr",
                                                     "da":"dk",
                                                     "de":"de",
                                                     "it":"it",
                                                     "ja":"jp",
                                                     "nl":"nl",
                                                     "ru":"ru",
                                                     "th":"th",
                                                     "zh":"cn",
                                                     "pt":"pt",
                                                     "ca":"catalonia"]
   
Also, you can do this in the collectory module.

Now we are going to suppose that you don't want to have a flags, maybe for more accesibility or for other reasons. In this case, you have to modify the code of this plugin. To do that you have to download the plugin, calling it locally in the /grails-app/BuildConfig.groovy, and you have to modify /lang-selector-0.3/grails-app/views/langSelector/_selector.gsp:

BuildConfig.groovy:

    grails.plugin.location.'lang-selector' = "plugins/lang-selector-0.3"


_selector.gsp:

    <div id="lang_selector">
    <span style="color:white"><g:message code="1" default="|"/></span>
	<g:each in="${flags.keySet().sort() }" var="lang">
		<a href="${ uri + lang }" title="${message(code:'tittle.lang_link')}">
			<span class="lang_flag ${ lang==selected.toString()? selected_class : not_selected_class }" style="margin-left: 14px;">
			<g:if test="${flags[lang] == 'catalonia'}">
			        <g:message code="1" default="Català"/>
			</g:if>
			<g:if test="${flags[lang] == 'gb'}">
			        <g:message code="1" default="English"/>
			</g:if>

			<g:if test="${flags[lang] == 'es'}">
			        <g:message code="1" default="Español"/>
			</g:if>
			<%--<img alt="" src="${resource(plugin:'langSelector',dir:'images/flags/png',file:flags[lang]+'.png') }" border="0">--%>
			</span>
		</a>
		<span style="color:white"><g:message code="1" default="|"/></span>
	</g:each>
</div>


