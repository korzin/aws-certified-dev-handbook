#EC2 Scope

## Amazon Machine Images (AMI)

 Display AMI: DescribeImages -Provides the information required to launch an instance.
 
### AMI Lifecycle


                                                                     --(launch)-->[EC2 Instance]
                                                                   /
    --(create)-->[Template for instance]---(register)-->[AMI#1]---| 
                                                           |       \
                                                           |         --(copy)---->[AMI#2]
                                                      (deregister)
          
A shared AMI is an AMI that a developer created and made available for other developers to use.                                          
             
Snapshots of both data and root volumes can be encrypted and attached to an AMI. EC2 instances with encrypted volumes are launched from AMIs in the same way as other instances.
                                                                                 
If you have an AMI with encrypted snapshots, you can choose to re-encrypt them with a different encryption key as part of the CopyImage action. 

                                              
### AMI Types
You can select an AMI to use based on the following characteristics:
* Region (by the way. AMI can be copied to another region)
* Operating system
* Architecture (32-bit or 64-bit)
* Launch Permissions

    |Launch Permission|	Description|
    |-----------------|---|
    |public|	The owner grants launch permissions to all AWS accounts.|
    |explicit|	The owner grants launch permissions to specific AWS accounts.|
    |implicit|	The owner has implicit launch permissions for an AMI.|
* Storage for the Root Device (**EBS-backed AMI** vs **Instance-backed AMI**) 
                                                     
### Linux AMI Virtualization Types:
* HVM AMIs (all instances support)
  HVM AMIs are presented with a fully virtualized set of hardware and boot by executing the master boot record of the root block device of your image. This virtualization type provides the ability to run an operating system directly on top of a virtual machine without any modification, as if it were run on the bare-metal hardware.
* PV AMIs (specific inctances support)
  PV AMIs boot with a special boot loader called PV-GRUB, which starts the boot cycle and then chain loads the kernel specified in the menu.lst file on your image. Paravirtual guests can run on host hardware that does not have explicit support for virtualization, but they cannot take advantage of special hardware extensions such as enhanced networking or GPU processing.
* PV on HVM
             
                                               
                                               
------

## EC2 Service

### Shared responsibility model //TODO

![Shared responsibility model][https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg]

With the AWS Shared Responsibility Model, the security implementation of a customer’s infrastructure 
is shared between AWS and the customer. AWS is responsible for the global security “of” the cloud, 
which in practice means, protecting the underlying infrastructure (network, hardware, software, and 
facilities) from vulnerabilities, fraud, abuse, and intrusions, and providing customers with the 
necessary security capabilities.

On the other hand, the customer is responsible for security “in” the cloud, which 
means, the security of their content, applications, platform, operating systems, and networks.
 While AWS offers you several security tools to help you with security, such as CloudTrail, Security 
 Groups, and IAM, their implementation is optional. Customers have the control to choose what security
  they want to implement to protect their IT infrastructure. Therefore, it’s important that customers 
  carefully consider the services they select because their responsibility is determined by the AWS 
  Cloud Services they choose.

### Network and Security

If an instance fails and you launch a replacement instance, the replacement has a different public IP address than the original. However, if your application needs a static IP address, you can use an Elastic IP address.
 
**The keys that Amazon EC2 uses are 2048-bit SSH-2 RSA keys. You can have up to five thousand key pairs per region.**

An EC2 instance can only ONE role attached at a time

If the Amazon EC2 action that you are testing creates or modifies a resource, you should make the request using the DryRun parameter (or run the AWS CLI command with the --dry-run option). In this case, the call completes the authorization check, but does not complete the operation. 

#### Elastic IP Addresses

 With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.

A disassociated Elastic IP address remains allocated to your account until you explicitly release it.

An Elastic IP address is for use in a specific region only.

You can move an Elastic IP address from one instance to another. The instance can be in the same VPC or another VPC, but not in EC2-Classic.

Your Elastic IP addresses remain associated with your AWS account until you explicitly release them.

LIMIT : You're limited to 5 Elastic IP addresses; to help conserve them, you can use a NAT device (see NAT).

#### Network interface

A network interface can include the following attributes:
* A primary private IPv4 address from the IPv4 address range of your VPC
* One or more secondary private IPv4 addresses from the IPv4 address range of your VPC
* One Elastic IP address (IPv4) per private IPv4 address
* One public IPv4 address
* One or more IPv6 addresses
* One or more security groups
* A MAC address
* A source/destination check flag
* A description

#### Security Groups

A security group acts as a firewall that controls the traffic allowed to reach one or more instances. When you launch an instance, you assign it one or more security groups. You add rules to each security group that control traffic for the instance. 

The following are the characteristics of security group rules:
* By default, security groups allow all outbound traffic.
* You can't change the outbound rules for an EC2-Classic security group.
* Security group rules are always permissive; you can't create rules that deny access.
* Security groups are stateful — if you send a request from your instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules. For VPC security groups, this also means that responses to allowed inbound traffic are allowed to flow out, regardless of outbound rules. For more information, see Connection Tracking.
* You can add and remove rules at any time. Your changes are automatically applied to the instances associated with the security group after a short period. 
  Note: The effect of some rule changes may depend on how the traffic is tracked. For more information, see Connection Tracking.
* When you associate multiple security groups with an instance, the rules from each security group are effectively aggregated to create one set of rules. We use this set of rules to determine whether to allow access. 
  
  Note: You can assign multiple security groups to an instance, therefore an instance can have hundreds of rules that apply. This might cause problems when you access the instance. We recommend that you condense your rules as much as possible.

Use    
      
      describe-prefix-lists

API command return ** prefix list name and prefix list ID of the service and the IP address range for the service** 

**For each rule, you specify the following:**

* Protocol: The protocol to allow. The most common protocols are 6 (TCP) 17 (UDP), and 1 (ICMP).

* Port range : For TCP, UDP, or a custom protocol, the range of ports to allow. You can specify a single port number (for example, 22), or range of port numbers (for example, 7000-8000).

ICMP type and code: For ICMP, the ICMP type and code.

* Source or destination: The source (inbound rules) or destination (outbound rules) for the traffic. Specify one of these options:
    * An individual IPv4 address. You must use the /32 prefix length; for example, 203.0.113.1/32.
    * (VPC only) An individual IPv6 address. You must use the /128 prefix length; for example 2001:db8:1234:1a00::123/128.
    * A range of IPv4 addresses, in CIDR block notation, for example, 203.0.113.0/24.
    * (VPC only) A range of IPv6 addresses, in CIDR block notation, for example, 2001:db8:1234:1a00::/64.
    * (VPC only) The prefix list ID for the AWS service; for example, pl-1a2b3c4d. For more information, see Gateway VPC Endpoints in the Amazon VPC User Guide.
    * Another security group. This allows instances associated with the specified security group to access instances associated with this security group. This does not add rules from the source security group to this security group. You can specify one of the following security groups:
       * The current security group.
       * EC2-VPC: A different security group for the same VPC or a peer VPC in a VPC peering connection.
* (Optional) Description: You can add a description for the rule;

###Instance Metadata and User Data

#### Metadata

Instance metadata is data about your instance that you can use to configure or manage the running instance.

curl http://169.254.169.254/latest/meta-data/ 

* ami-id and other AMI info
* block-device-mapping/ 
* hostname
* iam/  
* instance-action
* instance-id
* instance-type
* local-hostname
* local-ipv4
* mac
* metrics/
* network/ you can get subnetId
* placement/
* profile
* public-hostname
* public-ipv4
* public-keys/
* reservation-id
* security-groups
* services/


#### User data

http://169.254.169.254/latest/user-data

If you stop an instance, modify its user data, and start the instance, the updated user data is not executed when you start the instance.

User data is limited to 16 KB. This limit applies to the data in raw form, not base64-encoded form.


### EC2 Monitoring
    
#### Automated Monitoring Tools

* System Status Checks 
  
   monitor the AWS systems required to use your instance to ensure they are working properly. These checks detect problems with your instance that require AWS involvement to repair.
   
   Examples : 
   * Loss of network connectivity
   * Loss of system power
   * Software issues on the physical host
   * Hardware issues on the physical host 

* Instance Status Checks - monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair. When an instance status check fails, typically you will need to address the problem yourself (for example by rebooting the instance or by making modifications in your operating system). 

  Examples of problems that may cause instance status checks to fail include:
  * Failed system status checks
  * Misconfigured networking or startup configuration
  * Exhausted memory
  * Corrupted file system
  * Incompatible kernel
  
* Amazon CloudWatch Alarms 
* Amazon CloudWatch Events 
* Amazon CloudWatch Logs
* CloudWatch Agent

#### Manual Monitoring Tools
* EC2 Dashboard
* CloudWatch dashboard


#### Important metrics
|Item to Monitor|	Amazon EC2 Metric	|Monitoring Agent/CloudWatch Logs|
|---|---|---|
|CPU utilization | CPUUtilization |  |
|Network utilization | NetworkIn |  |
|NetworkOut | Disk performance |  |
|DiskReadOps | DiskWriteOps  |  |
|Disk Reads/Writes | DiskReadBytes and DiskWriteBytes  |  |
|Memory utilization, disk swap utilization, disk space utilization, page file utilization, log collection |  |CloudWatch Agent|


-------

## Instance types 

### Instance Family	Current Generation Instance Types:
#### **General purpose**(examples : t2.2xlarge , m4.large)

General purpose instances provide a balance of compute, memory, and networking resources, and can be used for a variety of workloads.

* M5 instances 

    M5 instances are the latest generation in Amazon EC2's General purpose instance family. M5 instances give you an ideal cloud infrastructure, offering a balance of compute, memory, and networking resources for a broad range of applications that are deployed in the cloud. 

    M5 instances are well-suited for the following applications:
    * Web and application servers
    * Small and medium databases
    * Gaming servers
    * Caching fleets
* T2 Instances
  
  T2 instances provide a baseline level of CPU performance with the ability to burst to a higher level when required by your workload. A T2 Unlimited instance can sustain high CPU performance for any period of time whenever required. For more information, see T2 Instances. 
  
  T2 instances are well-suited for the following applications:
  * Websites and web applications
  * Code repositories
  * Development, build, test, and staging environments
  * Microservices
  * Running backend servers for SAP, Microsoft SharePoint, cluster computing, and other enterprise applications

#### **Compute optimized**(examples : c4.large)
    
Compute optimized instances are ideal for compute-bound applications that benefit from high-performance processors. 

They are well suited for the following applications:    
* Batch processing workloads    
* High-performance web servers    
* High-performance computing (HPC)    
* Scientific modeling    
* Machine learning inference
    
#### **Memory optimized**(examples : r4.large , x1e.16xlarge , z1d.12xlarge)

Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.

* R4, R5, and R5d Instances

    These instances are well suited for the following applications:
    * High-performance, relational (MySQL) and NoSQL (MongoDB, Cassandra) databases.
    * Distributed web scale cache stores that provide in-memory caching of key-value type data (Memcached and Redis).
    * In-memory databases using optimized data storage formats and analytics for business intelligence (for example, SAP HANA).


* X1 Instances

    These instances are well suited for the following applications:

    * In-memory databases such as SAP HANA, including SAP-certified support for Business Suite S/4HANA, Business Suite on HANA (SoH), Business Warehouse on HANA (BW), and Data Mart Solutions on HANA. For more information, see SAP HANA on the AWS Cloud.
    * Big-data processing engines such as **Apache Spark or Presto**.
    * High-performance computing (HPC) applications.


* z1d Instances

    These instances deliver both high compute and high memory and are well-suited for the following applications:

    * Relational database workloads

#### **Storage optimized**(examples : d2.xlarge , h1.2xlarge , i3.large)
    
Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to application

D2 and H1 instances suited for: 
* Massive parallel processing (MPP) data warehouse
* MapReduce and Hadoop distributed computing
* Log or data processing applications

#### **Accelerated computing**(examples :  f1.16xlarge , g3.4xlarge , p2.xlarge)

If you require high processing capability, you'll benefit from using accelerated computing instances, which provide access to hardware-based compute accelerators such as Graphics Processing Units (GPUs) or Field Programmable Gate Arrays (FPGAs). Accelerated computing instances enable more parallelism for higher throughput on compute-intensive workloads.


### Instance Purchasing Options

#### Purchasing types: 
* On-Demand Instances -- Pay, by the second, for the instances that you launch.
  
* Reserved Instances -- Purchase, at a significant discount, instances that are always available, for a term from one to three years.

  Payment option: No Upfront, Partial Upfront, or All Upfront.
  
  Term: One-year or three-year. A year is defined as 31536000 seconds (365 days). Three years is defined as 94608000 seconds (1095 days).
  
  Offering class: Convertible or Standard.
  
  If you require a capacity reservation on a continuous basis, Reserved Instances might meet your needs and decrease costs.

  
* Scheduled Instances -- Purchase instances that are always available on the specified recurring schedule, for a one-year term.

  Scheduled Instances are a good choice for workloads that do not run continuously, but do run on a regular schedule. For example, you can use Scheduled Instances for an application that runs during business hours or for batch processing that runs at the end of the week.

* Spot Instances -- Request unused EC2 instances, which can lower your Amazon EC2 costs significantly.
    
    If you are flexible about when your instances run, Spot Instances might meet your needs and decrease costs.
   
   Amazon EC2 sets aside pools of EC2 instances in each Availability Zone for use as Scheduled Instances. Each pool supports a specific combination of instance type, operating system, and network (EC2-Classic or EC2-VPC).

    Spot Instance pool – A set of unused EC2 instances with the same instance type, operating system, Availability Zone, and network platform (EC2-Classic or EC2-VPC).
    
    Spot price – The current price of a Spot Instance per hour.
    
    Spot Instance request – Provides the maximum price per hour that you are willing to pay for a Spot Instance. If you don't specify a maximum price, the default maximum price is the On-Demand price. When the maximum price per hour for your request exceeds the Spot price, Amazon EC2 fulfills your request if capacity is available. A Spot Instance request is either one-time or persistent. Amazon EC2 automatically resubmits a persistent Spot request after the Spot Instance associated with the request is terminated. Your Spot Instance request can optionally specify a duration for the Spot Instances.

* Dedicated Hosts -- Pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.

    An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing per-socket, per-core, or per-VM software licenses, including Windows Server, Microsoft SQL Server, SUSE, Linux Enterprise Server, and so on.
    
    Difference between Dedicated host and Dedicated Instance : 
    
    |Topic|Dedicated Host|Dedicated Instance|
    |------|-------|----|
    |Billing|Per-host billing|Per-instance billing
    |Visibility of sockets, cores, and host ID|Provides visibility of the number of sockets and physical cores|No visibility
    |Host and instance affinity|Allows you to consistently deploy your instances to the same physical server over time|Not supported
    |Targeted instance placement|Provides additional visibility and control over how instances are placed on a physical server|Not supported
    |Automatic instance recovery|Not supported|Supported
    |Bring Your Own License (BYOL) |Supported |Not supported

* Dedicated Instances -- Pay, by the hour, for instances that run on single-tenant hardware.

    Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at the hardware level. In addition, Dedicated Instances that belong to AWS accounts that are linked to a single payer account are also physically isolated at the hardware level. However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.
       
    | Tenancy 	| Description |
    |-----------|-------------|
    |default  | Your instance runs on shared hardware.|
    |dedicated     |  Your instance runs on single-tenant hardware.|
    |host| Your instance runs on a Dedicated Host, which is an isolated server with configurations that you can control.|
    
    After you launch an instance: 
    * You cannot change the tenancy of an instance from default TO dedicated or host
    * You cannot change the tenancy of an instance from dedicated or host TO default after you've launched it.

    
Each instance that you launch into a VPC has a tenancy attribute. This attribute has the following values.

### Inctance lifecyle

![Instance status flow][https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/instance_lifecycle.png]

Notice that you can't stop and start an instance store-backed instance.

Any status except Running, are not billed

When instance is stopped(=> ebs-backed), Aws take money only for EBS volumes

After stopping, starting, rebooting instance (EBS-backed) IPv4 retains.

If you enable termination protection, you can't terminate the instance using the console, CLI, or API.

An instance **reboot** is equivalent to an operating system reboot. In most cases, it takes only a few minutes to reboot your instance. When you reboot an instance, it remains on the same physical host, so your instance keeps its public DNS name (IPv4), private IPv4 address, IPv6 address (if applicable), and any data on its instance store volumes.

### Placement groups
Determines how instances are placed on underlying hardware.
#### Cluster Plaement Group
A cluster placement group is a logical grouping of instances within a single Availability Zone.
Cluster placement groups are recommended for applications that benefit from low network latency, high network throughput, or both, and if the majority of the network traffic is between the instances in the group.
#### Spread Placement Groups
A spread placement group is a group of instances that are each placed on distinct underlying hardware.

Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other. Launching instances in a spread placement group reduces the risk of simultaneous failures that might occur when instances share the same underlying hardware. Spread placement groups provide access to distinct hardware, and are therefore suitable for mixing instance types or launching instances over time.

A spread placement group can span multiple Availability Zones, and you can have a maximum of seven running instances per Availability Zone per group.

-----

## EBS

###EBS Volumes

An Amazon EBS volume is a durable, block-level storage device that you can attach to a single EC2 instance. 

By default, Amazon EBS-backed instance root volumes have the DeleteOnTermination flag set to true.

You can restore an Amazon EBS volume with data from a snapshot stored in Amazon S3. You need to know the ID of the snapshot you want to restore your volume from and you need to have access permissions for the snapshot.

EBS volumes that are restored from encrypted snapshots are automatically encrypted.
 
New EBS volumes receive their maximum performance the moment that they are available and do not require initialization (formerly known as pre-warming). 

EBS volumes replicated within the Availability Zone

You can detach an Amazon EBS volume from an instance explicitly or by terminating the instance. However, if the instance is running, you must first unmount the volume from the instance.

If an EBS volume is the root device of an instance, you must stop the instance before you can detach the volume.

#### Volume mapping 

After you create a volume, you can attach it to any EC2 instance in the same Availability Zone.

You can detach an Amazon EBS volume from an instance explicitly or by terminating the instance. However, if the instance is running, you must first unmount the volume from the instance.

If an EBS volume is the root device of an instance, you must stop the instance before you can detach the volume.

You can reattach a volume that you detached (without unmounting it), but it might not get the same mount point and the data on the volume might be out of sync if there were writes to the volume in progress when it was detached.

* Show list of disks with status, size, mountpoint: 
         
         lsblk
* Check whether disk have filesystem: 
    
         file -s /dev/xvd* 
         
* Create file system ext4: 
        
         mkfs -t ext4  /dev/xvd*

*  Mount disk to /my/mountpoint/path. 
   After that **lsblk** will show /my/mountpoint/path as mountpoint
   
         mount /dev/xvd* /my/mountpoint/path
* Unmount given disk:

         umount -d /dev/xvd* 

#### Limits 

Limit for number of attached volumes is 40 for Linux and about (16 or 26) for Windows ec2is

Amazon EBS currently supports a maximum volume size of 16 TiB

####EBS benefits : 
 * Data availability : automatically replicated within that zone to prevent data loss due to failure of any single hardware component within Availability Zone. 
 * Data persistence : Data in save even if you stop-start-reboot-terminate instance to which volume is attached
 * Data encryption : For simplified data encryption, you can create encrypted EBS volumes with the Amazon EBS encryption feature. All EBS volume types support encryption. 
 * Snapshots : When you create a new volume from a snapshot, it's an exact copy of the original volume at the time the snapshot was taken. EBS volumes that are restored from encrypted snapshots are automatically encrypted. By optionally specifying a different Availability Zone, you can use this functionality to create a duplicate volume in that zone. The snapshots can be shared with specific AWS accounts or made public. When you create snapshots, you incur charges in Amazon S3 based on the volume's total size. For a successive snapshot of the volume, you are only charged for any additional data beyond the volume's original size.
               Snapshots are incremental backups, meaning that only the blocks on the volume that have changed after your most recent snapshot are saved. If you have a volume with 100 GiB of data, but only 5 GiB of data have changed since your last snapshot, only the 5 GiB of modified data is written to Amazon S3. Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the volume. Snapshots stored in S3
 * Flexibility : EBS volumes support live configuration changes while in production. You can modify volume type, volume size, and IOPS capacity without service interruptions.


#### EBS Volume states

#### EBS Troubleshooting

Process can be used to recover non-working boot volume:
* Detach volume
* Attach to healthy instance as non-boot volume
* Fix issue in files
* Reattach to original instance
* Restart original instance

Volume cant be attached to ec2i, maybe causes are :
* Limit - volumes you can attach to your instance. (about 40 for linux and up to 26 for Win)
  
* If a volume is encrypted, it can only be attached to an instance that supports Amazon EBS encryption. For more information, see Supported Instance Types.
  
* If a volume has an AWS Marketplace product code:
  * The volume can only be attached to a stopped instance.
  * You must be subscribed to the AWS Marketplace code that is on the volume.
  

![EBS Volume lifecycle][https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/images/state_diagram_ebs.png]

#### EBS Volumes types

*  Solid-State Drives (SSD)
* 	Hard disk Drives (HDD)

|     | SSD | SSD | HDD | HDD |
|-----|-----|-----|-----|-----|
|Volume Type	|General Purpose SSD (gp2)* |	Provisioned IOPS SSD (io1)|	Throughput Optimized HDD (st1)|	Cold HDD (sc1)|
|Description|General purpose SSD volume that balances price and performance for a wide variety of workloads	|Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads |Low cost HDD volume designed for frequently accessed, throughput-intensive workloads|	Lowest cost HDD volume designed for less frequently accessed workloads|
|Use Cases	|Recommended for most workloadsSystem boot volumes, Low-latency interactive apps, Development and test environments|Critical business applications that require sustained IOPS performance, or more than 10,000 IOPS or 160 MiB/s of throughput per volume(e.g. MongoDB, Cassandra, Microsoft SQL Server) | Fast throughput at a low price( Big data, Data warehouses, Log processing, **Cannot be a boot volume**)  | Large volumes of data that is **infrequently** accessed(lowest storage cost is important, **Cannot be a boot volume**) |
|Volume Size|	1 GiB - 16 TiB	|4 GiB - 16 TiB|	500 GiB - 16 TiB	|500 GiB - 16 TiB|
|Max. IOPS**/Volume	|10,000	|32,000***	|500|	250|

#### EBS Volume Monitoring (CloudWatch metrics)
* VolumeReadBytes and VolumeWriteBytes : Bytes

  Provides information on the I/O operations in a specified period of time.
* VolumeReadOps, VolumeWriteOps : Count
  
  The total number of I/O operations in a specified period of time.
* VolumeTotalReadTime, VolumeTotalWriteTime : Seconds
  
  The total number of seconds spent by all operations that completed in a specified period of time. If multiple requests are submitted at the same time, this total could be greater than the length of the period. For example, for a period of 5 minutes (300 seconds): if 700 operations completed during that period, and each operation took 1 second, the value would be 700 seconds.
* VolumeIdleTime : Seconds
  
  The total number of seconds in a specified period of time when no read or write operations were submitted.
* VolumeQueueLength : Count

  The number of read and write operation requests waiting to be completed in a specified period of time.
* VolumeThroughputPercentage : Percent

  Used with Provisioned IOPS SSD volumes only. The percentage of I/O operations per second (IOPS) delivered of the total IOPS provisioned for an Amazon EBS volume. Provisioned IOPS SSD volumes deliver within 10 percent of the provisioned IOPS performance 99.9 percent of the time over a given year.


###EBS Snapshots

You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved. This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data. When you delete a snapshot, only the data unique to that snapshot is removed. Each snapshot contains all of the information needed to restore your data (from the moment when the snapshot was taken) to a new EBS volume.

When you create an EBS volume based on a snapshot, the new volume begins as an exact replica of the original volume that was used to create the snapshot. The replicated volume loads data lazily in the background so that you can begin using it immediately. If you access data that hasn't been loaded yet, the volume immediately downloads the requested data from Amazon S3, and then continues loading the rest of the volume's data in the background.

Deleting a snapshot of a volume has no effect on the volume. Deleting a volume has no effect on the snapshots made from it.

EBS snapshots broadly support EBS encryption:
* Snapshots of encrypted volumes are automatically encrypted.
* Volumes that are created from encrypted snapshots are automatically encrypted.
* When you copy an unencrypted snapshot that you own, you can encrypt it during the copy process.
* When you copy an encrypted snapshot that you own, you can reencrypt it with a different key during the copy process.

Although you can delete a snapshot that is still in progress, the snapshot must complete before the deletion takes effect. This may take a long time. If you are also at your concurrent snapshot limit (five snapshots in progress), and you attempt to take an additional snapshot, you may get the ConcurrentSnapshotLimitExceeded error.

###EBS Encryption

Amazon EBS encryption offers a simple encryption solution for your EBS volumes without the need to build, maintain, and secure your own key management infrastructure. When you create an encrypted EBS volume and attach it to a supported instance type, 
the following types of data are encrypted:
* Data at rest inside the volume
* All data moving between the volume and the instance
* All snapshots created from the volume
* All volumes created from those snapshots

EBS encrypts your volume with a data key using the **industry-standard AES-256**(AES-256-XTS) algorithm.

Amazon EBS encryption uses AWS Key Management Service (AWS KMS) customer master keys (CMKs) when creating encrypted volumes and any snapshots created from them. A unique AWS-managed CMK is created for you automatically in each region where you store AWS assets. This key is used for Amazon EBS encryption unless you specify a customer-managed CMK that you created separately using AWS KMS.

You cannot change the CMK that is associated with an existing snapshot or encrypted volume. However, you can associate a different CMK during a snapshot copy operation so that the resulting copied snapshot uses the new CMK.

Because of security constraints, you cannot directly restore an EBS volume from a shared encrypted snapshot that you do not own. You must first create a copy of the snapshot, which you will own.

To migrate data from unencrypted volume to encrypted volume you can: 
* Attach unencrypted and encrypted volumes to certain ec2i
* use command **dd** to copy from unencrypted(**/dev/xdf**) to encrypted(**/dev/xvdg**) volume:
     
     
      dd if/dev/xdf of=/dev/xvdg bs=64K conv=noerror,sync



#### How EBS use KMS? 
The following explains how Amazon EBS uses your CMK:
* When you create an encrypted EBS volume, Amazon EBS sends a **GenerateDataKeyWithoutPlaintext** request to AWS KMS, specifying the CMK that you chose for EBS volume encryption.
* AWS KMS generates a new data key, encrypts it under the specified CMK, and then sends the encrypted data key to Amazon EBS to store with the volume metadata.
* When you attach the encrypted volume to an EC2 instance, Amazon EC2 sends the encrypted data key to AWS KMS with a Decrypt request.
* AWS KMS decrypts the encrypted data key and then sends the decrypted (plaintext) data key to Amazon EC2.
* Amazon EC2 uses the plaintext data key in hypervisor memory to encrypt disk I/O to the EBS volume. The data key persists in memory as long as the EBS volume is attached to the EC2 instance.

###EBS Performance
EBS volumes created from EBS snapshots must be initialized. &quot;Initialized&quot; occures the first time a storage block on the volume is read - and the performance impact can be implaced by up to 50%

You can avoid this performance hit in a production environment by reading from all of the blocks on your volume before you use it; this process is called initialization. For a new volume created from a snapshot, you should read all the blocks that have data before using the volume.
    
#### IOPS
     
IOPS are a unit of measure representing input/output operations per second. The operations are measured in KiB, and the underlying drive technology determines the maximum amount of data that a volume type counts as a single I/O. I/O size is capped at 256 KiB for SSD volumes and 1,024 KiB for HDD volumes because SSD volumes handle small or random I/O much more efficiently than HDD volumes.

#### Amazon EBS Performance Tips
* Use EBS-Optimized Instances
* Apply pre-warming
* else

### Root device volume
Each instance that you launch has an associated root device volume, either an Amazon EBS volume or an instance store volume.

You can use block device mapping to specify additional EBS volumes or instance store volumes to attach to an instance when it's launched. You can also attach additional EBS volumes to a running instance; see Attaching an Amazon EBS Volume to an Instance. However, the only way to attach instance store volumes to an instance is to use block device mapping to attach them as the instance is launched.

Root device volume types: Instance store and EBS-backed store

#### Instance store volume 

An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type. While an instance store is dedicated to a particular instance, the disk subsystem is shared among instances on a host computer.


You can specify instance store volumes for an instance only when you launch it. You can't detach an instance store volume from one instance and attach it to a different instance.

The data in an instance store persists only during the lifetime of its associated instance. 
If an instance reboots (intentionally or unintentionally), data in the instance store persists. 

However, data in the instance store is lost under any of the following circumstances:

 * The underlying disk drive fails

 * The instance stops

 * The instance terminates


Therefore, do not rely on instance store for valuable, long-term data. Instead, use more durable data storage, such as Amazon S3, Amazon EBS, or Amazon EFS.

With AMIs backed by instance store, you're charged for instance usage and storing your AMI in Amazon S3. With AMIs backed by Amazon EBS, you're charged for instance usage, Amazon EBS volume storage and usage, and storing your AMI as an Amazon EBS snapshot.

#### EBS volumes - SEPARATE SECTION -> BELOW ...

#### How to encrypt root volume? 
1. You have to create snapshot of your root volume. 
2. Then create a copy of volume with option - encrypt. 
3. Then create AMI from encrypted copied root volume. 
4. Then create EC2 inctance from this AMI(have to use larger machines)

-------

##EC2 scope Troubleshooting

### EC2 Troubleshooting

#### Instance launch common errors

* InstanceLimitExceeded
  
  You have reached the limit on the number of instances that you can launch in a region.

* InsufficientInstanceCapacity 

  AWS does not currently have enough available On-Demand capacity to service your request.

* Instance from Pending ---> Terminated 
  
  Problem with volumes (corrupted snapshot, rich EBS limit, no permissions to encrypted volume)

#### Connection to ec2i

* Connection timeout 
  
  Check Security groups
  
* Access denied (public key) 
  
  Write right username before @
  
* Error: Unprotected Private Key File

  Use chmod 
        
        [ec2-user ~]$ chmod 0400 .ssh/my_private_key.pem
        
#### Instance stuck in Stopping state

You are not charged when instance not in Running state. 

Out can use force stop command :
 
        aws ec2 stop-instances --instance-ids i-0123ab456c789d01e --force

















# Unsorted 

* 
* A security groups must be assigned to an instance during the creation process
* Each instance must be placed in certain VPC, subnet, availability zone
