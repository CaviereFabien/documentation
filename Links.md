# Links

@todo : to be completed

@todo : Mapping data ressource - collection - institution

## Provider codes

Help to map the dataResource to the institution and/or the collection 


***

### SOLUTION 1 (_Solution use on GBIF France portal_) :

>Download the DwC-A in local

>Open the resource file using Excel

>Add filters to the file

>Go to institutionCode and collectionCode

>Click on the column name for knowing the different codes used by this dataset

__IMPORTANT :__ works with resources having a number of occurrences lower than the maximum number of lines in Excel (around 1 million)

***

### SOLUTION 2 :
 
>You can also run the indexation, there is an info line with this information :

>INFO : [DataLoader] - The current institution codes for the data resource

>INFO : [DataLoader] - The current collection codes for the data resource

>Enter those codes to your platform

***

## Creating the mapping

If the specific providerCodes do not exist, enter them using “Manage provider code” page : 

`http://URL_to_your_ALA_portal/providerCode/list` 

Create the provider map between the data resource, the institution and/or the collection in the following page : 

`http://URL_to_your_ALA_portal/providerMap/list`

## Entering metadata

Fill in the metadata for the newly created dataresource. 

If the dataResource is a link to a collection :
* if it doesn’t exist :  create the collection page.
* if it does exist : add the collection to the record consumer of this dataResource 

Link the dataResource to an institution :
* if it doesn’t exist : create the institution page by filling in the metadata.
* if it exists : add the institution to the record consumer of this dataResource.

Don’t forget to go back to the dataResource page to fill in the record consumers if the collection or/and institution doesn’t exist.