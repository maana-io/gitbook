# What are Problem Questions?

At the end of this topic, you will be able to take the first steps of building a solution by identifying and decomposing problem questions.

### Business Objectives to User Requirements

Staying with our definition of knowledge as the source for finding the answer to big, complex question about a domain, the questions have to be broken down into smaller pieces that best represent the problem domain. To define the problem domain, Q allows users to recursively work through a problem decomposition process.

Each problem-question, including the top-level PQ, can be represented using the concept of a Function \(multiple inputs, one output\) in the Q platform. One of the high level benefits of using this format is that you will end up with a 1 to 1 mapping in terms of expressing the same thing as the function. 

The first step of the process is to identify what your problem question \(PQ\) is.  This will come from your original Business Objective.  You'll want to start by phrasing the problem as "Given X, what is Y?"  This is your top-level PQ. Once you've identified the top-level PQ, you'll want to start to decompose it into "smaller" PQs that when put together, solve the top-level PQ.  

To begin the PQ decomposition process, ask yourself "Can you get Y from X directly \(meaning Y is an attribute of X\), or does it require a query?" If it requires an explicit query, ask yourself "Can the PQ be broken down into intermediate PQs that build the logic for getting Y given X?"  If the answer is yes, then you'll want to walk back through the Problem Decomposition process again. Continue repeating this process until everything can be gotten through an implicit query or the explicit queries cannot be decomposed further.  At that point, you'll have your PQ completely broken down and can move on to the next step in the process.

![Problem-Question Decomposition](https://maanaimages.blob.core.windows.net/maana-q-documentation/Product%20Guide/Problem-Question%20Decomposition.png)

### What are the benefits of this approach?

By decomposing problem-questions into smaller parts, you end up creating an architectural scaffolding for your solution that can then be reinforced with the right data, algorithms and services. This also adds _reusable_ pieces that speed up the construction of similar or adjacent solutions. Another benefit of this approach is explainability. 

The ability to think abstractly about problems, and then to represent the logic and reasoning behind the decision making capabilities allows future users to backtrack and say, "Okay, this is why this decision was made." That's incredibly important for most of our customers. It's imperative that users know how you got to the answers. Proper problem-question decomposition allows you to easily show them that.

Next let's take a look at an example of problem-question decomposition and see how that fits in with the problem-question modeling provided by the Q platform.

