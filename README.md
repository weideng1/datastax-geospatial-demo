Geo Spatial Demo
====================

NOTE - this example requires DSE > 4.5

## Scenario

This is short demo which shows how to find all the uk postcode within a certain area. This area can be a postcode
or a longitude/latitude combination.

## Schema Setup
Note : This will drop the keyspace "datastax_postcode_demo" and create a new one. All existing data will be lost. 

To specify contact points use the contactPoints command line parameter e.g. '-DcontactPoints=192.168.25.100,192.168.25.101'
The contact points can take mulitple points in the IP,IP,IP (no spaces).

To create the a single node cluster with replication factor of 1 for standard localhost setup, run the following

    mvn clean compile exec:java -Dexec.mainClass="com.datastax.demo.SchemaSetup"

Now we can load the postcode data from the postcodes_new.csv file in the home directory.

You can use the cqlsh copy to do this. 

Open a cql shell and run  

	copy datastax_postcode_demo.postcodes (post_code, lon_lat) from '{demo_dir}/postcodes_new.csv';

When the data is loaded, the Solr code needs to be updated with config and schema which will allow us to search.

Then go to the 'src/main/resources/solr'

Use the 'Commands.txt' file which shows the commands run to add the config and schema to create the Solr core. The commands assume you are running this on your localhost, if you are not, you will need to change the host name. 

Once these commands have been run, we can start to query the Solr Admin. 

First we will using the 'q' field to query for post_code = SW209AQ

![Image of Postcode lookup]
(https://raw.githubusercontent.com/PatrickCallaghan/images/master/PostCodeLookup.png)

To remove the tables and the schema, run the following.

    mvn clean compile exec:java -Dexec.mainClass="com.datastax.demo.SchemaTeardown"
    
    
