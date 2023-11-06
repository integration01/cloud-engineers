# Using ExaCS or ADB-D
These services both exist in the tenancy as a way for us to utilize dedicated resources and save on costs of using serverless Autonomous and DBaaS.  We have set these services up in such a way that engineers can use them.

All Infrastructure and VM Clusters exist in the compartment called `(root) / cloud-engineering-shared / ExaCS `.  The VCN that all shared clusters utilizes is attached to a Dynamic Routing Gateway, and this docuemnt will describe how to connect to this DRG from any other VCN in the region.

## Diagram of compartment, VCN

Diagram

## Creation of ExaCS Database
Create an ExaCS DB

### Using Data Guard
After the database has been created, create a DG peer...

### Using Database Management
Enable for DB Management

## Creation of ADB Database
Within an ACD...

### Using Data Guard
Use of Data Guard should be decided up front, as there are 2 ADB Autonomous Container Databases (ACD) to choose from.  One is enabled for Autonomous Data Guard, the other is not.  Placement of an ADB instance within one of these ACDs will dictate whether Data Guard is enabled for that database.

## VCN Connection Details
Attaching your VCN, etc...

## Connection Details
Install SQL Plus on your VM in your VCN...
