# RC1-016: Catalog Service: unable to refresh schema for system service

{% tabs %}
{% tab title="Description" %}
An error should not be received for this case.
{% endtab %}

{% tab title="Repro Steps" %}
```
POST https://ci04.corp.maana.io:8443/service/io.maana.catalog/graphql HTTP/1.1
 Accept: application/json
 Content-Type: application/json
 Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IlJEUkRRamM0UWpFNU16SXpNa05GTXpNNU1qWkRORFUzUWtNNFJEaEVOelkzUWpRM09UQkZOdyJ9.eyJpc3MiOiJodHRwczovL21hYW5hLmF1dGgwLmNvbS8iLCJzdWIiOiJ4VThvWUczNldSV2dTNDZDcURUb0ZEZURpbDBMMTlUd0BjbGllbnRzIiwiYXVkIjoiaHR0cHM6Ly9oNC5tYWFuYS5pby8iLCJpYXQiOjE1NDg2NzI0ODMsImV4cCI6MTU1MTI2NDQ4MywiYXpwIjoieFU4b1lHMzZXUldnUzQ2Q3FEVG9GRGVEaWwwTDE5VHciLCJzY29wZSI6InJlYWQ6Y2xpZW50X2dyYW50cyIsImd0eSI6ImNsaWVudC1jcmVkZW50aWFscyJ9.Hc27BQuXaDLtbogrIj5GuOf-cYOO1gSy3F5hRa7CuSbbjswwZkH21FujiIJYNY8Zpss-TkRonaBJTokbU1Jl_D_cKglVk6p5UchG8DCxtYZKkUQ1QrIKjiMJpsdB-f9_RczqvqogkARofDnZVTcmmoydFB9nBUSggiPbWnGkDNP28LA7_OJhv9X5Lne3Nlx0pIXYvmYNrJFVs_B6WS5DCnWUjveY_kUefXWticAdnSLag8Jbl3SxiDB9N5kPsi0sHTjmGneQcfxhIDSH3me0mpvjVxuIj1WeZfEqZfZGRxIHe1BW69LSHSvN3TChc06PeJlw3dD-pv1yBVWZA_5usg
 Content-Length: 1734
{
 "operationName": "REFRESH_SERVICE_SCHEMA",
 "query": "mutation REFRESH_SERVICE_SCHEMA ($id: ID!) {
 refreshServiceSchema(id: $id) {
 id
 name
 description
 tags
 }}",
 "variables": {
 "id": "io.maana.entityextractor"
 }
 } 
```
{% endtab %}

{% tab title="Expected Result" %}
200 OK, no errors in response.
{% endtab %}

{% tab title="Actual Result" %}
200 OK with unexpected error message.

```
HTTP/1.1 200 OK
access-control-allow-credentials: true
access-control-expose-headers: Authorization
connection: keep-alive
content-length: 212
content-type: application/json; charset=utf-8
date: Mon, 28 Jan 2019 10:51:15 GMT
server: nginx/1.14.2
vary: Accept-Encoding
x-powered-by: Express

{"data":{"refreshServiceSchema":null},"errors":[{"message":"Cannot update 'readOnly' service. First use 'setIsReadOnly' in order to modify.","locations":[{"line":65,"column":5}],"path":["refreshServiceSchema"]}]} 

```
{% endtab %}
{% endtabs %}

