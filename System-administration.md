##Backing up Cassandra data store##

Backing up Cassandra is essentially making a snapshot of occurrence store.

Cassandra comes with some command-line tools that we use for this task:
* cassandra-cli
* nodetool

###Synopsis on Cassandra occurrence store###
Where indexed occurrence data is stored:

    $ cd /data/cassandra/data/occ

(to provide directory description)

Connect to Cassandra and have a glimpse of stored records:

    $ cassandra-cli
		[default@unknown] use occ;
		[default@occ] list occ limit 1;
		
In the last line an UUID is generated automatically by Cassandra. As long as a record is contained by the same data resource determined by __druid__, the UUID will be stable.

It's also possible if you want to print out a specific record:

    [default@occ] get occ where uuid = 'e47e0e31-ff9c-4f31-b598-34f452cb023f';
		
###Making a snapshot###
Assuming it's the first time we make a snapshot, this directory should be empty before we do:

    $ cd /data/cassandra/data/occ/occ && ls

(By default this directory is owned by root so you will need to __sudo__.)

Now make a snapshot of `occ`, which we store occurrence data:

    $ nodetool snapshot occ

The terminal returns:

    Requested creating snapshot for: occ 
    Snapshot directory: 1406163740504

A directory `1406163740504` is created under `/data/cassandra/data/occ/occ/snapshots`. If you list the files under the `1406163740504` directory, you'll notice it has the same files in `/data/cassandra/data/occ/occ`. 1406163740504 is where you backup occurrence store and `/data/cassandra/data/occ/occ` is where backed up occurrence data would be restored.

(@todo explain location when biocache sampling is running)

###Pointing to a remote Cassandra instance###
Chances are you want to use a remote Cassandra instance. To do this, update `listen_address: localhost` in `/etc/cassandra/cassandra.yaml` by replacing 'localhost' with the domain name of the remote Cassandra.

##Backing up Solr index##
To be written.
