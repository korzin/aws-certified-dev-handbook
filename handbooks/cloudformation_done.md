
#CloudFormation

Number of templates  :  No limit  

Charges for AWS resources created during template instantiation apply irrespective of whether the stack could be created successfully or not.
    
Max number of Parameter: 60

Max number of stacks per region is 200

If error occur during creation of a stack, ROLLBACK_IN_PROGRESS an then ROLLBACK_COMPLETE statuses appear
## Cloud formation concepts

### Definition

AWS CloudFormation is a service that helps you model and set up your Amazon Web 
Services resources so that you can spend less time managing those resources and 
more time focusing on your applications that run in AWS. 

#### How CF is works internally

It makes a API calls to AWS services. Therefore you should have permissions to do a call.

### Some concepts

#### Templates 

An AWS CloudFormation template is a JSON or YAML formatted text file. 
You can save these files with any extension, such as **.json**, **.yaml**, 
**.template**, or **.txt**. AWS CloudFormation uses these templates as 
blueprints for building your AWS resources.

Example of template 


        {
          "AWSTemplateFormatVersion" : "2010-09-09",
          "Description" : "A sample template",
          "Resources" : {
            "MyEC2Instance" : {
              "Type" : "AWS::EC2::Instance",
              "Properties" : {
                "ImageId" : "ami-2f726546",
                "InstanceType" : "t1.micro",
                "KeyName" : "testkey",
                "BlockDeviceMappings" : [
                  {
                    "DeviceName" : "/dev/sdm",
                    "Ebs" : {
                      "VolumeType" : "io1",
                      "Iops" : "200",
                      "DeleteOnTermination" : "false",
                      "VolumeSize" : "20"
                    }
                  }
                ]
              }
            },
            "MyEIP" : {
              "Type" : "AWS::EC2::EIP",
              "Properties" : {
                "InstanceId" : {"Ref": "MyEC2Instance"}
              }
            }
          }
        }

####Stacks
When you use AWS CloudFormation, you manage related resources as a single 
unit called a stack. You create, update, and delete a collection of resources
 by creating, updating, and deleting stacks. All the resources in a stack are defined by the stack's AWS CloudFormation template. 
 
Stack waiting: WaitCondition  


####Change Sets
If you need to make changes to the running resources in a stack, you update 
the stack. Before making changes to your resources, you can generate a change 
set, which is summary of your proposed changes. Change sets allow you to see 
how your changes might impact your running resources, especially for critical 
resources, before implementing them.

For example, if you change the name of an Amazon RDS database instance, AWS 
CloudFormation will create a new database and delete the old one. You will 
lose the data in the old database unless you've already backed it up. If you 
generate a change set, you will see that your change will cause your database
 to be replaced, and you will be able to plan accordingly before you update 
 your stack. 

## Components

### Templates

Key Points:

* You can add input parameters whose values are specified when you create an AWS 
CloudFormation stack at run time.
* As and when you need to upgrade your templates, you can modify them with versioning 
capabilities to ensure that any updates/upgrades are controlled. In addition, 
you can visualise your templates as diagrams and even edit them using a drag and 
drop interface with the AWS CloudFormation Designer.
* You can deploy and update a template and its associated collection of resources 
(called a stack) by using the AWS Management Console, AWS Command Line Interface,
 or APIs. CloudFormation. CloudFormation is available free of cost, but you still 
 have to pay for the underlying resources you deploy from your template.
* CloudFormation enables you to replicate your infrastructure in multiple regions 
quickly without having to manually build out your infrastructure from scratch in
 every region. You can reuse your templates to set up your resources consistently
  and repeatedly.
  
#### Template structure

The following example shows a YAML-formatted template fragment.

        ---
        AWSTemplateFormatVersion: "version date"
        Description:
         String
        Metadata:
          template metadata
        Parameters:
          set of parameters
        Mappings:
          set of mappings
        Conditions:
          set of conditions
        Transform:
          set of transforms
        Resources:
          set of resources
        Outputs:
          set of outputs
          
**Template sections**: 
  
  Templates include several major sections. The Resources section is the 
  only required section. Some sections in a template can be in any order.
   However, as you build your template, it might be helpful to use the 
   logical ordering of the following list, as values in one section might 
   refer to values from a previous section. The list gives a brief 
   overview of each section.

* Format Version (optional)

  The AWS CloudFormation template version that the template conforms to. The template format version is not the same as the API or WSDL version. The template format version can change independently of the API and WSDL versions.

* Description (optional)
  
  A text string that describes the template. This section must always follow the template format version section.

* Metadata (optional)

  Objects that provide additional information about the template.

* Parameters (optional)
  
  Values to pass to your template at runtime (when you create or update a stack). 
  You can refer to parameters from the Resources and Outputs sections of the template.

* Mappings (optional)

  A mapping of keys and associated values that you can use to specify conditional
  parameter values, similar to a lookup table. You can match a key to a
  corresponding value by using the Fn::FindInMap intrinsic function in the 
  Resources and Outputs section.

* Conditions (optional)

  Conditions that control whether certain resources are created or whether certain resource properties are assigned a value during stack creation or update. For example, you could conditionally create a resource that depends on whether the stack is for a production or test environment.

* Transform (optional)

  For serverless applications (also referred to as Lambda-based applications), specifies the version of the AWS Serverless Application Model (AWS SAM) to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template. The model defines the syntax that you can use and how it is processed.

  You can also use AWS::Include transforms to work with template snippets that are stored separately from the main AWS CloudFormation template. You can store your snippet files in an Amazon S3 bucket and then reuse the functions across multiple templates.

* Resources **_(REQUIRED)_**
  
  Specifies the stack resources and their properties, such as an Amazon Elastic Compute Cloud instance or an Amazon Simple Storage Service bucket. You can refer to resources in the Resources and Outputs sections of the template.

* Outputs (optional)
  
  Describes the values that are returned whenever you view your stack's properties. For example, you can declare an output for an S3 bucket name and then call the aws cloudformation describe-stacks AWS CLI command to view the name.
  
### Resource section

**Logical ID** - is a name, required to reference the resource in other parts of the 
template. For example, if you want to map an Amazon Elastic Block Store volume to 
an Amazon EC2 instance, you reference the logical IDs to associate the block stores 
with the instance.

**Physical ID** - is the actual assigned name for that resource, such as an EC2 instance
 ID or an S3 bucket name. Use the physical IDs to identify resources outside 
 of AWS CloudFormation templates, but only after the resources have been created.  
  
**Resource type** - e.g. AWS::EC2::Instance 
  
**Resource properties** - e.g. for each ec2i specify an AMI ID:

Example of AMI id in JSON format:
        
        Resources:
          MyEC2Instance:
            Type: "AWS::EC2::Instance"
            Properties:
              ImageId: "ami-2f726546"
          

## Intrinsic functions 

* Fn::Base64 - get base64 encoded string
* Fn::Cidr - return array of CIDR address block. ( !Cidr [ ipBlock, count, cidrBits ] )
* Condition functions: Fn::And, Fn::Equals, Fn::If, Fn::Not, Fn::Or
* Fn::FindInMap - ( !FindInMap [ RegionMap, !Ref "AWS::Region", 32bit ] )
* Fn::GetAtt - ( !GetAtt myELB.SourceSecurityGroup.GroupName )
* Fn::GetAZs - returns an array that lists Availability Zones for a specified region
* Fn::ImportValue - (Fn::ImportValue !Sub "${NetworkStack}-SubnetID") - and this crap was exported in another stack in Output section
* Fn::Join
    
        !Join
          - ''
          - - 'arn:'
            - !Ref Partition
            - ':s3:::elasticbeanstalk-*-'
            - !Ref 'AWS::AccountId'
* Fn::Select - returns a single object from a list of objects by index. (like in java: List::get(i))
        
        !Select [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ]
* Fn::Split

        { "Fn::Split" : [ "|" , "a|b|c" ] }
* Fn::Sub - there are 2 types: with specifying what to insert, and without specifying(e.g. using AWS::StackName )

        Name: !Sub
          - www.${Domain}.${AWS::StackName}
          - { Domain: !Ref RootDomainName }

* Fn:Ref - specify logical ID, and function will return physical ID. E.g. ( { "Ref" : "logicalName" } )
          
     

## API (just to review)

CreateStack

CreateStackInstances

CreateStackSet

ListStackResources 

ListStackInstances

ListStackResources

ListStacks
 
ListStackSets

UpdateStack

DescribeStacks 

DescribeStackEvents

DescribeStackInstance

DescribeStackResource 
