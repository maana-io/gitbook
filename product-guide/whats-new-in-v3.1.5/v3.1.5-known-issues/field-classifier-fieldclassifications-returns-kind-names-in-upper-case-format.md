# Field-classifier: 'fieldClassifications' returns kind names in upper case format

{% tabs %}
{% tab title="Description" %}
Kind names should be in an appropriate format.
{% endtab %}

{% tab title="Repro Steps" %}
1. Send 'classifyFields' for 'File' kind.

```python
POST https://ci04.corp.maana.io:8443/service/io.maana.fieldclassifier/graphql HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IlJEUkRRamM0UWpFNU16SXpNa05GTXpNNU1qWkRORFUzUWtNNFJEaEVOelkzUWpRM09UQkZOdyJ9.eyJpc3MiOiJodHRwczovL21hYW5hLmF1dGgwLmNvbS8iLCJzdWIiOiJ4VThvWUczNldSV2dTNDZDcURUb0ZEZURpbDBMMTlUd0BjbGllbnRzIiwiYXVkIjoiaHR0cHM6Ly9oNC5tYWFuYS5pby8iLCJpYXQiOjE1NDg2NzI0ODMsImV4cCI6MTU1MTI2NDQ4MywiYXpwIjoieFU4b1lHMzZXUldnUzQ2Q3FEVG9GRGVEaWwwTDE5VHciLCJzY29wZSI6InJlYWQ6Y2xpZW50X2dyYW50cyIsImd0eSI6ImNsaWVudC1jcmVkZW50aWFscyJ9.Hc27BQuXaDLtbogrIj5GuOf-cYOO1gSy3F5hRa7CuSbbjswwZkH21FujiIJYNY8Zpss-TkRonaBJTokbU1Jl_D_cKglVk6p5UchG8DCxtYZKkUQ1QrIKjiMJpsdB-f9_RczqvqogkARofDnZVTcmmoydFB9nBUSggiPbWnGkDNP28LA7_OJhv9X5Lne3Nlx0pIXYvmYNrJFVs_B6WS5DCnWUjveY_kUefXWticAdnSLag8Jbl3SxiDB9N5kPsi0sHTjmGneQcfxhIDSH3me0mpvjVxuIj1WeZfEqZfZGRxIHe1BW69LSHSvN3TChc06PeJlw3dD-pv1yBVWZA_5usg
Content-Length: 862

{
  "operationName": "CLASSIFY_FIELDS",
  "query": "mutation CLASSIFY_FIELDS ($kindId: ID!){
    classifyFields (kindId: $kindId) {
        id
    }}",
  "variables": {
    "kindId": "1bc543d9-e50e-4289-9a54-59cbbd8e1b3d"
  }
} 
```

Response:

```python
HTTP/1.1 200 OK
access-control-allow-credentials: true
access-control-expose-headers: Authorization
connection: keep-alive
content-length: 73
content-type: application/json; charset=utf-8
date: Mon, 28 Jan 2019 10:48:54 GMT
server: nginx/1.14.2
vary: Accept-Encoding
x-powered-by: Express

{"data":{"classifyFields":{"id":"33205814-9e3a-44c7-9089-49a0edbdfc05"}}} 
```

2. Send 'fieldClassifications' query for 'File' kind.

```python
POST https://ci04.corp.maana.io:8443/service/io.maana.fieldclassifier/graphql HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IlJEUkRRamM0UWpFNU16SXpNa05GTXpNNU1qWkRORFUzUWtNNFJEaEVOelkzUWpRM09UQkZOdyJ9.eyJpc3MiOiJodHRwczovL21hYW5hLmF1dGgwLmNvbS8iLCJzdWIiOiJ4VThvWUczNldSV2dTNDZDcURUb0ZEZURpbDBMMTlUd0BjbGllbnRzIiwiYXVkIjoiaHR0cHM6Ly9oNC5tYWFuYS5pby8iLCJpYXQiOjE1NDg2NzI0ODMsImV4cCI6MTU1MTI2NDQ4MywiYXpwIjoieFU4b1lHMzZXUldnUzQ2Q3FEVG9GRGVEaWwwTDE5VHciLCJzY29wZSI6InJlYWQ6Y2xpZW50X2dyYW50cyIsImd0eSI6ImNsaWVudC1jcmVkZW50aWFscyJ9.Hc27BQuXaDLtbogrIj5GuOf-cYOO1gSy3F5hRa7CuSbbjswwZkH21FujiIJYNY8Zpss-TkRonaBJTokbU1Jl_D_cKglVk6p5UchG8DCxtYZKkUQ1QrIKjiMJpsdB-f9_RczqvqogkARofDnZVTcmmoydFB9nBUSggiPbWnGkDNP28LA7_OJhv9X5Lne3Nlx0pIXYvmYNrJFVs_B6WS5DCnWUjveY_kUefXWticAdnSLag8Jbl3SxiDB9N5kPsi0sHTjmGneQcfxhIDSH3me0mpvjVxuIj1WeZfEqZfZGRxIHe1BW69LSHSvN3TChc06PeJlw3dD-pv1yBVWZA_5usg
Content-Length: 864

{
  "operationName": "FIELD_CLASSIFICATIONS",
  "query": "query FIELD_CLASSIFICATIONS ($id: ID!) {
    fieldClassifications(id: $id) {
        id
        fieldId
        name
        score
    }}",
  "variables": {
    "id": "1bc543d9-e50e-4289-9a54-59cbbd8e1b3d"
  }
} 
```

```python
Response:

HTTP/1.1 200 OK
access-control-allow-credentials: true
access-control-expose-headers: Authorization
connection: keep-alive
content-length: 1053
content-type: application/json; charset=utf-8
date: Mon, 28 Jan 2019 10:48:54 GMT
server: nginx/1.14.2
vary: Accept-Encoding
x-powered-by: Express

{"data":{"fieldClassifications":[[],[{"id":"jJoKc0qn1eVbPhFTTCH4eekUlRE=","fieldId":"6abeb009-810d-4d3b-8f7d-6c0d5161ff0d","name":"URL","score":0.7769230769230769}],[{"id":"JRpEZ+3hMnhyhi/oDl+V4ITnPMo=","fieldId":"96f94fc2-55e3-49ed-83ea-9d3628b22bb8","name":"NULL","score":0.7769230769230769}],[{"id":"wakY+8ovTj5mru7P8Cfw4kAUMqI=","fieldId":"67e9461e-8e74-4be0-9244-a394eb20c2cf","name":"NULL","score":0.7769230769230769}],[{"id":"qJOZLIPy2fdqJYHk1+aKPN8dlgY=","fieldId":"a36deff0-308c-4842-90a0-053749033049","name":"Number","score":0.9615384615384616},{"id":"qXlGil7fkUAhh8/VBK5JcrkTBXg=","fieldId":"a36deff0-308c-4842-90a0-053749033049","name":"DateKind","score":0.038461538461538464}],[{"id":"cYafysXCFp1eCIiul/Tjw3xJ2qc=","fieldId":"b5793965-bbb1-4e6e-b422-635ba058a07a","name":"NULL","score":0.7769230769230769}],[{"id":"FOgdw4P6TqFcuz7w81ijByy9KhU=","fieldId":"9dcef2c3-04cb-4e16-9700-04aba9e7b4a3","name":"INT","score":1},{"id":"eqZluGtSwSP0FpWRPnSSwFhQtRI=","fieldId":"9dcef2c3-04cb-4e16-9700-04aba9e7b4a3","name":"Categorical","score":1}]]}}
```
{% endtab %}

{% tab title="Expected Result" %}
All kind names are returned in appropriate format.
{% endtab %}

{% tab title="Actual Result" %}
'Kind' kind is returned as KIND.

```python
{"data":{"fieldClassifications":[[],[{"id":"jJoKc0qn1eVbPhFTTCH4eekUlRE=","fieldId":"6abeb009-810d-4d3b-8f7d-6c0d5161ff0d","name":"URL","score":0.7769230769230769}],[{"id":"JRpEZ+3hMnhyhi/oDl+V4ITnPMo=","fieldId":"96f94fc2-55e3-49ed-83ea-9d3628b22bb8","name":"NULL","score":0.7769230769230769}],[{"id":"wakY+8ovTj5mru7P8Cfw4kAUMqI=","fieldId":"67e9461e-8e74-4be0-9244-a394eb20c2cf","name":"NULL","score":0.7769230769230769}],[{"id":"qJOZLIPy2fdqJYHk1+aKPN8dlgY=","fieldId":"a36deff0-308c-4842-90a0-053749033049","name":"Number","score":0.9615384615384616},{"id":"qXlGil7fkUAhh8/VBK5JcrkTBXg=","fieldId":"a36deff0-308c-4842-90a0-053749033049","name":"DateKind","score":0.038461538461538464}],[{"id":"cYafysXCFp1eCIiul/Tjw3xJ2qc=","fieldId":"b5793965-bbb1-4e6e-b422-635ba058a07a","name":"NULL","score":0.7769230769230769}],[{"id":"FOgdw4P6TqFcuz7w81ijByy9KhU=","fieldId":"9dcef2c3-04cb-4e16-9700-04aba9e7b4a3","name":"INT","score":1},{"id":"eqZluGtSwSP0FpWRPnSSwFhQtRI=","fieldId":"9dcef2c3-04cb-4e16-9700-04aba9e7b4a3","name":"Categorical","score":1}],[{"id":"sHsbcQLUcBoZusoeOHRGEf6Wvr4=","fieldId":"0qUoVFS2haVs3apDwcWYBIDOejQ=","name":"KIND","score":1},{"id":"uBmS9oK16APeQt3fXzBLjzU5mkw=","fieldId":"0qUoVFS2haVs3apDwcWYBIDOejQ=","name":"Categorical","score":1}]]}} 
```
{% endtab %}
{% endtabs %}

