# How can I specialize another service's Kinds?

## Question

#### How can I specialize another service's Kinds?

It is a best practice to rely on existing Knowledge Services when developing other services and applications.  Kinds shared from these services may need specializing in the context of the depending service.

We'd like to take advantage of shared schema, resolvers, and persistence \(scoped or shared\), as provided by the service, while providing custom definitions, resolvers, and persistence \(_scoped_ or _shared_\).

For example, service Core provides Email, which consists of only an address, and the common OpenCRUD boilerplate.

```
Core.Email { address: String }
```

I would like my new service to rely on this service while defining Email that adds a type property \(e.g., work, personal\) and also has OpenCRUD boilerplate.

```
MyService.Email { email: Core.Email, type: String }
```

By _scoped_, I mean that the shared service provide persistence for Email but in my context \(i.e., only email addresses that I store\). This is in contrast to _shared_, in which I would like to use and add to a collective set email addresses.  \(I don't mean to prescribe the solution, rather an illustration of a desired capability.\) . How can I specialize a shared Kind \(schema, resolver, persistence\), while delegating to it?

## Answer

\[TBD\]

