---
description: Familiarize with Maana's methodology to decompose problems
---

# Problem Decomposition

## **Computational Knowledge Graph Technology and Systems Engineering**  

In Systems Engineering, the most generic definition of a System is simply: _'the Solution to a Problem.'_  Whether a system exists in physical or digital domains, and regardless of different levels of complexity, this orientation towards 'problem-solving' is a common theme in systems engineering philosophies and processes. 

Similarly, Maana's Computational Knowledge Graph \(CKG\) Technology is conducive for representing highly complex 'systems' with an orientation towards problem-solving and improved decision making. Taking this comparison further, we identify 4 areas of overlap between Systems Engineering and CKG Technology. These are summarized in the figure below.

![](../../../.gitbook/assets/image%20%28142%29.png)

### **Top-Down Approach**

In Systems Engineering it is fundamental to start by looking at the **system as a whole** in order to provide a thorough understanding of its components, its environment and interfaces, **System-level requirements** are often developed as a priority. This process is often followed by the i**dentification of likely sub-systems**, which are further broken down into assemblies and components. This process continues until a complete understanding is achieved of the system from top to bottom. This approach is documented on process standards such as ANSI/EIA-632.

A Top Down approach is key to ensuring any type of requirement low in the hierarchy can be traced up the top driver, and vice-versa. This level of interconnectedness is key to Systems Engineering approaches. 

In a similar manner, the methodology for decomposing a given problem in Maana Q, follows a Top Down approach where all subsequent decomposition steps maintain a relevance to the whole and a connection to the top. This architecture helps maintain coherency and also result in a more holistic approach to uncovering knock-on effects, interdependencies and system dynamics. 

### **Difference between System and System-of-Systems:** 

A '**System-of-Systems'** is a group of individual Systems. In this case, each System is optimized for its own purpose. The System-of-Systems is most likely not optimized. In business terms, this is equivalent to '**Local Optimization'** which is a common symptom for deficient systems thinking. 

 On the contrary, a **System \(made out of Sub-Systems\)** is optimized for its own purpose. This key concept of Systems Engineering is often overlooked in many domains. In a similar manner, the emphasis of CKG technologies is that of '**Global Optimization**' over 'Local Optimization', which is the result of modeling Systems and not a collection of isolated entities.  

### **Multi-disciplinary by Nature**

Systems Engineering emphasis the key role of interfaces between specialized functions. In a similar manner, CKG technologies foster the interaction of different roles. 

### **Lifecycle Thread**

One popular framework in Systems Engineering is: C - Conceive, D - Design, I - Implement, O - Operate. This emphasizes that Systems grow through different phases. The lack of a system approach often leads to failures, delays in interfaces between these distinct phases. CKG technologies applied through systems' lifecycle result in the persistence of contextual meaning of information from phase to phase. 

---

1. Identifying the problems means **spelling out** **in detail** **the terms used to describe the problem**
   1. **Let's consider the question** "Which car should I buy?"
      1. Identify the **given context**, and the **desired outcome**
         1. 1. Context: "I currently own a car valued at 20k and I have another 10k to spend. I would prefer it were an electric car, and I would like it to be red."
            2. Outcome: "a list of the top 5 recommended cars for me to buy"
         2. Do I have a good understanding of the **given context**? 
            1. Have I considered enough known factors so that I'm able to [naively](https://stackoverflow.com/questions/5700575/what-is-a-naive-algorithm-and-what-is-a-closed-form-solution) solve the problem?
               1. "What is the currency?" \(missing information\)
               2. "Would you buy a used car?" \(This could be a boolean input\)
               3. "Where do you live? Different promotions and discounts are available depending on your geographical location" \(This would be a geolocation input\)
            2. Are any of the given factors \(or inputs\) actually [red herrings](https://en.wikipedia.org/wiki/Red_herring)? 
               1. "Does the color of the car affect its price?" \(sometimes\)
         3. Can I imagine the "state of the world" when the problem is solved**?** **\(aka the "ideal world"\)**
            1. 1. "I get my 5 recommendations, and depending on the outcome, I'd choose one and buy it" \(Here our ideal state actually takes place when I buy a new car, and don't need to reach into my **savings**. Are there more problems that could be defined here? 
            2. When we set out to solve a problem, we initially have to visualize the best outcome in our mind's eye. This process helps us hone in on the properties of this "ideal" state of the world.  
            3. What are the concepts that describe the "ideal world"?
            4. Does my description of the "ideal world" match the **stakeholders'** description of an the "ideal world"? \(Is this "ideal" what everybody wants?\)
               1. **Need a different PQ** **here?**
      2. Identify nouns and verbs \(and/or questions\) for the given context and desired outcome
         1. **Nouns** \(which represent concepts\) are represented in Q  by [Kinds](https://en.wikipedia.org/wiki/Kind_%28type_theory%29)
            1. The **fields** of a Kind are its properties.
            2. Each field can refer to another Kind
            3. Each field \(or property\) of a Kind can indicate can be regarded as "singular" or "plural" \(a single element or a set\)
            4. Each field of a Kind can either be a required \(or non-nullable\) property of that Kind, or it could be optional \(or nullable\).
         2. **Verbs** \(which represent actions or dynamics between concepts\) and **questions** guide us in creating **functions** that describe the causal connection between the **given context** and the **desired outcome** 
         3. Functions take the form of "**given X what is Y?"** and are denoted name\(X\): Y
            1. X is the input to the function and represents what is known
            2. Y is the output of the function and represents what is unknown
            3. Functions can be **pure** or **impure**, depending on if it produces side effects or is referentially transparent \(i.e., always produces the same value, given the same input\).
            4. Sometimes X is nothing, such as:
               1. the impure function now\(\): Time, which doesn't produce the same value every time it is called
               2. or the pure function ten\(\): Integer, which always produces the same value \(10\)
                  1.  This is also called a constant function
   2. As we add details to our solution, we make it more coherent and defensible \(we provide more details to the "explanation" of this solution\)
      1. This includes identifying all the **relevant properties and relations** a Kind has
      2. Each relation is also a Kind, this process is repeated until the level of detail is sufficient to reason about the problem \(We'll discuss more about defining Kinds in the Ontology Building section\)
2. **Problem decomposition**
   1. When we decompose a problem, we are trying to tease apart all of the **factors** that we recognize as **contributing** to the solution. 
      1. For each property of the desired outcome \(represented by a Kind\), we need to consider: what steps must be taken to form the desired outcome given the situation \(or the **input** to our **function**\).
         1. Can we name these steps? These are the names of functions representing each step.
         2. What is the context \(or the given **input**\) for each of these steps? 
            1. Is the context provided for the step **sufficient to reason about completing this step**?
         3. Can we \(and should we\) add more context \(or inputs\) to this step? 
      2. As mentioned above, any concept has **name**, **properties**, and **relations**.
         1. A property is simple attribute, like height or due date.  Properties can't "stand on their own" \(i.e., some thing has a height\)
         2. A relation is a connection from one concept to another concept, such as Vessel has Cargo, each having their own properties and additional relations
   2. Can this problem be solved by and existing resource? \(A function in a service\)
   3. Can / how could the problem be broken up? 
      1. What concepts affect or contribute to the solution?
      2. What sub problems \(or "functions"\)  are involved in the solution? 
      3. Not all problems should be addressed at once. In fact, we need to limit the cognitive load required to understanding each "level" of our solution to the minimum possible. Consider the following questions as guidance for whether or not to add another problem to your current context. 
         1. Hierarchy 
            1. Do any the functions on this context depend on one another?
            2. Could/should a set of problems be combined?
         2. Scoping 
            1. is now the right time to articulate this problem/concept?
            2. Is anything required  to solve any of the sub problems, that is not provided by the containing problem \(the wrapping function\)?
   4. The process of problem decomposition can continue, **until** 
      1. There is a resource known to the author which could satisfy the requirement set by a function
      2. The author doesn't have \(and can't obtain\) more knowledge to further describe additional "sub problems", or another author would be better equipped to continue the decomposition.
3. **Reuse**
   1. Motivation for reuse
      1. Efficiency - not having to recreate the wheel speeds up development
      2. Collaboration - reuse forces common patterns to be shared as well as a common understanding, makes system cross-organizational \(opposed to silos of knowledge\)
      3. Generalization - Having reuse in mind helps with not over specifying our solution. 
         1. **Why is that important?...**
   2. Consider how a function could \(and if it should\) be reused in a different context. 
      1.  Is your function too specific or not specific enough?
   3. If broken differently, could you create functions with a bigger chance of being reused?
   4. Does a similar concept exist? Can it be specialized to be applied in this context?
   5. Does a similar function exist? Can it be wrapped and provided the required context?
   6. Could composition of existing functions to solve the problem
4. **Improvement**
   1. The solution does not have to be perfect the first time your write it. In fact it most likely will not be. 
      1. The process of developing a solution includes
         1. Exploring all the known facets of the problem 
         2. Unearthing the unknown unknowns 
         3. Ensuring team members and stakeholders develop a shared understanding of both the problem and the solution 
      2. The problem is going to be solved iteratively until the solution performs as expected
      3. The continuous improvement to the solution is going to be guided by
         1. Performance 
            1. Does the solution actually solve the problem?
            2. How well is the solution solving the problem?
            3. Could the solution \(or it components\) be improved?
         2. The quality of the solution 
            1. The level of detail involved that would contribute to the qualification the solution
            2. The verifiability of the logic of the solution
               1. Can the current components of the solution convince stakeholders of the correctness of the solution?
5. **Ontology Building**
   1. An ontology is a set of concepts, properties, relations, and individuals in a subject area or domain. In **knowledge modeling**, our goal is to develop a shared ontology for specific domains. By creating ontologies shared by different parts of our organization, we promote a **shared** **understanding** of our domain and we enable effective conversation around these shared concepts. 
   2. When we define a concept in a shared ontology, we should consider the following
      1. Is the definition of the concept too specific to be part of a shared ontology?
      2. Can a concept be broken down into separate concepts \(i.e., layers of abstraction\)?
      3. Are the properties of the concept inherent to the concept? For example, a "Person" has a "name", but not every person has a job. Should "job" be a property of "Person"?
   3. Relationships can themselves be modeled as concept, if they require properties and relations
      1. The relationship between an Employer and Employee is one of Employment
      2. It is insufficient to model this situation as Employer has Employees \(and the reciprocal Employee has Employers\), since we likely wish to capture job title/position, start/end dates, department, manager, salary, etc.

