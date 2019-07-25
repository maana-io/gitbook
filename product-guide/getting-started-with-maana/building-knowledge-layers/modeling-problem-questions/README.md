# Modeling Problem Questions

The goal of problem-question \(PQ\) modeling is to decompose a top level PQ into small enough PQs that each one can easily be implemented using code. Then it is just a matter of swapping in a Function from a service that has code that will perform the needed calculations. Ideally, this Function already exists in a service somewhere and can simply be added. However, it may not exist, at which point a new query or mutation needs to be added to a service and it needs an implementation that will perform the computation.

One of the keys of successful PQ decomposition is decomposing PQs into pieces that represent reusable functions. Reusable functions encapsulate functionality that is applicable to multiple solutions. Creating these reusable functions is what allows one to truly harness the power of the Q platform. You can think of Q a bit like a toolbox and Functions are the tools. Every time a new function is created it gets added to the toolbox. Just like a tool that can be used in multiple projects is much more valuable than one that can only be used a single project, Functions that can be used in multiple solutions are much more valuable than Functions that can only be used in a single solution. This will allow you \(or someone else\) to solve similar problems without having to reinvent the wheel every time.

When decomposing PQs, asking yourself the following can help lead to a good solution:

1. Does a Function that solves this PQ already exist?
   1. If not, if this PQ is implemented in code, would the Function be reusable in other solutions?
2. Is it difficult to decompose this PQ into multiple smaller PQs?
3. Can this PQ easily be implemented in code? \(this may be something that software engineers help decide\)

If you answer "no" to any of these questions, it is worth trying to decompose the PQ even further.

There may be multiple ways to decompose a PQ, so how do you decide which way to decompose it? Let's take a quick look at an example of a PQ and walk through the decomposition.

> PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?

Let's ask ourselves the questions above. The first question is

> Does a Function that solves this PQ already exist?

If it does, great, you're done! That wouldn't be a very useful example though, so let's say that it doesn't exist. Next question

> If this PQ is implemented in code, would the Function be reusable in other solutions?

It seems very specific as is, so this seems like a "no". 

Now that we've already answered "no" to the first two questions, we should try to decompose it further, however for the sake of this exercise let's take a look at the last two questions:

> Is it difficult to decompose this PQ into multiple smaller PQs?
>
> Can this PQ easily be implemented in code?

There are a few ways to decompose this further, so "no" to the first question. For the second question, this probably wouldn't be hard to code but since we can easily decompose it further, let's do it.

One way to decompose this would be the following two PQs

> PQ: Given an actor and a year, what films was the actor in during the given year?
>
> PQ: Given a list of films, what is the highest grossing film?

Putting these two together gives us an answer to our original PQ. It has been decomposed!

An alternative decomposition is

> PQ: Given an actor, what are the his/her highest grossing films by year?
>
> PQ: Given a list of films and a year, what is a film from the list that was released in that year?

It may not be obvious but this also would also answer the original PQ.

Which decomposition makes more sense? Let's go with the first one because its PQs seem much more reusable. For each PQ, let's ask ourselves the same set of questions, starting with the first PQ:

> PQ: Given an actor and a year, what films was the actor in during the given year?

Let's say there isn't a Function that already exists that answers this. This also looks like it can be decomposed further.

{% hint style="info" %}
Try decomposing this PQ yourself before reading on!
{% endhint %}

How can this be decomposed further? How about this \(your solution may be different!\):

> PQ: Given an actor, what is the list of films the actor was in?
>
> PQ: Given a list of films and a year, what are the films from the list that were released in that year?

Once again, for each of these PQs ask yourself the four questions above. Let's say at this point we are satisfied that we have sufficiently decomposed these PQs. Now let us return to the second PQ from the first decomposition we did:

> PQ: Given a list of films, what is the highest grossing film?

Ask ourselves the same four questions. This seems pretty straightforward to implement, seems very reusable, and would be pretty difficult to decompose further so let's keep it as is. This leaves us with the following decomposition:

> * Top level PQ: Given an actor and a year, what was the highest grossing film of the year that the actor was in?
>   * PQ: Given an actor and a year, what films was the actor in during the given year?
>     * PQ: Given an actor, what is the list of films the actor was in?
>     * PQ: Given a list of films and a year, what are the films from the list that were released in that year?
>   * PQ: Given a list of films, what is the highest grossing film?

Great! Now that we have decomposed a problem-question, how do we model this solution in Q? Let's take a look at that next.

{% hint style="info" %}
It is highly encouraged to model the solution in Q _during_ the process of problem-question decomposition rather than doing the two independently. This is what Q is built for!
{% endhint %}

