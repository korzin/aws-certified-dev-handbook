# Identity Access Management

## Policies

### Policy types

#### Identity-based policies 
 Attach managed and inline policies to IAM identities, such as users, groups to which users belong, and roles.
 
#### Resource-based policies 
 Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies.
 
#### Organizations SCPs 
 Use an AWS Organizations service control policy (SCP) to apply a permissions boundary to an AWS Organizations organization or organizational unit (OU).
 
#### Access control lists (ACLs) 
 Use ACLs to control what principals can access a resource. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure.

## KMS

### Definition
AWS Key Management Service (AWS KMS) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data. The master keys that you create in AWS KMS are protected by FIPS 140-2 validated cryptographic modules.

### Customer master key (CMK)

The primary resources in AWS KMS are customer master keys (CMKs). You can use a CMK
to encrypt and decrypt up to 4 kilobytes (4096 bytes) of data. Typically, you use 
CMKs to generate, encrypt, and decrypt the data keys that you use outside of AWS
KMS to encrypt your data. This strategy is known as envelope encryption.

While creating key, you have the option of providing the key policy for the new CMK.
 If you don't provide one, AWS KMS creates one for you. This default key policy has
  one policy statement that gives the AWS account (root user) that owns the CMK full 
  access to the CMK and enables IAM policies in the account to allow access to the CMK.
  
AWS KMS stores, tracks, and protects your CMKs. When you want to use a CMK, you 
access it through AWS KMS. CMKs never leave AWS KMS unencrypted. This strategy differs from data
 keys that AWS KMS returns to you, optionally in plaintext. AWS KMS does not store, manage, or track 
 your data keys.

#### CMK Types
* Customer managed CMKs are CMKs that you create, manage, and use. This includes enabling and disabling
 the CMK, rotating its cryptographic material, and establishing the IAM policies and key policies 
 that govern access to the CMK, as well as using the CMK in cryptographic operations. 
 You can allow an AWS service to use a customer managed CMK on your behalf, but you retain
  control of the CMK.

* AWS managed CMKs are CMKs in your account that are created, managed, and used on your behalf 
by an AWS service that is integrated with AWS KMS. This CMK is unique to your AWS account and 
region. Only the service that created the AWS managed CMK can use it.

 
### Data keys 

Data keys are encryption keys that you can use to encrypt data, including large amounts of data and other data encryption keys.

You can use AWS KMS customer master keys (CMKs) to generate, encrypt, and decrypt data keys. 
However, AWS KMS does not store, manage, or track your data keys, or perform cryptographic operations 
with data keys. You must use and manage data keys outside of AWS KMS.

To create a data key, call the GenerateDataKey operation. AWS KMS uses the CMK that you specify 
to generate a data key. The operation returns a plaintext copy of the data key and a copy of
 the data key encrypted under the CMK
 
 AWS KMS cannot use a data key to encrypt data, but you can use the data key outside of KMS, such as by using OpenSSL

### KMS integration with other services

#### KMS with S3

<p>Amazon S3 and AWS KMS perform the following actions when you request that your data be decrypted.</p>
<ul>
<li>Amazon S3 sends the encrypted data key to AWS KMS</li>
<li>AWS KMS decrypts the key by using the appropriate master key and sends the plaintext key back to Amazon S3</li>
<li>Amazon S3 decrypts the ciphertext and removes the plaintext data key from memory as soon as possible</li>
</ul>

If file in S3 bucket is encrypted, you are not able to view it using the
 public link. You should see a message saying 
 
     Requests specifying Server Side Encryption 
     with AWS KMS managed keys require 
     AWS Signature Version 4.

If you are uploading or accessing objects encrypted by SSE-KMS, you need to use 
**AWS Signature Version 4** for added security. Signature Version 4 is the process to 
add authentication information to AWS requests. When you use the 
AWS Command Line Interface (AWS CLI) or one of the AWS SDKs to make requests to AWS,
 these tools automatically sign the requests for you with the access key that you 
 specify when you configure the tools. When you use these tools, you don't need to
  learn how to sign requests yourself. For more information on this process read 
  this blog post: <a href="https://aws.amazon.com/blogs/security/how-to-use-the-rest-api-to-encrypt-s3-objects-by-using-aws-kms/" target="_blank">blog post</a>
  


  
  
  