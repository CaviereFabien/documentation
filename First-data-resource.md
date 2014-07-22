One of the task you might want to do immediately after the installation is to upload data and see how the ALA site present the data.

Here are some preliminary steps to achieve this:

###Request a data download from the GBIF Portal###
Assuming the test installation is done by following the installation guide. We should be able to navigate to the admin interface by the following URL: <http://10.1.1.2/collectory/manage/list>.

At the very bottom of the page, two features are available for this task: 1) [Add all GBIF resource](http://10.1.1.2/collectory/manage/gbifLoadCountry) for a country; 2) [Upload GBIF file](http://10.1.1.2/collectory/dataResource/gbifUpload).

![Metadata management](/AtlasOfLivingAustralia/documentation/wiki/img/metadata_management.png)

For the purpose of testing, we want to see occurrence point on the map later. So instead of getting country data dump from GBIF Portal directly, we could instead manually create a DwC-A with search criteria that include geo-referenced occurrences. An example being [geo-referenced holotype specimens in Denmark](http://www.gbif.org/occurrence/search?HAS_COORDINATE=true&SPATIAL_ISSUES=false&COUNTRY=DK&TYPE_STATUS=LECTOTYPE), which only contains 7 records and the archive here:

Assuming the file is 0008542-140429114108248.zip

###Create a data resource on the ALA site###

Now,
1. Click 'upload' GBIF File;
1. Find the file in your desktop and click "upload";
1. The result being like this page:
![Result of uploading](/AtlasOfLivingAustralia/documentation/wiki/img/result_of_uploading.png)

Remember the UID: dr0 in the first section. This UID will be what we use for the next indexing and processing step.

Run data indexing and processing against the newly created data resource

This is done through the command-line interface. Now navigate to ala-install/vagrant/ubuntu and

    $ vagrant ssh

Then, for now, continue the rest as the root user:

    $ sudo su

Start the biocache console:

    $ biocache

Load, Sample, Process, Index the dr0 resource we have just uploaded:

    biocache> ingest dr0

At this point, visit http://10.1.1.2/collectory/public/show/dr0 and you can see that the ALA site is aware of those records in the uploaded archive.
![After uploading](/AtlasOfLivingAustralia/documentation/wiki/img/after.png)

Click the "view records" button, you should be able to see the map of records:
![After uploading](/AtlasOfLivingAustralia/documentation/wiki/img/indexed.png)

Congratulations! You now have the first data resource uploaded and processed.