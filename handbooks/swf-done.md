# SWF

In addition to a core SDK that calls service APIs, Amazon SWF provides the AWS Flow Framework with which you can write distributed applications using programming constructs that structure asynchronous interactions.

Workflow have a state. When state is changed then decider can determine next activity to perform.

## Workflow-s

Using the Amazon Simple Workflow Service (Amazon SWF), you can implement
 distributed, asynchronous applications as workflows. Workflows coordinate
  and manage the execution of activities that can be run asynchronously across 
  multiple computing devices and that can feature both sequential and parallel 
  processing.

## Workflow history

The progress of every workflow execution is recorded in its workflow history, 
which Amazon SWF maintains. The workflow history is a detailed, complete, and 
consistent record of every event that occurred since the workflow execution started.

The workflow history has several key benefits:

* It enables applications to be stateless, because all information about a workflow execution is stored in its workflow history.

* For each workflow execution, the history provides a record of which activities were scheduled, their current status, and their results. The workflow execution uses this information to determine next steps.

* The history provides a detailed audit trail that you can use to monitor running workflow executions and verify completed workflow executions.

## Actors

* Workflow Starters

  A workflow starter is any application that can initiate workflow executions.
   In the e-commerce example, one workflow starter could be the website at
    which the customer places an order. 

* Deciders

  A decider is an implementation of a workflow's coordination logic. Deciders control the flow of activity tasks in a workflow execution. Whenever a change occurs during a workflow execution, such as the completion of a task, a decision task including the entire workflow history will be passed to a decider. 

* Activity Workers

  An activity worker is a process or thread that performs the activity tasks that are part of your workflow. The activity task represents one of the tasks that you identified in your application.

## Tasks 

Amazon SWF interacts with activity workers and deciders by providing them with work assignments known as tasks. There are three types of tasks in Amazon SWF:

* Activity task 
  
  An Activity task tells an activity worker to perform its function, such as to
   check inventory or charge a credit card. The activity task contains all the
    information that the activity worker needs to perform its function.

* Lambda task
  
  A Lambda task is similar to an Activity task, but executes a Lambda function 
  instead of a traditional Amazon SWF activity. For more information about how
   to define a Lambda task, see AWS Lambda Tasks.

* Decision task 
  
  A Decision task tells a decider that the state of the workflow execution has
   changed so that the decider can determine the next activity that needs to be 
   performed. The decision task contains the current workflow history.
   
   
## Amazon SWF Domains
Domains provide a way of scoping Amazon SWF resources within your AWS account. All the components of a workflow, such as the workflow type and activity types, must be specified to be in a domain.


## SWF FAQ

#### When should I use Amazon SWF vs. AWS Step Functions?

AWS Step Functions is a fully managed service that makes it easy to coordinate
the components of distributed applications and microservices using visual
workflows. Instead of writing a Decider program, you define state machines
in JSON. AWS customers should consider using Step Functions for new
applications. If Step Functions does not fit your needs, then you should 
consider Amazon Simple Workflow (SWF).

## AWS Flow Framework
The AWS Flow Framework is an enhanced SDK for writing distributed, asynchronous programs that can run as workflows 
on Amazon SWF. It is available for the Java and Ruby programming languages, and it provides classes that simplify 
writing complex distributed programs.

## SWF Limits 

SWF retention: 1 year  
SWF Domain: 100 per account (containers for segregating app resources)  
SWF Workflow/activity: 10,000  
SWF Request size: 1MB  
SWF Open: 1000

## SWF API

#### Activity workers API

PollForActivityTask

RespondActivityTaskCompleted

RespondActivityTaskFailed

RespondActivityTaskCanceled

RecordActivityTaskHeartbeat

#### Deciders API

PollForDecisionTask

RespondDecisionTaskCompleted

#### Workflow execution API

RequestCancelWorkflowExecution

StartWorkflowExecution

SignalWorkflowExecution

TerminateWorkflowExecution

#### Visibility actions API

Activity Visibility

ListActivityTypes

DescribeActivityType