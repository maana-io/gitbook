---
description: Execute functions efficiently using Maana Q
---

# Working with Lists

## Overview

So far, we have only worked with single-instance types \(scalars or Kinds\), such as a `name: STRING`, `dob: DATE`, `ceo: PERSON`.  It is often necessary to also model collections of types, such as the set of `employees: [Employee]` at a `Company`, the set of a `departments: [Department]` within the `Company`, `availabilityDates: [DATE]`.  In these tutorials, you will learn how to effectively use **lists** \(_aka_ collections, arrays\) in both modeling and computation.

## Introduction

A **list** in Maana Q is an **unordered** collection of the **same type** of _elements_, possibly **duplicate**, and possibly **`null`**.  Let's examine these attributes more closely and understand some of their implications.

### Lists are Strongly-Typed

The Maana Q system is _strongly-typed_, in that the system enforces compatibility of definitions between interacting components \(functions\).  It should not be possible, for instance, to send a `Person` instance to `loadVessel(cargo: Cargo)`.

A list, indicated by enclosing a type in square brackets \('`[]`'\), must be a collection of that type of element.  In other words, we always have a _list of type_ `T`.

{% hint style="info" %}
A list contains elements of the same type
{% endhint %}

Since lists are strongly-typed, it is not possible to provide generic operations on them \(i.e., [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_%28computer_science%29)\).  The Maana Q Scalars service provides various list operations for the scalar types, but you will need to supply custom functions for dealing with lists involving your types.

{% hint style="warning" %}
You must supply custom functions for manipulating lists of your own Kinds
{% endhint %}

### Lists are Unordered

The elements of list are not guaranteed to be in any order.  Sorting lists is usually dependent on the type of element being sorted.  For instance, how does one _naturally_ sort a list of `Person`? By name?  Last name?  Age?  Height?  Length of employment?

### Common Operations on Lists

Lists, regardless of type of element, have a standard set of _conceptual_ operations that often arise, such as:

* **Count** - how many elements are there?
* **Sort** - arrange the sequence in some order
* **Combine** - add two lists together in various ways \(concatenate, union, merge\)
* **CRUD** - add, update, remove elements
* **Search** / **Query** - find elements meeting specific criteria; predicates applied to attributes
* **Filter** - remove elements meeting criteria

## Lesson Goals



## 





















