# Using ExaCS or ADB-D
These services both exist in the tenancy as a way for us to utilize dedicated resources and save on costs of using serverless Autonomous and DBaaS.  We have set these services up in such a way that engineers can use them.

All Infrastructure and VM Clusters exist in the compartment called `(root) / cloud-engineering-shared / ExaCS `.  The VCN that all shared clusters utilizes is attached to a Dynamic Routing Gateway, and this docuemnt will describe how to connect to this DRG from any other VCN in the region.

## Diagram of Compartment, VCN, Infra, Clusters, Connections

![Diagram](images/ExaCS-ADB-Integration01-Nov%202023.png)

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

### Ranges required for ExaCS
* Ashburn IAD - 172.16.100.0/24
* Phoenix PHX - 172.17.100.0/24

### DRG Attachment
Attach your VCN to the DRG in either or both regions

### DNS Resolver
DNS Resolver Private View to ExaCS VCN

### Route to DRG
Add a route from your subnet's route table to DRG for the ExaCS CIDR Block

### Security List or NSG
Add Egress TCP/1521 for the block above

## Connection Details
Install SQL Plus on your VM in your VCN...

sudo dnf install oracle-instantclient-release-el8
sudo dnf install oracle-instantclient-basic
sudo dnf install oracle-instantclient-sqlplus

### Ensure nslookup and nc work
Before connecting to any DB, please check both that the SCAN Listeners are able to nslookup and can connect on port 1521:

#### ExaCS IAD VM Cluster

```bash
[opc@engineer-vm ~]$ nslookup dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com
Server:		169.254.169.254
Address:	169.254.169.254#53

Non-authoritative answer:
Name:	dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.207
Name:	dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.220
Name:	dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.161
```
NC output
```bash
[opc@engineer-vm ~]$ nc -vz dbnode-giusq-scan.sub09231348061.exaiadvcn.oraclevcn.com 1521
Ncat: Version 7.70 ( https://nmap.org/ncat )
Ncat: Connected to 172.16.100.220:1521.
Ncat: 0 bytes sent, 0 bytes received in 0.01 seconds.
```
#### ExaCS IAD ADB VM Cluster

```bash
[opc@engineer-vm ~]$ nslookup host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com
Server:		169.254.169.254
Address:	169.254.169.254#53

Non-authoritative answer:
Name:	host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.190
Name:	host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.231
Name:	host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com
Address: 172.16.100.192
```
NC Output
```bash
[opc@engineer-vm ~]$ nc -vz host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com 1521
Ncat: Version 7.70 ( https://nmap.org/ncat )
Ncat: Connected to 172.16.100.192:1521.
Ncat: 0 bytes sent, 0 bytes received in 0.01 seconds.
```
### Connect to ExaCS instance

### Connect to ADB-D instance
Example of connecting to an ADB-D instance from your VM:

```bash
[opc@engineer-vm ~]$ sqlplus admin@(DESCRIPTION=(CONNECT_TIMEOUT=90)(RETRY_COUNT=50)(RETRY_DELAY=3)(TRANSPORT_CONNECT_TIMEOUT=3)(ADDRESS_LIST=(LOAD_BALANCE=ON)(ADDRESS=(PROTOCOL=TCP)(HOST=host-knpvi-scan.sub09231348061.exaiadvcn.oraclevcn.com)(PORT=1521)))(CONNECT_DATA=(SERVICE_NAME=AGADBDG_medium.atp.oraclecloud.com)))
```
