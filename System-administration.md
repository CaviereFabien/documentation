##Backing up Cassandra data store##

Backing up Cassandra is essentially making a snapshot of occurrence store.

Cassandra comes with some command-line tools that we will use for this task:
* cassandra-cli
* nodetool

###Synopsis on Cassandra occurrence store###
Where indexed occurrence data is stored:

    $ cd /data/cassandra/data/occ

Connect to Cassandra and have a glimpse of stored records:

    $ cassandra-cli
		[default@unknown] use occ;
		[default@occ] list occ limit 1;
		
It's also possible if you want to print a particular record:

    [default@occ] get occ where uuid = 'e47e0e31-ff9c-4f31-b598-34f452cb023f';
		

    
(to provide directory description)





###Making a snapshot###

    $ nodetool snapshot occ
    $ cd cassandra/data/
    $ ls -la
    $ cd occ
    $ ls -al

loc for sampling. environment

    $ cd snapshots # backups are here
    


##Solr index##

		
    $ 

###Pointing to a remote Cassandra instance###
cassandraHost