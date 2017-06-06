## Overview
This page will cover the process of management of data resource :
* How to update data resource
* Provider codes
* Entering metadata
* Creating the mapping
* Ingest of resources

# How to update data resource#

See the [[First data resource|First-data-resource]] and [[Other ways to add data resource|Other-ways-to-add-data-resource]] pages.


# Provider codes#

Help to map the dataResource to the institution and/or the collection 


***

### SOLUTION 1 (_Solution use on GBIF France portal_) : ###

>Download the DwC-A in local

>Open the resource file using Excel

>Add filters to the file

>Go to institutionCode and collectionCode

>Click on the column name for knowing the different codes used by this dataset

__IMPORTANT :__ works with resources having a number of occurrences lower than the maximum number of lines in Excel (around 1 million)

***

### SOLUTION 2 : ###
 
>You can also run the indexation, there is an info line with this information :

>INFO : [DataLoader] - The current institution codes for the data resource

>INFO : [DataLoader] - The current collection codes for the data resource

>Enter those codes to your platform

***


# Entering metadata #

Fill in the metadata for the newly created dataresource. 

If the dataResource is a link to a collection :
* if it doesn’t exist :  create the collection page.
* if it does exist : add the collection to the record consumer of this dataResource 

Link the dataResource to an institution :
* if it doesn’t exist : create the institution page by filling in the metadata.
* if it exists : add the institution to the record consumer of this dataResource.

Don’t forget to go back to the dataResource page to fill in the record consumers if the collection or/and institution doesn’t exist. 

# Creating the mapping #

If the specific providerCodes do not exist, enter them using “Manage provider code” page : 

`http://URL_to_your_ALA_portal/providerCode/list` 

Create the provider map between the data resource, the institution and/or the collection in the following page : 

`http://URL_to_your_ALA_portal/providerMap/list`

# Ingest of resources#

## Dataset ##

***

### In case of a small dataresource ( < 50 000 records)###

1 Connect to the server where your biocache tool is hosted

2 Connect to biocache 

	$ sudo biocache

3 Run the following command line: 

	$ ingest –dr <dataresource_id>

You can also run directly on the terminal

	$ sudo biocache ingest -dr <dataresource_id>
	
__Important :__ you will not have logs if you don’t specify the out file.

***

### In case of a big dataresource ( > 50 000 records and < 8 millions) ###

1 Connect to the server where your biocache tool is hosted

2 Connect to biocache : 

	$ sudo biocache

3 Run the following command lines: 

	$ load <dataResource_id>
	$ process -dr <dataResource_id>
	$ sample -dr <dataResource_id> 
	$ index -dr <dataResource_id>

You can also run directly on the terminal, the command lines above with 

	$ sudo biocache 

***

### In case of a really big dataresource ( DwC-A size > 1 Go) ###

 1 Upload a modified DwC-Archive with 15 occurrences in order to create the dataset into the system.

 2 Copy the real DwC-Archive instead of the modified one on the `/collectory/upload/` folder

 3 Then run the load, process and index commands : 

	$ load <dataResource_id>
	$ process -dr <dataResource_id>
	$ sample -dr <dataResource_id> 
	$ index -dr <dataResource_id>
 
 We need to do step 1 because the ZipFile library used by the biocache-store can’t open a file bigger than 1 GO

 You need to have a server with at least the size of your DwC-Archive in RAM. 


## All of your resources ##

You can run one command line (as sudo user):

	$ nohup biocache ingest -all > /tmp/load.log &

You can run three different command lines directly on the terminal (as sudo user):

	$ biocache bulk-processor load -t 7 > data/output_load.log
	$ biocache bulk-processor process -t 6 > data/output_process.log
	$ biocache bulk-processor index -ps 1000 -t 8 > /data/output_index.log

With the `-t` option, you will give the number of CPU you want to use for the processus.

With the `-ps` option, you will give the number of occurrences per pages on SOLR. 