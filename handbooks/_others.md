
## CloudFront

134 Points of Presence (123 Edge Locations and 11 Regional Edge Caches


You can clear cache objects before the TTL but you will be charged for this.
 You may choose to do so if your TTL is set for a long duration and you need 
 to distribute an immediate update of your content.

### Regional edge

Regional edge caches are CloudFront locations that are deployed globally, close to your viewers. 
They're located between your origin server and the global edge locations that serve content directly to viewers. 
As objects become less popular, individual edge locations may remove those objects to make room for more popular content.
Regional edge caches have a larger cache than an individual edge location, so objects remain in the cache longer at
the nearest regional edge cache location. This helps keep more of your content closer to your viewers, reducing
the need for CloudFront to go back to your origin server, and improving overall performance for viewers.





## ElasticCache  TODO

#### TTL
    
Time to live (TTL) is an integer value that specifies the number of seconds until the key expires. 
When an application attempts to read an expired key, it is treated as though the key is not found, 
meaning that the database is queried for the key and the cache is updated. This does not guarantee 
that a value is not stale, but it keeps data from getting too stale and requires that values in the
 cache are occasionally refreshed from the database.


## Snowball

### Key Features

* Encryption
  
  All data transferred to Snowball is automatically encrypted with 256-bit encryption keys 
* Tamper Resistant

  The Snowball device is equipped with tamper-resistant seals and includes a built-in
   Trusted Platform Module (TPM) that uses a dedicated processor designed to detect any
    unauthorized modifications to the hardware, firmware, or software. AWS inspects every 
    device for any signs of tampering and to verify that no changes were detected by the TPM.

*End-to-End Tracking - no description

CLOUD MIGRATION
If you have large quantities of data you need to migrate into AWS, Snowball is often much faster and more cost-effective than transferring that data over the Internet.
DISASTER RECOVERY
In the event that you need to quickly retrieve a large quantity of data stored in Amazon S3, Snowball devices can help retrieve the data much quicker than high-speed Internet.
DATACENTER DECOMMISSION
There are many steps involved to decommissioning a datacenter to make sure valuable data is not lost. Snowball can help ensure that your data is securely and cost-effectively transferred to AWS during this process.
CONTENT DISTRIBUTION
Use Snowball devices if you regularly receive or need to share large amounts of data with clients, customers, or business associates. Snowball devices can be sent directly from AWS to client or customer locations.





