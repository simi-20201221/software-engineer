# Programming Language - Interpreter
============


## Reference

* http://www.craftinginterpreters.com/


## Content


### Concept

* Interpreter for a full-featured language: two complete
* Language
  * Little language
  * Domain-specific language
* Interpreter
* Compiler
* Implementation
  * (1) Source text
  * (2) Analyzes
  * (3) Transform
  * (4) Higher-level presentation
  * (5) Low-level presentation


### Interpreter - A Map of the Territory

* ![Interpretre - A Map of the Territory](interpreter/interpreter-map-territory.png)



#### Scanning - Lexing (Lexical analysis)

* Takes in the `linear stream of characters` and `chunks` them together into a series of something more akin to `words`.
* In `programming languages`, each of these `words` is called a `token`.

#### Parsing

* `Syntax` gets a `grammar`.
* The ability to compose larger `expressions` and `statements` out of smaller parts.
* Parser: `parse tree` or `abstract syntax tree (AST)` or `syntax trees`.
* `Syntax errors`.

#### Static analysis

* Local variables? Global? Where are they defined?
* The first bit of analysis that most languages do is called `binding` or `resolution`.
* For each `identifier`, find out where that name is defined and wire the two together.
* `Scope`: the region of source code where a certain name can be used to refer to a certain declaration.
* Language typed
  * Statically typed
    * type check
    * type error
  * Dynamically typed
* Stored
  * attributes
  * symbol table
    * the keys to this table are identifiers—names of variables and declarations

#### Intermediate representations

* Source language where the program is written in
* Intermediate representation
* Final architecture where the program will run

#### Optimization

* Optimize - performance effort on the runtime

#### Code generation

* `Code` here usually refers to the kind of primitive `assembly`-like instructions a `CPU runs` and `not` the kind of `source code` a `human` might want to `read`.
* CPU
  * real
    * get an executable that the OS can load directly onto the chip.
    * `native code` is lightning `fast`, but generating it is a lot of work, complex. 
    * `compiler` is tied to a `specific architecture` (ex: if compiler targets `x86` machine code, it’s not going to run on an `ARM` device)
  * virtual
    * virtual machine code
    * bytecode
      * designed to map a little more closely to the language’s semantics, and not be so tied to the peculiarities of any one computer architecture and its accumulated historical cruft
      * like a dense, binary encoding of the language’s low-level operations.

#### Virtual machine

* A program that emulates a hypothetical chip supporting your virtual architecture at runtime.
* Running bytecode in a VM is `slower` than translating it to native code `ahead of time` because every instruction must be simulated at `runtime` each time it executes.
* Implicity and portability

#### Runtime

* If `compiled` it to `machine code`, simply tell the `operating system` to `load` the `executable` and `off` it goes. 
* If `compiled` it to `bytecode`, need to `start` up the `VM` and `load` the program into that.
* Manages memory
  * `garbage collector` going in order to reclaim unused bits
* `instance of` kind if object during excution
* In a fully `compiled language`, the code implementing the `runtime` gets inserted directly into the resulting executable (each compiled application has its own copy of runtime directly embedded in it => Go language).
each compiled application has its own copy of Go’s runtime directly embedded in it.
* If the language is `run inside an interpreter or VM`, then the runtime lives there (Java, Python, JavaScript, ... language)

#### Compiler

* `Compiling` is an `implementation technique` that involves translating a source language to some other—usually lower-level—form. 
  * When generate `bytecode` or `machine code` => compiling. 
  * When transpile to another high-level language => compiling.
* `Compiler` is mean translates `source code` to some other form but does `not execute` it.
  * The user has to take the resulting output and run it themselves.
* `Interpreter` is mean takes in `source code` and `executes` it immediatelt.
  * It runs programs `from source`

#### Tree-walk interpreters

#### Transpilers

#### Just-in-time (JIT) compilation


### Fundamental

* [The Next 700 Programming Languages](https://homepages.inf.ed.ac.uk/wadler/papers/papers-we-love/landin-next-700.pdf)

#### High-level Language

* **(1) Typing**
  * Static typed
    * Type errors are detected and reported at compile time before any code is run
    * Most statically typed languages do some type checks at runtime.
  * Dynamically typed
    * Defer checking for type errors until runtime right before an operation is attempted.
    * `Variables` can `store values` of `any type`, and a `single variable` can even `store values` of `different types` at `different times`.
    * If try to `perform` an `operation` on `values` of the `wrong type`, then the `error` is `detected` and `reported` at `runtime`.
* **(2) Automatic Memory Management**
  * Managing memory: two main techniques
    * `reference counting`
      * simpler to implement
      * Perl, PHP, and Python, ...
    * `tracing garbage collection` (`garbage collection` - `GC`)
      * Working at the level of raw memory
      * [A Unified Theory of Garbage Collection](https://researcher.watson.ibm.com/researcher/files/us-bacon/Bacon04Unified.pdf)

#### Data Types

* Built-in data types
  * `Boolean`
    * value: true/false
    * logic
  * `Number`
    * integer
    * double-floating point
  * `String`
    * string literal
    * enclosed in doule quotes
  * Nil/`Null`
    * represents `no value`
    * null pointer error

#### Operator

* `binary` operators

* **(1) Arthmetic**
  * add (`+`); subtract (`-`); multiply (`*`); divide (`/`)
* **(2) Logical**
  * Comparision: lessThan (`<`); lessThan orEqual (`<=`); greaterThan (`>`);
greaterThan orEqual (`>=`);
  * Equality (`==`)
  * Inequality (`!=`)
  * And (`&` or `&&`)
  * Or (`|` or `||`)
  * Xor (`^`)
  * Not (`!`)

#### Expression

* `Operands` are the `subexpressions` on either side of the `operator`.
* Because the `operator` is `fixed` in the `middle` of the `operands`, these are also called `infix` operators (as opposed to `prefix` operators where the operator comes before the operands, `postfix` where it comes after).
* An `and` expression determines if `two values` are `both true`. 
  * It returns the `left` operand if it’s `false`, or the `right` operand otherwise.
  * (`short-circuit`) Not only does and return the left operand if it is false, but it also doesn’t even `evaluate` the right one in that case.
* An `or` expression determines if either of `two values` (or both) are `true`. 
  * It returns the `left` operand if it is `true` and the `right` operand otherwise.
  * (`short-circuit`) If the left operand of an or is true, the right is skipped.
* `Precedence` and `grouping`
  * use `()` to group stuff
* An expression’s `main job` is to `produce a value`.

#### Statements and State

* A statement’s `job` is to `produce an effect`.
* Statements do `not evaluate` to a `value`, to be useful they have to otherwise change the world in some way—usually `modifying` some `state`, `reading input`, or `producing output`.
* An `expression` followed by a `semicolon (;)` promotes the expression to `statement-hood`. This is called (imaginatively enough), an `expression statement`.

#### Block

* To `pack` a series of `statements` where a `single one` is expected
* Blocks also `affect scoping`

#### Variable

* `Declare` variable
  * Ex: using `var` statements
  * name variable
* `Initializer` variable
  * If `omit` the `initializer`, the `variable’s value defaults` to nil/`null`.
* `Access` and `Assign` a variable
* `Scope` of variable
  * Global variable
  * Local variable


#### Control Flow

* **(1) Conditional**
  * `if`...`else`... statement 
    * executes one of two statements based on some condition.
  * Conditional operator (`?`...`:`...)
  * `switch`...`case`... statement
* **(2) Loop**
  * `while` loop 
    * executes the body repeatedly as long as the condition expression evaluates to true.
  * `for` loop
    * `for-in` or `foreach` loop
      * explicitly iterating over various sequence types
* **(3) Jump**
  * `break`
  * `continue`

#### Functions

* Functions are `first` class
  * They are `real values` that can `get a reference` to, `store in variables`, `pass around`,
* `Declare` function
  * A `parameter` (`formal parameters` or `formals`) is a `variable` that `holds` the `value` of the `argument` inside the `body` of the `function`. 
  * A function `declaration` has a `parameter list`.
  * Function declarations are `statements`
    * can `declare local functions inside another function`.
* The `body` of a `function` is always a `block`. 
  * `Inside` it, can `return` a `value` using a `return statement`.
  * If `execution` reaches the `end of the block` without hitting a return, it `implicitly returns` nil/`null`.
* Type of function
  * `Closures`
    *  ```js
       fun outerFunction() {
            fun localFunction() {
                print "I'm local!";
            }

            localFunction();
        }

        fun returnFunction() {
            var outside = "outside";

            fun inner() {
                print outside;
            }

            return inner;
        }

        var fn = returnFunction();
        fn();
        ```
    * combine local functions, first-class functions, and block scope,...
    * inner() accesses a local variable declared outside of its body in the surrounding function.
    * closure function do: inner() has to `hold on` to references to any surrounding variables that it uses so that they stay around even after the outer function has returned. 
* Function `call` expression
  * `passing argument`
  * An `argument` (`actual parameter`) is an `actual value` pass to a function when it. 
  * A function `call` has an `argument list`.

#### Resolving and Binding

#### Classes or prototypes

* object-oriented language & object-oriented programming (`OOP`)
  * `encapsulating` `behavior` and `state` together
* [Class-based programming](https://en.wikipedia.org/wiki/Class-based_programming)
  * two core `concepts`: `instances` and `classes`.
  * Instances `store` the `state` for each `object` and have a `reference` to the `instance’s class`. 
  * Classes `contain` the `methods` and `inheritance chain`.
  * To `call` a `method` on an `instance`, there is always a level of indirection. Look up the instance’s class and then find the method there:
  * ![Class-based programming](./fundamental/class-based-programming.png)
* [Prototype-based programming](https://en.wikipedia.org/wiki/Prototype-based_programming)
  * merge these two concepts (`instances` and `classes`), `only objects—no classes`.
  * each individual `object` may contain `state` and `methods`.
  * Objects can `directly inherit` from each other (or `delegate to` in prototypal lingo)
  ![Prototype-based programming](./fundamental/prototype-based-programming.png)
  * prototypal languages are more fundamental than classes.
    * really neat to implement because they’re so `simple`
    * express lots of unusual patterns that classes steer away from
* There are three broad paths to object-oriented programming
  * Class
  * [Prototype](http://gameprogrammingpatterns.com/prototype.html)
  * [Multi-methods](https://en.wikipedia.org/wiki/Multiple_dispatch)
* Life Cycle Object Class
  * ![Life Cycle Object Class](./fundamental/life-cycle-object-class.png)
  * `Exposes` a `constructor` to `create` and `initialize` new `instances` of the `class`
  * `Provides` a way to `store` and `access` fields on `instances`
  * ``Defines`` a set of `methods` shared by all `instances` of the `class` that operate on each instances’ `state`.
* `Declare` a class
  * The `body` of a `class` contains its `methods` and `field`.
  * When the class declaration is executed, creates a class object and stores that in a variable named after the class.
  *   ```java
        class Breakfast {
            cook() {
                print "Eggs a-fryin'!";
            }

            serve(who) {
                print "Enjoy your breakfast, " + who + ".";
            }
        }

        // Store it in variables.
        var someVariable = Breakfast;

        // Pass it to functions.
        someFunction(Breakfast);

        breakfast.meat = "sausage";
        breakfast.bread = "sourdough";
        ```
  * Freely add `properties` onto `objects`
    * `Assigning to a field creates it if it does not already exist`.
  * Define an initializer (`constructor`)
    * `ensuring` the `object` is in a `valid` state when it’s `created`.
    * called `automatically` when the `object` is `constructed`.
    * Any `parameters` passed to the `class` are forwarded to its `initializer`.
      *   ```java
            class Breakfast {
                init(meat, bread) {
                    this.meat = meat;
                    this.bread = bread;
                }

            // ...
            }

            var baconAndToast = Breakfast("bacon", "toast");
            baconAndToast.serve("Dear Reader");
            // "Enjoy your bacon and toast, Dear Reader."
            ```
* `Create` instances
* `Access` a field or method
  * On the current object from within a method: use `this` keyword
    *   ```java
        class Breakfast {
        serve(who) {
            print "Enjoy your " + this.meat + " and " + this.bread + ", " + who + ".";
        }

        // ...
        }
        ```

#### Inheritance

* `Reuse` method across `multiple classes` or `objects`
* `single inheritance`
  *   ```java
        class Brunch extends Breakfast {
            drink() {
                print "How about a Bloody Mary?";
            }
        }
        ```
  * `derived` class or `subclass`
  * `base` class or `superclass`
* `Every` method defined in the `superclass` is also `available` to its `subclasses`.
  *   ```java
        var benedict = Brunch("ham", "English muffin");
        benedict.serve("Noble Reader");
        ```
* Call a `method` on own `instance` without hitting own `methods`: use `super` keyword
* Every `instance` of a `subclass` is an `instance` of its `superclass` too, but there may be `instances` of the `superclass` that are `not instances` of the `subclass`.
  * => in the universe of objects, the `set of subclass objects` is `smaller` than the `superclass’s set`

#### Hash Table

* Hash table is `associates` a set of `keys` with a set of `values`.
* Each `key/value` pair is an `entry` in the `table`. 
  * Given a `key`, can look up its corresponding `value`. 
  * Can `add` new `key/value` pairs and `remove entries` by `key`. 
  * If `add` a new value for an `existing` key, it `replaces` the `previous entry`.
  * `Given a key, a hash table returns the corresponding value in constant time (regardless of how many keys are in the hash table)`.
* Hash function
  * get to the `hash` part of `hash table`.
  * A `hash function` takes some larger blob of data and `hashes` it to produce a fixed-size integer `hash code` whose value depends on all of the bits of the original data. 
  * A good hash function has three main goals:
    * `It must be deterministic`. 
      * The same input must always hash to the same number. 
      * If the same variable ends up in different buckets at different points in time, it’s gonna get really hard to find it.
      * `It must be uniform`. 
        * Given a typical set of inputs, it should produce a wide and evenly distributed range of output numbers, with a few clumps or patterns as possible. 
        * It scatters values across the whole numeric range to minimize collisions and clustering.
        * `It must be fast`. 
          * Every operation on the hash table requires to hash the key first. 
          * If hashing is slow, it can potentially cancel out the speed of the underlying array storage.
* Building a Hash Table
* Hashing strings

#### Error handling

* ErrorReporter
  * error()
  * report()
* Runtime Errors
  * Runtime errors are failures that the language semantics demand detects and report while the program is running (hence the name).
* Exception

