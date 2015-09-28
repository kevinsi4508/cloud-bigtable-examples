# Coinflow Backend

This is a Cloud Dataflow rewrite of the [Apache Storm](https://github.com/GoogleCloudPlatform/cloud-bigtable-examples/tree/master/java/storm) example.

It stores the Coinflow Websocket data inside Cloud Bigtable, along with calculating some moving
price average analytics using Cloud Dataflow Windows.

Since this is a streaming example using an unbounded source, it is currently not possible to run
this pipeline locally.

## Project Setup

## Project setup

### Install the Google Cloud Platform SDK

In order to run this mapreduce sample please follow the Cloud Bigtable [Getting Started](https://cloud.google.com/bigtable/docs/hbase-shell-quickstart#before_you_start)

  * Create a project
  * Enable Billing
  * Create a [Cloud Bigtable Cluster](https://cloud.google.com/bigtable/docs/creating-cluster)
  * Development Environment Setup
      * Install [Google Cloud SDK](https://cloud.google.com/sdk/)
      * Install [Java 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or higher.
      * Install [Apache Maven](https://maven.apache.org/)

### Provision a Bigtable Cluster

In order to provision a Cloud Bigtable cluster you will first need to create a
Google Cloud Platform project. You can create a project using the
[Developer Console](https://cloud.google.com/console).

After you have created a project you can create a new [Cloud Bigtable cluster](https://cloud.google.com/bigtable/docs/creating-cluster) by
clicking on the "Storage" -> "Cloud Bigtable" menu item and clicking on the
"New Cluster" button.  After that, enter the cluster name, ID, zone, and number
of nodes. Once you have entered those values, click the "Create" button to
provision the cluster.

### Make a GCS Bucket

Make a GCS bucket that will be used by bdutil to store its output and to copy
files to the VMs.  There are two ways to make a GCS Bucket,

1. In the Cloud Console, select "Storage" > "Cloud Storage" > "Storage
   browser" and click on the "Add bucket" button. Type the name for your
   bucket and click "Create".  (Note - Names are a global resource, so make
   yours long and unique)
1. Use the gsutil tool's Make Bucket command:

    `$ gsutil mb -p <project ID> gs://<bucketName>`

### Create The Bigtable Table

1. Follow the instructions to run the [HBase Shell](https://cloud.google.com/bigtable/docs/hbase-shell-quickstart)
1. Launch hbase shell
1. Create the table (here, table name is coinbase, and column family is cb)

    `create 'coinbase', 'cb'`
1. If you used a different table name or column family, be sure to change it Schema.java.

### Build the Jar File

    `mvn clean package`

## Deploying

1. Run:

    `./run.sh` <your-project-id> <your-bigtable-cluster-id> <your-bigtable-table>


Copyright Google 2015