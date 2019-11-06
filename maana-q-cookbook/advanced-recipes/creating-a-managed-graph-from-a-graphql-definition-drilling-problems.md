# Creating a Managed Graph from a GraphQL Definition: Drilling Problems

## About this Tutorial

In this tutorial, you will walk step-by-step for creating a managed graph from a GraphQL definition, loading it with data, adding custom services, and building a knowledge application.

### Installation

Use the GraphQL command line interface \(CLI\) with the Maana plugin:

```
npm i -g graphql-cli graphql-cli-maana
```

## Creating a Managed Graph

### Setup

Maana has included a `.graphqlconfig` file preconfigured for this tutorial.

**Minimally, ensure the endpoint is correct for the Maana endpoint you are using.**

**Optionally**, to create a configuration from scratch, create a CKG project and GraphQL endpoint, as in:

```
gql init
? Enter project name (Enter to skip): ckg
? Local schema file path: ckg.graphql
? Endpoint URL (Enter to skip): https://<maana host>:8443/graphql
? Name of this endpoint, for e.g. default, dev, prod: (default)
? Subscription URL (Enter to skip):
? Do you want to add other endpoints? No
? What format do you want to save your config in? JSON

About to write to /home/me/maana/training/.graphqlconfig:

{
  "projects": {
    "ckg": {
      "schemaPath": "ckg.graphql",
      "extensions": {
        "endpoints": {
          "default": "https://<maana host>:8443/graphql"
        }
      }
    }
  }
}

? Is this ok? Yes
```

### 1. Authenticating with Maana

Maana endpoints require a valid \(authenticated\) user in order to prevent unauthorized access.

#### Maana Q v3.1.0 and later

After creating a new `.graphqlconfig` file connecting to a Maana API endpoint:

1. Login to the Maana Knowledge Portal.
2. Click on your user icon and select your profile.
3. At the bottom of the profile page click the 'Get CLI Authentication Token' button.
4. Go through the login process \(again\).
5. Copy the generated auth token that shows up below the button.
6. In the terminal run `gql msignin` and when asked paste the Authentication Token into the prompt.
7. Run `gql menv --shell <your shell>` in the current terminal window to run authenticated GraphQL calls.
   * Example: Run `gql menv --shell bash` if you are using bash
   * You will see output similar to:

     ```
     export MAANA_AUTH_TOKEN=<token here>
     # Run this command to configure your shell
     # eval $(gql menv --shell bash)
     ```

   * Now run `eval $(gql menv --shell bash)` like it asks you at the bottom of the output.
8. Run `gql ping` to test out that the authentication works \(you will get an error if it did not\).

{% hint style="info" %}
#### **Additional Notes**

* When you add another project to your `.graphqlconfig` file you can run `gql maddheaders --project <Project Name>`to add the headers to the new project.
* When you want to run the CLI against the Maana API in a different terminal window you will need to run `gql env` again.
* If your authentication token expires you can run `gql mrefreshauth` to refresh the authentication token, when the Maana API is configured to allow the refreshing of authentication tokens.
{% endhint %}

#### Maana Q v3.0.5

After creating a new project connecting to a Maana endpoint, you will need to setup the project to add an authentication header to the requests.

1. Login to the Maana Knowledge Portal.
2. Click on your user icon and select your profile.
3. At the bottom of the profile page click the 'Get CLI Authentication Token' button.
4. Go through the login process \(again\).
5. Copy the generated auth token that shows up below the button.
6. In the terminal add an environment variable for the auth token.

```
# *nix based systems
export MAANA_AUTH_TOKEN=<paste auth token here>
```

```
rem Windows command line
set MAANA_AUTH_TOKEN=<paste auth token here>
```

```
# Windows power shell
$Env:MAANA_AUTH_TOKEN = "<paste auth token here>"
```

7. Add the authorization header to the Maana endpoint:

```
     "ckg": {
      "schemaPath": "ckg.graphql",
       "extensions": {
         "endpoints": {
-           "default": "https://<maana host>:8443/graphql"
+           "default": {
+             "url": "https://<maana host>:8443/graphql",
+             "headers": {
+               "Authorization": "Bearer ${env:MAANA_AUTH_TOKEN}"
+             }
+           }
         }
       }
     }
```

### 2. Create the Service

The domain model for the tutorial has already been created: `model.gql`. This GraphQL SDL file contains only the types we care about: Well, Location, DrillingReport, DrillingProblem, ...

Let Maana completely manage these types, creating the boilerplate queries, mutations, and subscriptions covering the basic CRUD \(Create, Read, Update, Delete\) operations.

You can use the GraphQL CLI with the Maana plugin command: `maddsvc` \("add service"\):

```
gql maddsvc "Drillng Problems" -s model.gql -p ckg
Using endpoint default: {"url":"https://<maana host>:8443/graphql"}
Read file: model.gql size: 483
Sending query:

      mutation addServiceSource($input: AddServiceSourceInput!) {
        addServiceSource(input: $input)
      }

✔ Call succeeded:
{"addServiceSource":"50d759d5-983d-4ea2-9773-20077c9b823e"}
```

Take note of the generated service id, since you'll add it as a new GraphQL **endpoint** to your CLI configuration.

### 3. Update the Config

Add another project to you graphql config using the following template to build your service url. Make sure that your url ends in `/graphql`.

#### Template:

```
https://<maana host>:8443/service/<service id>/graphql
```

#### Command:

```
gql add-project
? Enter project name for new project: db
? Local schema file path: db/schema.graphql
? Endpoint URL (Enter to skip): <service url>
? Name of this endpoint, for e.g. default, dev, prod: (default)
? Subscription URL (Enter to skip):
? Do you want to add other endpoints? No

Adding the following endpoints to your config:  db
? Is this ok? Yes
```

Again, you need to add the authorization header.

* In Maana Q 3.1.0 or later just run the `gql maddheaders` command.
* In Maana Q 3.5.0 will require adding it manually, check [here](https://github.com/maana-io/q-tutorials/tree/master/drill_prob#v3.0.5) for instructions.

### 4. Introspecting the Service

Only a few types were specified for the **domain model**. Maana adds a set of boilerplate types and operations as part of a fully-managed service. The **schema** for this service can be retrieved by:

```
gql get-schema -p dp
```

### 5. Loading Instance Data

Now that the model has been turned into a service, you can upload instance data to populate \("hydrate"\) the graph:

```
gql mload data/DrillingProblem.csv -p dp
gql mload data/Location.csv -p dp
gql mload data/DrillingReport.csv -p dp
gql mload data/Well.csv -p dp
```

For convenience, these steps have been added to a script file: `loadData.sh`

