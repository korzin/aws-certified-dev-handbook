
# CloudFront

134 Points of Presence (123 Edge Locations and 11 Regional Edge Caches

## Regional edge

Regional edge caches are CloudFront locations that are deployed globally, close to your viewers. 
They're located between your origin server and the global edge locations that serve content directly to viewers. 
As objects become less popular, individual edge locations may remove those objects to make room for more popular content.
Regional edge caches have a larger cache than an individual edge location, so objects remain in the cache longer at
the nearest regional edge cache location. This helps keep more of your content closer to your viewers, reducing
the need for CloudFront to go back to your origin server, and improving overall performance for viewers.





# ElasticCache  TODO

#### TTL
    
Time to live (TTL) is an integer value that specifies the number of seconds until the key expires. 
When an application attempts to read an expired key, it is treated as though the key is not found, 
meaning that the database is queried for the key and the cache is updated. This does not guarantee 
that a value is not stale, but it keeps data from getting too stale and requires that values in the
 cache are occasionally refreshed from the database.













