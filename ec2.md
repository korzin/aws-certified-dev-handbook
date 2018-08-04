#EC2 Scope

## EC2 Service

### Instance Purchasing Options


#### Types: 
* On-Demand Instances -- Pay, by the second, for the instances that you launch.

  ddf
  
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










## EBS
    
#### Block mapping 
    
    
You can use block device mapping to specify additional EBS volumes or instance store volumes to attach to an instance when it's launched. You can also attach additional EBS volumes to a running instance; see Attaching an Amazon EBS Volume to an Instance. However, the only way to attach instance store volumes to an instance is to use block device mapping to attach them as the instance is launched.

### Root device volume
Each instance that you launch has an associated root device volume, either an Amazon EBS volume or an instance store volume.

Root device volume types: Instance store and EBS-backed store

#### Instance store volume 

An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type. While an instance store is dedicated to a particular instance, the disk subsystem is shared among instances on a host computer.



# Unsorted 

* An EC2 instance can only ONE role attached at a time
* A security groups must be assigned to an instance during the creation process
* Each instance must be placed in certain VPC, subnet, availability zone
