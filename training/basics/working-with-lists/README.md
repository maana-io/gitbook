---
description: Execute functions efficiently using Maana Q
---

# Working with Lists

So far, we have only worked with single-instance types \(scalars or Kinds\), such as a `name: STRING`, `dob: DATE`, `ceo: PERSON`. It is often necessary to also model collections of types, such as the set of `employees: [Employee]` at a `Company`, the set of a `departments: [Department]` within the `Company`, `availabilityDates: [DATE]`. In these tutorials, you will learn how to effectively use **lists** \(_aka_ collections, arrays\) in both modeling and computation.

## Introduction

A **list** in Maana Q is an **unordered** collection of the **same type** of _elements_, possibly **duplicate**, and possibly **`null`**. Let's examine these attributes more closely and understand some of their implications.

### Lists are Strongly-Typed

The Maana Q system is _strongly-typed_, in that the system enforces compatibility of definitions between interacting components \(functions\). It should not be possible, for instance, to send a `Person` instance to `loadVessel(cargo: Cargo)`.

A list, indicated by enclosing a type in square brackets \('`[]`'\), must be a collection of that type of element. In other words, we always have a _list of type_ `T`.

{% hint style="info" %}
A list contains elements of the same type
{% endhint %}

Since lists are strongly-typed, it is not possible to provide generic operations on them \(i.e., [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_%28computer_science%29)\). The Maana Q Scalars service provides various list operations for the scalar types, but you will need to supply custom functions for dealing with lists involving your types.

{% hint style="warning" %}
You must supply custom functions for manipulating lists of your own Kinds
{% endhint %}

### Lists are Unordered

The elements of list are not guaranteed to be in any order. Sorting lists is usually dependent on the type of element being sorted. For instance, how does one _naturally_ sort a list of `Person`? By name? Last name? Age? Height? Length of employment?

Since you are ALWAYS interacting with services, there is NEVER a guarantee about what is happening _behind_ the service interface --- you only have the interface it gives you. Therefore, there are no common **query** that can be issued for items that produces a specific **ordering** \(i.e., there is no `SELECT x WHERE y ORDER BY z` equivalent standard\). Therefore, in specific cases, please refer to the service schema for what it provides.

### Lists May Have `NULL` Elements

You have learned about the use of required vs optional type modifiers on scalars and Kinds. We can apply optionality requirements on lists, too, although it is a bit more complicated.

There are two possible things that could be optional \(i.e., allowed to be `null`\) when it comes to lists:

1. The list itself, e.g., `[Person]!`
2. The list elements, e.g., `[Person!]`

There are, therefore, 4 possible combinations with the most common being:

* `[Person]` - a possibly null list with possibly null elements
* `[Person!]!` - a non-null list with non-null elements

In fact, these are the **only two that are valid** in Maana Q.

{% hint style="info" %}
A non-`null` list with non-`null` elements can still be an **empty** list
{% endhint %}

Recall that a type is required if it is indicated with an exclamation point, e.g., `sayHello(person: Person!): String!`, which states that the function takes a required argument of `Person` and produces a required `String` value.

### Lists Can Have Duplicate Elements

By default, a Maana Q list has no restrictions on the values allowed to be in a list other than type. The concept of a set has non-duplicate element semantics and certain operations, such as union, imply such semantics. It is up to you if you wish to allow or disallow duplicates based on contest of use. Your functions will need to deal accordingly.

### Common Operations on Lists

Lists, regardless of type of element, have a standard set of _conceptual_ operations that often arise, such as:

* **Count** - how many elements are there?
* **Sort** - arrange the sequence in some order
* **Combine** - add two lists together in various ways \(concatenate, union, merge\)
* **CRUD** - add, update, remove elements
* **Search** / **Query** - find elements meeting specific criteria; predicates applied to attributes
* **Filter** - remove elements meeting criteria

## Lesson Goals

In this lesson set, you will learn how to:

* Use KindDB boilerplate functions to retrieve Kind collections
* Iterate through elements of a list, applying a function
* Kind field projection
* Combine lists in various ways
* Perform list filtering  

