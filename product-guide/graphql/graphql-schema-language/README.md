# GraphQL Schema Language

### GraphQL Schema Language - Type System

#### Object Type

Represents a node within the GraphQL graph:

`type Human {  
    name:  String  
    currentlocation:  String`

{% hint style="info" %}
**Note**:  Must have _at least_ one **field**.
{% endhint %}

#### Object Type:  Field Resolvers

**Resolvers** are passed with 3 main Arguments:

1. **Object** - The Object on which the Field is being resolved.
2. **Args** - The Arguments passed to the Field.
3. **Context** - A Context object useful for authentication and caching.

#### Object Type:  Summary

This represents a **Node** within the GraphQL graph:

`type Human {  
    name:  String  
    currentlocation:  (approximate: Boolean): String  
favouritePosts(first: Int = 5 after: Cursor): [Post}  
}`  


For each Node:

* They must have at least one **Field**.
  * Each Field must return a defined **Type**.
  * Fields are backed by a function called a **Resolver**.
  * Fields can have **Arguments**.
    * Arguments can have **Defaults**.

#### Union Types

Union Types are assumed to have _no Fields in common_.

`{  
  search(terms:  "Star Wars")  {  
       ... on Film  {  
          title  
          duration  
      }  
      ... on Publisher  {  
          name  
          address  
       }  
     }  
    }`   

### GraphQL Schema Language - Writing a Schema

#### The Mutation Type

A typical example might look like this:

`type mutation  {  
    setGreeting(input:  SetGreetingInput):  SetGreetingPayLoad  
}  
input  SetGreetingInput  {  
   newGreeting:  String  
}  
type  SetGreetingPayLoad  {  
   greeting:  String`

#### Schema Example

`scalar  JSON  
enum Color  {  RED,  GREEN,  BLUE,  OCTARINE  }  
input AgeRange  {  min:  Float!,  max:  Float!  }  
interface NamedEntity  {  name:  String!  }  
  
"""Someone who can log in"""  
type User implements NamedEntity  {  
   firstName:  String @deprecated(reason:  "Please use 'name' instead")  
   name:  String!  
   #  To the nearest nanaosecond  
   age:  Float  
   meta:  JSON  
   favoriteColor:  Color  
   friends:  [User}  
}  
type Query  {  
   viewer:  User  
   usersByAge(range:  AgeRange):  [User!]  
}`

####  Anatomy of a GraphQL Query

This is an example of a simple GraphQL query; 

`{  
   currentUser  {  
   name  
   website  
  }  
}`

`query ProfileQuery {  
    currentUser  {  
         name  
         website  
      }  
 }`

The name \(`ProfileQuery`\) is an optional, arbitrary name for the query.  It is useful for debugging.

#### Directives

Directives can be used to change how the server processes the query.  The GraphQL specification defines two directives:

1. @include
2. @skip

`query ProfileQuery(  
  $id: Int!,  
  $toggle: Boolean = true  
) {                                                              {  
     user(id:  $id)  {                                              "user": {  
        name          @include(if: $toggle)                          "name": "Bob Smith"  
        website        @skip(if: $toggle)                          }  
     }                                                              }  
  }`

#### Recap:

`query  ProfileQuery($id:  Int!)  {  
  user(id: $id) {  
     fullname: name  
     website  
  }  
}  
query                                #Operation type  
ProfileQuery                         #Operation name, for debugging  
($id:  Int!)                         #Variables and their types  
{                                    #Selection set  
     user(id:  $id)                  #Field with arguments, variable reference  
     {                               #Nested selection set  
          fullName:  name            #Aliased field, fetches 'name', calls it 'fullName'  
          website                    #Field sans alias  
     }                
}`               

### GraphQL Fragments

#### The Anatomy of a Fragment

`fragment GreetUserFragment on User {  
  id  
  name                    query MyQuery {  
}                           currentUser {      
                               id  
query MyQuery {                id  
currentUser {                  name  
  id                          }  
  ...GreetUserFragment      }  
     }  
}`     

#### Fragments can Compose other Fragments:

`quey MyQuery {  
  currentUser {  
     ...UserProfileFragment  
  }  
}  
fragment UserProfileFragment on User {  
  id  
  name  
  bio  
  ...LargeUserAvatarFragment  
}  
fragment LargeUserAvatarFragment on User {  
   largeAvatar: avatar(size: 300, retina: true)  
}`

{% hint style="info" %}
**Note**:  Simple string concatenation, as shown here, will not allow the same fragment twice.  It is suggested that a tool such as Apollo or Relay be used to do this.
{% endhint %}

#### **Inline Fragments**

A variant of these named fragments are anonymous inline fragments.

`{  
   search(phrase: "cream"){  
     ...on Food{  
       manufacturer  
       calories  
    }  
    ...on BeautyProduct {  
      manufacturer  
      spf  
    }  
    ...on Paint {  
      manufacturer  
      hexColor  
     }  
    }  
  }`

### Graph Mutations

#### Multiple Mutations in One Query

The following illustrates how to perform multiple mutations in one query:

`mutation {  
  # Mutation 1  
  updateCurrentUser(input: {  
    userPatch: {  
      website: "https://twitter.com/benjie"  
    }  
  }) {  
     user { website }  
  }   
  #Mutation 2  
  setGreeting(input: {  
    newGreeting: "Hello Universe!"  
  }) {  
     greeting  
  }  
}`





