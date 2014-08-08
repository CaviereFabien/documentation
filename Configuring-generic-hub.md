It is possible to have multiple web applications with custom user interface and showing data for a particular Hub using a single backend server.

Basic steps
* Styling your portal
* Create and configure the hub in the Collectory
* Configure the web app to show the records of the new hub

For details about styling see [[Styling the web app|Styling-the-web-app]]

## Create and configure the hub in the Collectory
In the collectory admin interface look for the *View all data hubs* option, here you can add a new DataHub. Edit the name and any other information you required.
In the **Members** section add the identifier of the Institutions, Collections and Data Resources that belong to the Hub. This is the information that will actually show in the web app.

## Configure the web app
Find the UID of the hub you already created in the Collectory admin interface.
In the web app config file (grails-app/conf/config.groovy) add the property with the appropiate UID.

    biocache.queryContext = "data_hub_uid:dh1"

## Configure the facet fields 

The config variables starting with `facets.` are responsible for this:

* **`facets.include`** - comma separated list of fields to include (usually only those fields not in the default set as specified by `${biocache.baseUrl}/search/facets`)
* **`facets.exclude`** - comma separated list of fields to exclude. i.e. fields in the default set you don't want to appear
* **`facets.hide`** -  comma separated list of field that would be included in the facet column, that you want to be hidden (i.e. un-ticked in the "customise filters" drop down menu). These fields will be displayed if the user changes the default display settings and chooses to turn them on.

Note, you can also change the **default set** of facets but this is set in the **biocache-service** application, also via config vars (I think). You may also want to change the way facets are **grouped** together (see `${biocache.baseUrl}/search/grouped/facets`).