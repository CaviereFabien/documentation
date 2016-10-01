# Setup the Atlas of Living Scotland

The Atlas of Living Scotland has been setup using a selection of [ansible](http://www.ansible.com/) scripts.
Most of these scripts are in the Atlas of Living Australia (ALA) repository [ala-install](http://github.com/atlasoflivingaustralia/ala-install).

This is here to provide an example of a system setup which goes beyond the ala-demo playbook, setting up more system components. 

There are a few additional ansible playbooks in this repository that have been used to setup the system.
The ansible inventories that have been used are in a private repository.


## Getting started

To reduce typing, set an unix alias up like so which points to the PEM file that you will use against the virtual machines:

```
export alias ansible-als='ansible-playbook --private-key ~/.ssh/XXXXXXXXX.pem -u ubuntu -s'
```

## Ansible playbooks used to setup the system

### Install registry (collectory)

This will setup the main registry for the system, the collectory.

```
ansible-als -i inventories/registry.als.scot ala-install/ansible/collectory.yml
```

### Install occurrence backend (biocache database)

```
ansible-als -i inventories/occurrence-db.als.scot ala-install/ansible/biocache-backend.yml
```

### Install images service

Install the image services and database backend.

```
ansible-als -i inventories/images.als.scot ala-install/ansible/image-service.yml
```

### Install central authentication service

Install the single sign on authentication component.

```
ansible-als -i inventories/auth.als.scot ala-install/ansible/auth2-standalone.yml
```

### Install sightings

Install the ad-hoc sightings components.

```
ansible-als -i inventories/ecodata.als.scot ala-install/ansible/ecodata.yml 
ansible-als -i inventories/sightings.als.scot ala-install/ansible/pigeonhole-standalone.yml 
```

### Index server

This script will setup SOLR on a standalone server.

```
ansible-als -i inventories/index.als.scot ala-install/ansible/solr-standalone.yml 
```

### Species pages webservices & UI (BIE)

This script will setup species pages and webservices on a standalone server.

```
ansible-als -i inventories/species-ws.als.scot ala-install/ansible/bie-index.yml 
ansible-als -i inventories/species.als.scot ala-install/ansible/bie-hub.yml 
```

### Biocache webservices & UI

This script will setup occurrence search pages and webservices on a standalone server.
```
ansible-als -i inventories/records-ws.als.scot ala-install/ansible/biocache-service.yml 
ansible-als -i inventories/records.als.scot ala-install/ansible/biocache-hub.yml 
```

### Install UK version of the name matching index

This script installs the name index on machines using the lucene name indexes. This would include biocache webservices, lists tool and a few other components.

```
ansible-als -i inventories/name-index als-install/ansible/name-index.yml 
```
