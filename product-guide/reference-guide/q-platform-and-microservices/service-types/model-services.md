# Model Services

### @TODO: Explanation of What is a Model Service and where along the service development it fits



### Additional Considerations: 

### Referencing Empty Kinds

Note that if an Outer Kind contains references to Inner Kind Ids that do not actually exist \(i.e. the Inner Kinds are empty\), running `allOuterKinds` will produce a `Null` in the field corresponding to the missing InnerKind. For Example: 

![There are 3 instances of q. q3 does not exist](../../../../.gitbook/assets/image%20%2893%29.png)

![Instance k1 of kind k references a q with id q3.](../../../../.gitbook/assets/image%20%2815%29.png)

![A NULL occupies the spot of the empty q3](../../../../.gitbook/assets/image%20%289%29.png)

Keep this in mind when your functions potentially may reference deleted or empty kinds. 

