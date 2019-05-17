# What are Problem Questions?

At the end of this topic, you will be able to take the first steps of building a solution by identifying and decomposing problem questions.

### Business Objectives to User Requirements

Staying with our definition of knowledge as the answer to a question in order to answer a big, complex question about a domain, it has to be broken down into smaller pieces that best represent the problem domain. To define the problem domain, Maana allows users to recursively work through a problem decomposition process.

Each problem-question, including the one at the very top can be represented using the concept of a Function \(multiple inputs, one output\) in the Maana platform. One of the high level benefits of using this format is that you will end up with a 1 to 1 mapping in terms of expressing the same thing as the function. 

The first step of the process is to identify what your problem question \(PQ\) is.  This will come from your original Business Objective.  You'll want to start by asking, "Given X, what is Y?"  Once you've identified your initial PQ, you'll want to start to identify concepts to define.  Then, add these identified concepts to your schema.

Next, you'll begin to interpret your PQ by asking questions like, "Should you get Y from X an implicit query \(Y is an attribute of X\), or through an explicit query?" This will prompt you to then ask, "Does the intermediate PQ build the logic for that relationship?"  If the answer is yes, then you'll want to walk back through the Problem Decomposition process again until you are able to answer no.  At that point, you'll have your PQ completely broken down and can move on to the next step in the process.



![](../../../../.gitbook/assets/image%20%2858%29.png)

### What are the benefits of this approach?

By decomposing problem-questions into smaller parts, you end up creating an architectural scaffolding for your solution that can then be reinforced with the right data, algorithms and services. This also adds reusable pieces that speed up the construction of similar or adjacent solutions. Another benefit of this approach is explainability. 

The ability to think abstractly about problems, and then to represent the logic and reasoning behind the decision making capabilities allows future users to backtrack and say, "Okay, this is why this decision was made." That's incredibly important for most of our customers. It's imperative that users know how you got to the answers. You have to be able to easily show them that.

