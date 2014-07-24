It is possible to have multiple web applications with custom user interface and showing data for a particular Hub using a single backend server.

Basic steps
* Styling your portal
* Create and configure the hub in the Collectory
* Configure the web app to show the records of the new hub

For details about styling see [[Styling the web app|Styling-the-web-app]]

## Create and configure the hub in the Collectory
In the collectory admin interface look for the *View all data hubs* option, here you can add a new DataHub. Edit the name and any other information you required.
In the **Members** section add the Institutions, Collections and Data Resources that belong to the Hub. This is the information that will actually show in the web app.

## Configure the web app
Find the UID of the hub you already created in the Collectory admin interface.
In the web app config file add the property with the appropiate UID.

    biocache.queryContext = "data_hub_uid:dh1"

