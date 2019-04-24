# Bots & Assistants

## Bots

Bots are designed for doing small and mundane tasks like mutations, for example, or in instances where we are moving data from one place to another, for housekeeping purposes. Activities like this aren't typically very interesting to a user, and so in many cases a Bot's actions may not even be need to be initiated by a user. 

### Loosely Coordinating Services

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVdnxVOMd0zDJQAgSCd%2F-LWJAwRVXZ47tMS7kZag%2F-LWJEdCQNM5ctwdhqbGp%2Fimage.png?alt=media&token=dd6385ec-2364-49d7-b7f9-7ef1e6ad2ce6)

![Example Screen](../../../.gitbook/assets/image%20%2890%29.png)

## Assistants

On Maana Q, you can think of Assistants as a UI for interacting with individual Bots. Some Bots will have Assistants, and/or will need an input from an Assistant before the Bot can run.  

Some of our Assistants can be very useful in extracting information from data and using that information to enrich the Knowledge Graph.  The Field Classification Assistant below is a good example of this.

### Concepts for Assistants

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVdnxVOMd0zDJQAgSCd%2F-LWJAwRVXZ47tMS7kZag%2F-LWJEylHHAzBtucZb2BT%2Fimage.png?alt=media&token=97893772-1830-4faf-8830-e6f566704b4e)

### Field Classification Assistant

The field classification assistant allows users to accept or ignore Types suggestions from the field classification Bot.  A user may add a new field for all instances, or add a new field for only matching instances.

#### For example:

* 92% of instances of Phone\_Number field below has been identified as Type Phone
* ~8% have been identified as NULL

![Example Screen](../../../.gitbook/assets/image%20%282%29.png)

## Future Assistants in the Pipeline

### Link Browsing across and within Kinds:

* Which Kinds in the system are related?
* Which Instances in a Kind are related to other instances or Kinds?

### Entity Recognition and Training:

* Train entities, classify Kind instances, browser related Entities, allow creation of links.

### Meta-Learning:

* AutoML-like train/predict flow.

