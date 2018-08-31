# Amazon RDS(Relational Database Service)

Migrate your database instances quickly to the another region use cross-region replication.
 
You can Set the `Auto Minor Version Upgrade to “No” ` to prevent any minor upgrades
from automatically taking place. 
 
You can use the reader endpoint to provide high availability for your read-only
queries from your DB cluster. You can place multiple Aurora Replicas in different 
Availability Zones and then connect to the reader endpoint for your read workload.

If your DB instance is not in a VPC, you can use the AWS Management
Console to easily move your DB instance into a VPC. You can also take 
a snapshot of your DB Instance outside VPC and restore it to VPC by
specifying the DB Subnet Group you want to use.

When you restore a snapshot, you cannot restore to the existing DB 
instance; you will have to restore to a new instance.

MS SQL Server Express and Web editions can range in size from 100 GB to 4 TB. 
SQL Server Standard and Enterprise editions can range in size from 200 GB to 4 TB.

Amazon RDS for MySQL, MariaDB and PostgreSQL allow you to add up to 5 read replicas to each DB Instance.

Read Replicas maybe called as Sql replicas. And remember that Aurora Replicas os not the same thing as read replicas

A database parameter group (DB Parameter Group) acts as a “container” for engine 
configuration values that can be applied to one or more DB Instances. If you create 
a DB Instance without specifying a DB Parameter Group, a default DB Parameter Group
is used.

To disable automated backups for a DB instance, set the backup retention parameter to 0; 
e.g. using the API – BackupRetentionPeriod = 0

## What RDS do

Amazon Relational Database Service 

## Some random facts to remember

RDS doesn't provide shell access to DB instances.

Use MySQL, MariaDB, or PostgreSQL Read Replicas to increase read scaling.

A DB instance is an isolated database environment running in the cloud. It is the basic 
building block of Amazon RDS

You can have up to 40 Amazon RDS DB instances. Of these 40, up to 10 can be Oracle or 
SQL Server DB instances under the "License Included" model.

While launch RDS instance you have flag 'Publicly accessible', defines whether assign
public IP address to instance or not.


## Read replicas 

Amazon RDS uses the MariaDB, MySQL, and PostgreSQL DB engines' built-in replication 
functionality to create a special type of DB instance called a Read Replica from a 
source DB instance. Updates made to the source DB instance are asynchronously copied
to the Read Replica. 

You can reduce the load on your source DB instance by routing 
read queries from your applications to the Read Replica. Using Read Replicas, you 
can elastically scale out beyond the capacity constraints of a single DB instance 
for read-heavy database workloads.

The Read Replica operates as a DB instance that allows only read-only connections.
Applications connect to a Read Replica the same way they do to any DB instance.
Amazon RDS replicates all databases in the source DB instance.

## Tags

Each Amazon RDS resource has a tag set, which contains all the tags that are 
assigned to that Amazon RDS resource. A tag set can contain as many as 10 tags,
or it can be empty. If you add a tag to an Amazon RDS resource that has the 
same key as an existing tag on resource, the new value overwrites the old value.
 
Ket-Value limits:  
* Key limit :  1 to 128 Unicode
* Value limit : 1 to 256 Unicode

## Multi-AZ

Technologies to provide Multi-AZ support: 
* **Amazon's failover technology** for Multi-AZ deployments(supported by Oracle, 
PostgreSQL, MySQL, and MariaDB) 
* SQL Server DB instances use **SQL Server Mirroring**. 
* **Amazon Aurora instances stores copies of the data** in a DB cluster across multiple AZ in Region

## Subnet group

Db subnet group defines which subnets and IP ranges the DB instance can use in VPC

## RDS Snapshot types

* automated - Return all DB snapshots that have been automatically taken by Amazon RDS for my AWS account.
* manual - Return all DB snapshots that have been taken by my AWS account.
* shared - Return all manual DB snapshots that have been shared to my AWS account.
* public - Return all DB snapshots that have been marked as public.



## Limits 

Backup retention period limits: 
* Default value = 1 day
* Min = 1 day
* Max = 35 days
* By the way, you cannot disable automated backups on Aurora

## Backups 


Amazon RDS creates a storage volume snapshot of your DB instance, backing up the entire DB 
instance and not just individual databases.


## AURORA
Amazon Aurora (Aurora) is a fully managed, **MySQL-** and **PostgreSQL-** compatible, relational database engine.

Can't be used in free-tier

Up to 15 Aurora Replicas

### Aurora serverless feature

Amazon Aurora Serverless is an on-demand, autoscaling configuration for Amazon Aurora. 

It's relatively simple, cost-effective option for infrequent, intermittent, 
or unpredictable workloads. 

Max size of the Aurora cluster volume is 64TB

The minimum storage is 10GB. Based on your database usage, your Amazon Aurora 
storage will automatically grow, up to 64 TB, in 10GB increments with no impact 
to database performance. You do not have provision storage in advance. Your 
database volume is divided into 10GB segments spread across many disks.