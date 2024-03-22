# Database Migration

It may be necessary to demonstrate a migration between ExaCS environments.  This may be parto f a demop or POC, or it may be required as we (administrators) re-do things or make updates.  For examplke, if a VM Cluster is to be de-commissioned, but you do not want to lose your database, this docuemnt gives you a couple of options.  Read on.

## Options

The options here:
* Set up Data Guard and Fail Over
* Relocate a PDB
* Clone a PDB

Data Guard is going to give you (and customers) the best experience in terms of uptime and availability.  It can be used for a migration as well.

For the Clone and Relocate options, you will need a Source and Target Container Database on different VM Clusters in the same region.  For these actions, it is recommended to have the source and target database at the same version, and retain the same administrator password.

### Data Guard

In this type of migration, you will first set up Oracle Data Guard, and then ensure it is working properly.  Following that, you will execute a failover, which will break the DG configuration, at which time you can terminate the (old)primary database.

Screen Shots TBD

DG Commands TBD

### PDB Clone

In this method, you will be able to make a clone of a PDB to another Database (on another VM Cluster), and then verify it works, then terminate the original.

### PDB Relocate

Similar to cloning, the DB itself is moved to an entirely different database.  
