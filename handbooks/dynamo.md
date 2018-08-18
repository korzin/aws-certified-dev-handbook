
## DynamoDB definition



## Primary key TODO 

Each primary key attribute must be defined as type string, number, or binary.

The following additional constraints apply to primary key attributes that
 are defined as type **STRING**s:

* For a simple primary key, the maximum length of the first attribute value
 (the partition key) is 2048 bytes.

* For a composite primary key, the maximum length of the second attribute value
 (the sort key) is 1024 bytes.

## Provisioned throughput TODO add info for calculations 


## Limits 

#### Provisioned throughput limits

Minimum settings for provisioned throughput are 1 read capacity unit and 1 write capacity unit.

| Region | Reads/Writes | per |
|---------|--------------|--------|
|N. Virginia | 40k        | table |
|N. Virginia | 80k      | account|
|Other reg.| 10k      | table |
|Other reg. | 20k    | account |

The provisioned throughput limit includes the sum of the capacity of the table together with the capacity of all of its global secondary indexes.

#### Table size limits
There is no practical limit on a table's size
#### Table limits
256 tables per region. You can request service limit increase in support
#### Table names
3 < tableName < 255
#### Attribute name
1 < attributeName < 64kb
####  Secondary Indexes limits
You can define a maximum of 5 local secondary indexes and 5 global secondary indexes per table.
#### Partition and sort Key Lengths
The minimum length of a partition and sort key value is 1 byte. 

The maximum length is 2048 bytes for partition key and 1024 for sort key.

#### API Limits 

* CRUD: 
  
  In general, you can have up to 10 CreateTable, UpdateTable, and DeleteTable requests running simultaneously (in any combination). 

* BatchGetItem
  
  A single BatchGetItem operation can retrieve a maximum of 100 items. The total size of all the items retrieved cannot exceed 16 MB.

* BatchWriteItem
  
  A single BatchWriteItem operation can contain up to 25 PutItem or DeleteItem requests. The total size of all the items written cannot exceed 16 MB.

* DescribeLimits

  DescribeLimits should only be called periodically. You can expect throttling errors if you call it more than once in a minute.

* Query
    
  The result set from a Query is limited to 1 MB per call. You can use the LastEvaluatedKey from the query response to retrieve more results.

* Scan
  
  The result set from a Scan is limited to 1 MB per call. You can use the LastEvaluatedKey from the scan response to retrieve more results.






## Tables 

 You can also use the UpdateTable operation to manually adjust your table's throughput capacity
 

### CreateTable API call

Use the CreateTable operation to create a table.
You must provide the following information: 
* Table name (unique in account and region)
* Primary key (if key is composite, specify which is HASH(partitionKey),
  which is RANGE(sortKey))
* Throughput settings (read and write throughput)

**Example of creating table**: 
    
    aws dynamodb create-table \
        --table-name Music \
        --attribute-definitions \
            AttributeName=Artist,AttributeType=S \
            AttributeName=SongTitle,AttributeType=S \
        --key-schema \
            AttributeName=Artist,KeyType=HASH \
            AttributeName=SongTitle,KeyType=RANGE \
        --provisioned-throughput \
            ReadCapacityUnits=10,WriteCapacityUnits=5

### UpdateTable API call

The UpdateTable operation allows you to do one of the following:

* Modify a table's provisioned throughput settings.

* Manipulate global secondary indexes on the table (see Global Secondary Indexes).

* Enable or disable DynamoDB Streams on the table

Status of tables flow while updating : 

AVAILABLE ----------> UPDATING -------------> AVAILABLE 
            (still available for queries)
## DynamoDB DataTypes

### General type groups 
DynamoDB supports many different data types for attributes within a table. They can be categorized as follows:

* Scalar Types – A scalar type can represent exactly one value. The scalar types are number, string, binary, Boolean, and null.

* Document Types – A document type can represent a complex structure with nested attributes—such as you would find in a JSON document. The document types are list and map.

* Set Types – A set type can represent multiple scalar values. The set types are string set, number set, and binary set.

#### Type descriptions 

* String
  Limits: Length must be greater than zero. Size limit of 400 KB.

* Number
  Numbers can be positive, negative, or zero. Numbers can have up to 38 digits precision. 
  In DynamoDB, numbers are represented as variable length. Leading and trailing zeroes are trimmed.
  All numbers are sent across the network to DynamoDB as strings.
  
* Binary 

  Base64-encoded 
  
  The length of a binary attribute must be greater than zero, and is constrained 
  by the maximum DynamoDB item size limit of 400 KB.

  If you define a primary key attribute as a binary type attribute, 
  the following additional constraints apply: ( JUST THE SAME AS WITH STRINGS)

  * For a simple primary key, the maximum length of the first attribute value (the partition key) is 2048 bytes.

  * For a composite primary key, the maximum length of the second attribute value (the sort key) is 1024 bytes.
    
* Boolean 

* Null

* Map (document type)
  
  Max 400kb
  
  A map is similar to a JSON object. Data structures up to 32 levels deep. 
 
* List (document type)
  
  Max 400kb
  
* Sets (Number, String, or Binary values)
 
  Each value within a set must be unique. 
  
#### Type descriptors (abbreviation in JSON)

The following is a complete list of DynamoDB data type descriptors:
* S – String
* N – Number
* B – Binary
* BOOL – Boolean
* NULL – Null
* M – Map
* L – List
* SS – String Set
* NS – Number Set
* BS – Binary Set

### Atomic Counters

You can use the UpdateItem operation to implement an atomic counter—a numeric 
attribute that is incremented, unconditionally, without interfering with other
 write requests. (All write requests are applied in the order in which they were
  received.) With an atomic counter, the updates are not idempotent. In other 
  words, the numeric value will increment each time you call UpdateItem


## API

### Quick list of some API with or without description

 Some API calls list:  
 * DescribeTable
 * ListTable
 * DescribeLimits
 * .... 

### CRUD API calls

DynamoDB provides four operations for basic create/read/update/delete (CRUD) functionality:

For each of these operations, you need to specify the entire primary key, not just part of it. 
#### PutItem – create an item. TODO description 
 

#### GetItem – read an item.  TODO description 
To read an item using GetItem, you must specify the partition key and sort key (if applicable) for that item.

With GetItem, you must specify the entire primary key, not just part of it. For example, if a table has a composite primary key (partition key and sort key), you must supply a value for the partition key and a value for the sort key.

To return the number of read capacity units consumed by GetItem, set the ReturnConsumedCapacity parameter to TOTAL.

CLI GetItem example with specifying items to return (projection-expression):
            
    aws dynamodb get-item \
        --table-name ProductCatalog \
        --key file://key.json \
        --projection-expression "Description, RelatedItems[0], ProductReviews.FiveStar"
     
#### UpdateItem – update an item.  TODO description 

#### DeleteItem – delete an item.  TODO description 

### Other API calls (Not less important) TODO other calls

In addition to the four basic CRUD operations, DynamoDB also provides the following:

Using these operations can reduce the number of network round trips from your 
application to DynamoDB. In addition, DynamoDB performs the individual read or
 write operations in parallel. 
 
These batch operations combine multiple CRUD operations into a single request.
 In addition, the batch operations read and write items in parallel to minimize
  response latencies.
  
#### BatchGetItem 
Read up to 100 items from one or more tables.

A single BatchGetItem operation can contain up to 100 individual GetItem 
requests and can retrieve up to 16 MB of data. In addition, a BatchGetItem 
operation can retrieve items from multiple tables.

####  BatchWriteItem 

Create or delete up to 25 items in one or more tables.


  
### Return Values
  In some cases, you might want DynamoDB to return certain attribute values as 
  they appeared before or after you modified them.
   The **PutItem, UpdateItem, and DeleteItem** operations have a 
   ReturnValues parameter that you can use to return the attribute 
   values before or after they are modified.
  
  The default value for ReturnValues is NONE
    
  The following are the other valid settings for ReturnValues, organized 
  by DynamoDB API operation:
  
  * PutItem
  
    ReturnValues: ALL_OLD
  
  * UpdateItem
    
    Return values: 
    * ALL_OLD
      
      Returns the entire item as it appeared before the update.
    * ALL_NEW 
      
      Returns the entire item as it appeared after the update.
    * UPDATED_OLD
  
      Returns **only the updated attributes**, as they appeared before the update.
    * UPDATED_NEW
   
      Returns **only the affected attributes**, as they appeared after the update.
  * DeleteItem
  
    ReturnValues: ALL_OLD
    
## Common Errors 


#### AccessDeniedException
You do not have sufficient access to perform this action.

HTTP Status Code: 400

#### IncompleteSignature
The request signature does not conform to AWS standards.

HTTP Status Code: 400

#### InternalFailure
The request processing has failed because of an unknown error, exception or failure.

HTTP Status Code: 500

#### InvalidAction
The action or operation requested is invalid. Verify that the action is typed correctly.

HTTP Status Code: 400

#### InvalidClientTokenId
The X.509 certificate or AWS access key ID provided does not exist in our records.

HTTP Status Code: 403

#### InvalidParameterCombination
Parameters that must not be used together were used together.

HTTP Status Code: 400

#### InvalidParameterValue
An invalid or out-of-range value was supplied for the input parameter.

HTTP Status Code: 400

#### InvalidQueryParameter
The AWS query string is malformed or does not adhere to AWS standards.

HTTP Status Code: 400

#### MalformedQueryString
The query string contains a syntax error.

HTTP Status Code: 404

#### MissingAction
The request is missing an action or a required parameter.

HTTP Status Code: 400

#### MissingAuthenticationToken
The request must contain either a valid (registered) AWS access key ID or X.509 certificate.

HTTP Status Code: 403

#### MissingParameter
A required parameter for the specified action is not supplied.

HTTP Status Code: 400

#### OptInRequired
The AWS access key ID needs a subscription for the service.

HTTP Status Code: 403

#### RequestExpired
The request reached the service more than 15 minutes after the date stamp on the request or more than 15 minutes after the request expiration date (such as for pre-signed URLs), or the date stamp on the request is more than 15 minutes in the future.

HTTP Status Code: 400

#### ServiceUnavailable
The request has failed due to a temporary failure of the server.

HTTP Status Code: 503

#### ThrottlingException
The request was denied due to request throttling.

HTTP Status Code: 400

#### ValidationError
The input fails to satisfy the constraints specified by an AWS service.

HTTP Status Code: 400
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
