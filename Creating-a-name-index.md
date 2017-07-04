# Creating a name index

Name indexing happens during the "processing" phase of ingestion. If a customised/national checklist is required, a new name index can be created.

## Playbook nameindexer-standalone.yml
Assuming you have an instance of ALA portal running, when you need to use your own name index, or update the existing name index, you want to run it separately so it doesn't potentially break the running service.

So as the tutorial of building a customised name index, we start from a vanilla vagrant ubuntu box.

    $ cd ala-install/vagrant/ubuntu
    $ vagrant status

At this point, if you have a vagrant box running, consider destroy it and start a fresh one.

    $ vagrant destroy
    $ vagrant up

Ensure the virtual box is up-and-running and you can login:

    $ vagrant ssh

Now, run the playbook for creating the instance that builds nameindexes:

    $ cd ../../ansible
    $ ansible-playbook -i inventories/vagrant nameindexer-standalone.yml --private-key ~/.vagrant.d/insecure_private_key -u root

Where the name sources are stored:

    $ cd /data/lucene/sources

Observe the target folder before we do name indexing:

    $ ls /data/lucene

It should have only 'sources' as a directory.

Now, to create a name index:

    $ sudo nameindexer -dwca /data/lucene/sources/dwca-col-mammals

(As 23 Jul 14, the default owner of /data is root so you need sudo to run nameindexer.)

Notice that here the 'dwca-col-mammals' is a directory extracted from dwca-col-mammals.zip. If you are working on your own checklist in DwC-A format, make sure you extract it before fire the nameindexer. Do `$ nameindexer -help` for more information.

Test search to see if the name index has been built successfully:

    $ sudo nameindexer -testSearch "Macropus rufus"

And you should see:

    Search for name
    ID: 6863103
    GUID: urn:lsid:catalogueoflife.org:taxon:d9f7aefa-29c1-102b-9a4a-00304854f820:col20120124
    Classification: "(Desmarest, 1822)",Animalia,Chordata,Mammalia,Diprotodontia,Macropodidae,Macropus
    Scientific name: Macropus rufus
    Authorship: (Desmarest, 1822)
    Rank: SPECIES
    Synonym: null
    Match type: exactMatch

That means you've got a working index.

After running the command above, `$ ls /data/lucene`, you'll see two new directories:

    namematching
    nmload-tmp

To use the new name index, you can zip these two directories and unzip and replace the same one on your production site. The next step would be to update the occurrence Solr index to use this new name index.

If only a few datasets with a rather small number (< ~5m) of record, you would simply run:

    biocache> index -dr [druid]

But if it's more than that, you should do:

    biocache> bulk-processor

## Supported checklist formats
To be written.

## About homonyms
The name indexing by default looks for `/data/lucene/sources/IRMNG_DWC_HOMONYMS` to analyse homonyms. If you have alternative homonyms to detect against, run `nameindexer` with `-irmng` flag and point to your own extracted homonym DwC-A.

To avoid obvious homonym indexing error, you can provide taxonomy hints in the Collectory when you edit the metadata of data resources by providing a taxonomy hint. The URL would be `/collectory/dataResource/edit/[druid]?page=%2Fshared%2FeditTaxonomyHints`. (Replace [druid] with your own.)