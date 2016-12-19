# Procedure

If you encounter this exception during data loading or processing, follow these steps

* make a snapshot with 'nodetool snapshot occ'
* stop service with 'service cassandra stop'
* run ``sstablescrub occ occ`` - this identifies and leaves the corrupt table untouched 
(has the previous command was run as sudo):
* chown -R cassandra:cassandra /data/cassandra/data/occ/occ
* move corrupt table to backup directory 
* nodetool repair occ