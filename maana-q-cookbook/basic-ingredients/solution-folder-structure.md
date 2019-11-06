# Solution Folder Structure

## Layout

A Knowledge solution usually consists of multiple microservices \(in Python, C\#, JavaScript, Scala, ...\) and a UI application \(in React, Angular, Django, ...\).  The following basic structure is recommend:

```
/my_solution
  /application
  /services
    /my_service_1
    /my_service_2
  .gitignore
  .graphqlconfig
  LICENCE.md
  README.md
```

## Branching Strategy

Assuming the use of a Git-based \(or Git-like\) repository, then it is recommended to setup a "development" branch and a "master" branch,.  Specific features are branched from "development" for a release cycle and merged back in \(via pull requests\).  When development is ready for release testing, then a "release candidate" branch is created and tested.  Any issues need to be managed between "development" and the "release candidate" branch, as "development" may now be ahead for the next release cycle.  When the "release candidate" is finalized, then it is merged into "master."



