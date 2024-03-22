# Database Migration (WIP)

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

In this method, you will be able to make a clone of a PDB to another Database (on another VM Cluster), and then verify it works, then terminate the original.  Before cloning, check source connectivity:

```bash

[opc@stuff ~]$ sqlplus sys@dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com:1521/MIGRSRC_PDB1.paas.oracle.com as sysdba

SQL*Plus: Release 19.0.0.0.0 - Production on Fri Mar 22 15:31:34 2024
Version 19.13.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
Version 19.22.0.0.0

SQL> select name from v$DATABASE;

NAME
---------
MIGRSRC
```

Cloning involves choosing a VM Cluster with an available Database to perform a remote clone to.

### PDB Relocate

Similar to cloning, the DB itself is moved to an entirely different database.  In the example below, the MIGRSRC Database has a PDB named PDB1 that we want to migrate to a Database called MIGRTGT on another VM Cluster.  Start by verifying connectivity to the source:

```bash

[opc@stuff ~]$ sqlplus sys@dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com:1521/MIGRSRC_PDB1.paas.oracle.com as sysdba

SQL*Plus: Release 19.0.0.0.0 - Production on Fri Mar 22 15:31:34 2024
Version 19.13.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
Version 19.22.0.0.0

SQL> select name from v$DATABASE;

NAME
---------
MIGRSRC
```
Now clone the database to the target database.  

Once complete (10-15 min), log into the new cloned DB.  Here is the connection detail:



```bash
[opc@stuff ~]$ sqlplus sys@kompally-zs9ta-scan.sub09231348061.exaiadvcn.oraclevcn.com:1521/AGIADS01_PDB1CLONE.paas.oracle.com as sysdba

SQL*Plus: Release 19.0.0.0.0 - Production on Fri Mar 22 15:49:23 2024
Version 19.13.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
Version 19.22.0.0.0

SQL> select name from v$DATABASE;

NAME
---------
AGIADS01
```

Now migrate the PDB to another Database. Note that you can change the name here, as shown.

