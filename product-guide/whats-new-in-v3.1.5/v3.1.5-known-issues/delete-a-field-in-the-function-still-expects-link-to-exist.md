# RC1-020: Delete a field in the function; still expects link to exist

{% tabs %}
{% tab title="Description" %}
Update function argument fails.
{% endtab %}

{% tab title="Repro Steps" %}
1. Create a function that contains 1 argument which links to the argument in the implementation function:

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXfBaozRmjhv4m21MfL%2F-LXfD_njRywaaanB5g6E%2Fimage.png?alt=media&token=2e7cf7df-29d1-4d5a-9d05-3167bd9b8061)

2. On knowledge graph, "RUN the function to make sure it works.

3. Delete the field from the function:

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LWSKjuJIsK0lFXCaEtL%2F-LXfBaozRmjhv4m21MfL%2F-LXfDe9CsCVE1_pbgZSH%2Fimage.png?alt=media&token=3e7309f7-d0cf-4e15-bb4a-eba551139ebd)
{% endtab %}

{% tab title="Expected Result" %}
Update the FG correctly.
{% endtab %}

{% tab title="Actual Result" %}
FG is not updated and expect to see the deleted argument.

ERROR:  
Unable to execute function:   
Can not find referenced argument ArgumentValue\(9bbd2be3-a4bf-4878-8e3b-fb4b911c7d4d,e1ad1c92-666c-44b1-a571-96b9c8bf7e24,None,Some\(c78ed3cf-0dde-4290-af31-4dc29a67a37f\)\) in function Function\(4e1ccb20-d521-4290-b431-678a9c3c9551,query,CKGFunctionType,fun2,List\(\),GQLString,List\(\),Service\(f717bd5d-33d5-4da1-8ad9-33ce6dad7acd,New Workspace,

[https://ci04.corp.maana.io:8443/service/f717bd5d-33d5-4da1-8ad9-33ce6dad7acd/graphql,LOGIC,None\),Some\(Implementation\(c51c9b95-7556-4562-a903-f58421d50912,Some\(539f9fea-8844-460e-b0bc-023432f190a1\),List\(ImplementationOperation\(539f9fea-8844-460e-b0bc-023432f190a1,ApplyOperationType,9c946b25-6f2e-42fc-891b-caddda2b6b41,List\(ArgumentValue\(9bbd2be3-a4bf-4878-8e3b-fb4b911c7d4d,e1ad1c92-666c-44b1-a571-96b9c8bf7e24,None,Some\(c78ed3cf-0dde-4290-af31-4dc29a67a37f](https://ci04.corp.maana.io:8443/service/f717bd5d-33d5-4da1-8ad9-33ce6dad7acd/graphql,LOGIC,None%29,Some%28Implementation%28c51c9b95-7556-4562-a903-f58421d50912,Some%28539f9fea-8844-460e-b0bc-023432f190a1%29,List%28ImplementationOperation%28539f9fea-8844-460e-b0bc-023432f190a1,ApplyOperationType,9c946b25-6f2e-42fc-891b-caddda2b6b41,List%28ArgumentValue%289bbd2be3-a4bf-4878-8e3b-fb4b911c7d4d,e1ad1c92-666c-44b1-a571-96b9c8bf7e24,None,Some%28c78ed3cf-0dde-4290-af31-4dc29a67a37f)\)\)\)\)\)\)\)\)
{% endtab %}
{% endtabs %}

