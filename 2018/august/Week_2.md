```
/^                                         /^^  
/^ ^^                                       /^^  
/^  /^^    /^^  /^^   /^^   /^^  /^^ /^^^^ /^/^ /^
/^^   /^^   /^^  /^^ /^^  /^^/^^  /^^/^^      /^^  
/^^^^^^ /^^  /^^  /^^/^^   /^^/^^  /^^  /^^^   /^^  
/^^       /^^ /^^  /^^ /^^  /^^/^^  /^^    /^^  /^^  
/^^         /^^  /^^/^^     /^^   /^^/^^/^^ /^^   /^^
                   /^^                          
```

#### 2018-08-09
- **GameMaker Language**
  - Comments are basically the same as Javascript comments `// /* */`
    - Adding `///` adding three lines in front of the comment will come up as a descriptor over the method it applies to.
  - `Literal` is a value that appears directly in your code.
  - `Identifiers` are names given to variables.
      ```
      age = 26
      age is the identifier
      26 is the literal value
      ```
  - `real('3') >> 3` takes a string and convert it into a number and `string(3) >> "3"` converts a number into a string.
  - `Variable Scope` describes the locations in the code where you have access to that variable >> global scope, instance scope and local scope.
    - `Global Scope` can be accessed from everywhere in the code.
    - `Instance Scope` are when variables are located within a instance. `name = Zuri`
    - `Local Scope` are variables defined within a local scope (Book does a shitty job explaining that part) `var name = Zuri`. The key difference with a local scope is that the keyword `var` proceeds it.
  - `Macros` are basically constants. Can't be reassigned. Fall under the _global scope_
    - Click `macro node` in the source tree
    - Select default
  - Enum are lists or set of key-value pairs. Accessing the values is the same as providing a object path in javascript. Enums are **constants**. Values can not be changed. Fall under the _global scope_
    ```
    enum level_locations {
      beginner='Fort Everest',
      intermediate= 'Hells Den',
      expert= 'Zeus Circuit'
    }
    ```
