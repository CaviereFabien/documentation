As we saw in the "First data resource" topic, you can retrieve all the GBIF resources of a country.
There is also the possibility of using a data provider to get data resources.

Here are the steps for these two methods:

###Add all GBIF resource for a country###

A new tool makes possible to download all the GBIF resources for a given country. In order to do that, you must:

2. In the form, fill in the desired country, your GBIF.org identifiers (used to log in http://www.gbif.org/) and the number of resources required.
2. You should get all the resources of this country automatically downloaded with this tool.

###Data providers###

The data providers are organizations, individuals, and other institutions as museums that provide access to some of their data.

To get the data they have given access to, here are the steps:

3. Go on http://ala-demo.org/collectory/manage/list, click on "View all data providers" then on "Add a new DataProvider"   
Enter a name and the URL adress of the IPT in the "enter name" part and click on "Check endpoint" in the IPT integration part.   

At the end, click on "Update data resources";

3. You have to 'ingest' the new data, so go to the terminal and type :  
	
    $sudo biocache
    biocache>ingest -a