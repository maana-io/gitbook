---
description: Adding services and clients to Auth0
---

# Authentication & Authorization

## Maana Services API

Under the APIs section of Auth0 make one for hitting the API of Maana Services. This is used as the service that the clients authenticate for.

### Important Settings

* **Token Expiration**: set how long an individual access token lives for. This is in seconds.
* **Token Expiration For Browser Flows**: specifically for browser based flows like single page apps. Has to be less than or equal to "Token Expiration" and 86400 seconds \(24 hours\)
* **Allow Offline Access**: needs to be turned on if you want future versions of the CLI to be able to renew its access token.

### Important Information

* **Id**: to tell Auth0 what API we are when talking with them.
* **Identifier**: used mostly by the applications to say who their audience is for their access token.

### Scope

The following scope needs to be added to the API so clients can be authorized against them.

* **'read:client\_grants'**: This needs to be added as it is requested by a number of the services

## Maana Services Client

Under the Applications section of Auth0, make a new application for "Machine to Machine". This is for Maana's services that need to authenticate against the API.

### Important Settings

* **Application Type**: needs to be set to "Machine to Machine Application" as there is no user to authenticate as.
* **Token Endpoint Authentication Method**: needs to be "Post".

### Important Information

* **Domain**: Endpoint used to get an access token.
* **Client ID**: ID used to tell Auth0 what application we are.
* **Client Secret**: This is the secret used verify who we are.

### API Access

* Go into the Maana Services API, and under the "Machine to Machine Applications" section and set this application to “authorized” and “has access” to the 'read:client\_grants' scope.

## Maana Knowledge Portal Client

Under the Application section of Auth0 you need to make a new application for "Single Page Application". This is for you to log into the web app.

### Important Settings <a id="important-settings-2"></a>

* **Application Type**: this needs to be set to "Single Page Application" as this is the login style to be used.
* **Allowed Callback URLs**: needs to be set to your public name with the '/callback' path added, example: "https://q.maana.io/callback".
* **Allowed Web Origins**: needs to be set to the your public name, example: "https://q.maana.io".

### Important Information <a id="important-information-2"></a>

* **Domain**: This is the endpoint that we need to get our access token.
* **Client ID**: This is the ID used to tell Auth0 what application you are using.

### Adding Connections

* Navigate to the "Connections" section of the application.
* Make sure you enable at least one connections for users to sign in through.
* More information about these connections can be found at [https://auth0.com/docs/applications/connections5](https://auth0.com/docs/applications/connections5). 

## Maana CLI Client <a id="adding-services-and-clients-to-auth0-3"></a>

Under the Application section of Auth0, make a new application for "Native" apps. This is for you to login to the CLI.

### Important Settings

* **Application Type**: this needs to be set to "Native" as this is the login style that we using.
* **Allowed Callback URLs**: needs to be set to your public name with the '/user' path added, example: "https://q.maana.io/user".
* **Allowed Web Origins**: needs to be set to the your public name, example "https://q.maana.io".

### Important Information

* Domain: This is the endpoint that we need to get our access token.
* Client ID: This is the ID used to tell Auth0 what application we are.

### Adding Connections

* Navigate to the "Connections" section of the application and make sure you enable at least one connections for users to sign in through.
* More information about these connections can be found at [https://auth0.com/docs/applications/connections5](https://auth0.com/docs/applications/connections5).

## General Web Applications <a id="adding-services-and-clients-to-auth0-4"></a>

We use the Auth0 Lock library with a Single Page Application style auth.

* It can be seen in action in the Maana template located at **https://github.com/maana-io/Q-kapp-templates - Update**
* Auth0has a great tutorial on how to implement auth here [https://auth0.com/docs/libraries/lock/v11](https://auth0.com/docs/libraries/lock/v11)
* To renew the access token, use Auth0's silent authentication method [https://auth0.com/docs/api-auth/tutorials/silent-authentication](https://auth0.com/docs/api-auth/tutorials/silent-authentication) with a demo code here [https://auth0.com/docs/quickstart/spa/react/05-token-renewal](https://auth0.com/docs/quickstart/spa/react/05-token-renewal)

