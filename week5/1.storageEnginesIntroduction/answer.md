## Question

The storage engine directly determines which of the following?

>Pluggable storage engines were introduced in MongoDB 3.0. Though this video makes repeated reference to MongoDB 3.0, that is not the latest release. In MongoDB 3.2, WiredTiger became the default storage engine. So simply running mongod from the command line will launch MongoDB with WiredTiger as the storage engine used. You can find the most recent release of MongoDB here.

## Answer

[The storage engine](https://docs.mongodb.com/manual/core/storage-engines/) is the component of the database that is responsible for managing how data is stored, both in memory and on disk. MongoDB supports multiple storage engines, as different engines perform better for specific workloads. 

drivers --> mongoServer --> storageEngine --> disk


- the data file format
- architecture of a cluster (doesn't affect communication between server )
- the wire protocol for the drivers (drivers talk to the server and server to store engine)
- format of indexes

## Result

- the data file format
- format of indexes