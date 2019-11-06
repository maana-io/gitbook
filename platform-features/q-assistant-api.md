# Q-Assistant-API

## What is the Q Assistant API?

The Q Assistant API is a client-side API exposed by the Q Knowledge Portal \(K Portal\) to service assistants. This API is exposed via the post-message protocol, as the assistants are embedded as HTML i-frames. 

### Post-Robot Communication

K Portal uses the kraken/post-robot library to enrich the communication with the assistant. Post-robot allows for asynchronous, promise-based request/response style behavior between the assistant and the assistant API. Assistant web applications are expected to use post-robot in order to communicate with the API. To help accelerate assistant application development, Maana  publishes its own client library for communicating with the API. This will be covered next.

### Q-Assistant-Client

The Q assistant client is an NPM package to allow for more streamlined, explicit,  and cross-platform communication with the K Portal API.

The assistant client is available as an NPM package at [https://www.npmjs.com/package/@io-maana/q-assistant-client](https://www.npmjs.com/package/@io-maana/q-assistant-client), and on Github at [https://github.com/maana-io/q-assistant-client](https://github.com/maana-io/q-assistant-client)

**Examples of using the assistant can be found on the NPM link above.**

`develop` branch on github will contain latest updates to the client and can be obtained by installing the npm package with a `@beta` tag. 

### Helper Surface Area in 3.2.1

There are several pieces of API surface area that are not documented, but are used as helper functions for documented surface area. 

These are explained below:

**enableInventoryChangedNotification**

This is a helper method used to grant consent for these notifications.

**disableInventoryChangedNotificaiton**

This is a helper method used  to revoke consent for these notifications.

**enableSelectionChangedNotification**

This is a helper method used to grant consent for these notifications.

**disableSelectionChangedNotification**

This is a helper method used to revoke consent for these notifications.

**getEventEmitter**

Returns the even emitter object used to handle subscriptions within the client.

### Undocumented \(experimental\) Surface Area in 3.2.1

These are officially unsupported in 3.2.1 and subject to change as they are experimental. 

**refreshServiceSchema**

Invokes a refresh of a service's schema in maana-catalog. Subsequenly, this method invokes `reloadServiceSchema` in order to update the workspace inventory. 

```
await AssistantAPIClient.refreshServiceSchema('serviceid...')
```

**reloadServiceSchema**

Ensures consistence between a service's schema, as it exists in Maana, and what is reflected in the workspace's service inventory. This does NOT invoke a refresh of the service schema through catalog; ****instead, it is designed to help ensure valid workspace state given peripheral updates. 

```
await AssistantAPIClient.reloadServiceSchema('serviceid...')
```

**createService**

Creates a service. Minimum input is an object containing `name` , `endpointUrl` , and `serviceType` fields. The service `id` will be returned. 

```
  const svc = await AssistantAPIClient.createService({
    name: 'mySvc',
    endpointUrl: 'http://192.....:...',
    serviceType: 'EXTERNAL'
  })
```

**importService**

Imports a service into the workspace inventory. Returns the service `id`

```
await AssistantAPIClient.importService('service id...'
```

**executeGraphql**

This is used to execute an arbitrary graphql query/mutation against a service. The input is an object containing`serviceId`, `query`, and `variables` \(a javascript object consisting of name/value pairs\). The result object containing `data` and `errors` fields will be returned:

```
  const result = await AssistantAPI.executeGraphql({
    serviceId: 'service id...',
    query: 'query{helloWorld}',
    variables: {}
  })
```





