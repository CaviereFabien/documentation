# Biocache ingest

@todo : to be completed

## Ingest of resources

### Dataset

***

#### In case of a small dataresource ( < 50 000 records) 

1 Connect to the server where your biocache tool is hosted

2 Connect to biocache 

	$ sudo biocache

3 Run the following command line: 

	$ ingest –dr <dataresource_id>

You can also run directly on the terminal

	$ sudo biocache ingest -dr <dataresource_id>
	
__Important :__ you will not have logs if you don’t specify the out file.

***

#### In case of a big dataresource ( > 50 000 records and < 8 millions)

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

#### In case of a really big dataresource ( DwC-A size > 1 Go)

 1 Upload a modified DwC-Archive with 15 occurrences in order to create the dataset into the system.

 2 Copy the real DwC-Archive instead of the modified one on the `/collectory/upload/` folder

 3 Then run the load, process and index commands : 

	$ load <dataResource_id>
	$ process -dr <dataResource_id>
	$ sample -dr <dataResource_id> 
	$ index -dr <dataResource_id>
 
 We need to do step 1 because the ZipFile library used by the biocache-store can’t open a file bigger than 1 GO

 You need to have a server with at least the size of your DwC-Archive in RAM. 


### All of your resources

You can run one command line (as sudo user):

	$ nohup biocache ingest -all > /tmp/load.log &

You can run three different command lines directly on the terminal (as sudo user):

	$ biocache bulk-processor load -t 7 > data/output_load.log
	$ biocache bulk-processor process -t 6 > data/output_process.log
	$ biocache bulk-processor index -ps 1000 -t 8 > /data/output_index.log

With the `-t` option, you will give the number of CPU you want to use for the processus.

With the `-ps` option, you will give the number of occurrences per pages on SOLR. 

## use & good pratices of Biocache
		
@todo : to be completed ; don't enter on biocache for biocache command line (flag by institution/ALA production)
	
## command for spatial module

@todo : to be completed