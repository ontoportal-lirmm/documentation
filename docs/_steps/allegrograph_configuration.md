---
title: Allegrograph Configuration
layout: default
description: Configuring settings after installation
weight: 95
status: Ready
---

# Allegrograph Configuration

These settings will configure your installation for your environment.

## Replacing 4store with Allegrograph

Your {{site.opva}} can use either 4store or (new with version 3.0) Allegrograph 
as its RDF backend store. 
The 4store is the default RDF store for the system, as we have much more experience with it to date. 

The configuration can be changed at any time by shutting down BioPortal,
resetting the backend store configuration attribute, 
and restarting BioPortal. 
However, the Annotator and search index data will not change when you switch the backend, so it isn't really feasible to go back and forth—you'll 
want to pick your backend system at the beginning,
or be prepared to re-index your databases with each switch.

### What's included?

We included a version of Allegrograph with your Appliance
that is tested to work with this version of the Appliance.
The included Allegrograph is not necessarily the most recent version of the Allegrograph software. 

If you want to upgrade your Allegrograph software to the most recent version,
you can obtain that from the Franz, Inc. website. 
However, we can not guarantee the compatibility of the Appliance
with the latest Allegrograph version.

### How to switch the Configuration

Update the configuration file inside your Virtual Appliance (VA)

	a) replace the following lines:
```
		config.goo_host          = 'localhost'
    	config.goo_port          = 8081
```
       with:

	    config.goo_backend_name  = 'AG'
	    config.goo_host          = 'localhost' # or your server name
	    config.goo_port          = 10035
	    config.goo_path_query    = '/repositories/ontoportal' # the last fragment must match the name of the repository you created in Step 3.
	    config.goo_path_data     = '/repositories/ontoportal/statements'
	    config.goo_path_update   = '/repositories/ontoportal/statements'

Restart your Virtual Appliance (see below). Your server is now pointing to AG as the backend.


## Obtaining and starting Allegrograph

1. If not already present in a current version, install the AllegroGraph (AG) server using the instructions on this page:

`https://franz.com/agraph/support/documentation/current/server-installation.html`

We recommend reviewing these instructions, which cover a number of different installation scenarios.

An example from this page of commands to start and stop Allegrograph:

```
Note that the last few lines of the script show how to start and stop AllegroGraph on your server. These lines will be similar to this example:

You can start AllegroGraph by running:  
/sbin/service agraph start  
 
You can stop AllegroGraph by running:  
/sbin/service agraph stop 
```

2. Once Allegrograph is running, navigate to the AG Admin console. By default it runs on port 10035:

```
http://<your server name>:10035/#
```

3. Under "Create new repository" type in a name for your new repository to be used for OntoPortal and click "Create". For Example: ontoportal

4. Once created, you should be able to navigate to your new repository via:

```
	http://<your server name>:10035/#/repositories/ontoportal
```

From this view, you can run SPARQL queries against your data, add or delete records, export the repository in a number of formats, and run reports on the use of your data store.
	

