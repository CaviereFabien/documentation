# Upload data

There are 4 means to upload data on your portal ; each one of them are explained on this page.

## Create a data resource on the ALA site

Go to your admin interface by the following URL: <http://URL_of-you-portal/collectory/manage/list>.

At the very bottom of the page, two features are available : 1) [Add all GBIF resource](http://10.1.1.2/collectory/manage/gbifLoadCountry) for a country; 2) [Upload GBIF file](http://10.1.1.2/collectory/dataResource/gbifUpload).

1. Click 'upload' GBIF File;
1. Find the file in your desktop and click "upload";
1. The result being like this page:

![Result of uploading](/AtlasOfLivingAustralia/documentation/wiki/img/result_of_uploading.png)

Remember the UID: dr0 in the first section. This UID will be what we use for the next indexing and processing step.

Run data indexing and processing against the newly created data resource

This is done through the command-line interface. Now navigate to ala-install/vagrant/ubuntu and

    $ vagrant ssh

Then, depending on whether the data directory is owned by root, continue the rest as the root user:

    $ sudo su

Start the biocache console:

    $ biocache

Load, Sample, Process, Index the dr0 resource we have just uploaded:

    biocache> ingest -dr dr0

At this point, visit http://10.1.1.2/collectory/public/show/dr0 and you can see that the ALA site is aware of those records in the uploaded archive.
![After uploading](/AtlasOfLivingAustralia/documentation/wiki/img/after.png)

Click the "view records" button, you should be able to see the map of records:
![After uploading](/AtlasOfLivingAustralia/documentation/wiki/img/indexed.png)

## Add all GBIF resource for a country

A new tool makes possible to download all the GBIF resources for a given country. In order to do that, you must:

1. In the form, fill in the desired country, your GBIF.org identifiers (used to log in http://www.gbif.org/) and the number of resources required.
1. You should get all the resources of this country automatically downloaded with this tool.

## Data providers

The data providers are organizations, individuals, and other institutions as museums that provide access to some of their data.

To get the data they have given access to, here are the steps:

1. Go on http://ala-demo.org/collectory/manage/list, click on "View all data providers" then on "Add a new DataProvider". Enter a name and the URL adress of the IPT in the "enter name" part and click on "Check endpoint" in the IPT integration part.
At the end, click on "Update data resources";

1. You have to 'ingest' the new data, so go to the terminal and type :  

	`$sudo biocache`   
	`biocache>ingest -a `


@todo : the last means of data upload