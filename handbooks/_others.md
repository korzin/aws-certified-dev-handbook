
## CloudFront

## Random facts about CloudFront
134 Points of Presence (123 Edge Locations and 11 Regional Edge Caches


You can clear cache objects before the TTL but you will be charged for this.
 You may choose to do so if your TTL is set for a long duration and you need 
 to distribute an immediate update of your content.

By default, objects stay in edge locations for 24 hours before expiry. You can specify settings for Minimum TTL, 
Maximum TTL and Default TTL. Note that you control cache duration of individual objects too. Cache-Control Max-age
 specifies how long you want the object to remain in cache before CloudFront will fetch the object again from the 
 origin server. The minimum expiration time CloudFront supports is 0 seconds for web distribution and 3600 seconds 
 for RTMP distributions. The maximum value is 100 years.

Because you cannot stream Adobe Flash multimedia content over HTTP or HTTPS, you must 
use RTMP distribution. RTMP can stream media files using Adobe Media Server using the
 Adobe Real-Time Messaging Protocol (RTMP). In addition, the source content must be an 
 Amazon S3 bucket.

## Choosing Between Signed URLs and Signed Cookies
CloudFront signed URLs and signed cookies provide the same basic functionality: they allow you to control who can access your content. If you want to serve private content through CloudFront and you're trying to decide whether to use signed URLs or signed cookies, consider the following.

Use signed URLs in the following cases:

You want to use an RTMP distribution. Signed cookies aren't supported for RTMP distributions.

You want to restrict access to individual files, for example, an installation download for your application.

Your users are using a client (for example, a custom HTTP client) that doesn't support cookies.

Use signed cookies in the following cases:

You want to provide access to multiple restricted files, for example, all of the files for a video in HLS format or all of the files in the subscribers' area of a website.

You don't want to change your current URLs.

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

Snowball has 10Gbps network interfaces with RJ45, SFP+ copper, and SFP+ optical network ports

### Key Features

* Encryption
  
  All data transferred to Snowball is automatically encrypted with 256-bit encryption keys 
* Tamper Resistant

  The Snowball device is equipped with tamper-resistant seals and includes a built-in
   Trusted Platform Module (TPM) that uses a dedicated processor designed to detect any
    unauthorized modifications to the hardware, firmware, or software. AWS inspects every 
    device for any signs of tampering and to verify that no changes were detected by the TPM.

* End-to-End Tracking - no description
### Use cases 

* CLOUD MIGRATION
   
   If you have large quantities of data you need to migrate into AWS, Snowball is often much faster and more cost-effective than transferring that data over the Internet.
* DISASTER RECOVERY
   
   In the event that you need to quickly retrieve a large quantity of data stored in Amazon S3, Snowball devices can help retrieve the data much quicker than high-speed Internet.
* DATACENTER DECOMMISSION
   
   There are many steps involved to decommissioning a datacenter to make sure valuable data is not lost. Snowball can help ensure that your data is securely and cost-effectively transferred to AWS during this process.
* CONTENT DISTRIBUTION
   
   Use Snowball devices if you regularly receive or need to share large amounts of data with clients, customers, or business associates. Snowball devices can be sent directly from AWS to client or customer locations.

### Remember 

Job manifest unlock code is a 25-character code to unlock the job manifest file.


## Elastic File System (EFS) 

The storage capacity will increase and decrease as you add or remove files

Benefits of EFS: 
* Can be accessed by multiple EC2I at the same time, 
* Multiple EC2i can access same data, 
* Can be mounted to on-premise servers(see AWS Direct Connect) , 
* Allow migrate data to and from on-premise servers, 
* Can scale on peta-bytes in size, maintaining law latency, 
* Only pay for what you use

## API Gateway 

Host names APIs in API Gateway, which are deployed to a specific
region and of the {rest-api-id}.execute-api.{region}.amazonaws.com format.
  

