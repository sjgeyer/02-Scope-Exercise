
#### Questions:
1. When this code is run in Node, e.g. `node index.js`, what are the two stages of execution for this file called, and which order do they happen in?

    - *The two stages of execution are creation (or compilation) and execution. Creation happens before execution.*

2. Write an explanation, using as much space as you need, relating to how the first stage of execution for this file operates.
    - *The creation phase is where all the variables and functions are hoisted and saved in memory space. At this point, only the names of the variables/functions are hoisted, not their assignments (with the exception of function declarations, which get their definition hoisted as well). For index.js specifically, the code run at this point is equivalent to:*
        - *var foo; (global)*
        - *function bar () {...}*
        - *var foo; (inside bar)*
        - *function baz () {...}*
        - *foo; (inside baz)*

3. Write an explanation, using as much space as you need, relating to how the second stage of execution for this file operates.
    - *The execution phase is where all variable/function assignments occur. For index.js, the code run at this point is equivalent to:*
        - *foo = 'bar'; (global)*
        - *bar = [Function], executes function*
        - *foo = 'baz'; (inside bar, shadows global foo)*
        - *baz = [Function], executes function*
        - *foo = 'bam'; (inside baz)*
        - *bam = 'yay'; (in use strict, will throw error because bam is not a defined variable)*
        - *looking for foo --> will be 'bar'*
        - *looking for bam --> error*
        - *looking for baz() --> error*

4. During the second stage of execution how many scopes have been registered by the engine?
    - *There are three scopes registered by the engine: global, bar, and baz.*
    - Which segments of the code do they belong to?
        - *Global scope includes lines 1-5 and 14-19.*
        - *Bar scope includes lines 6-8 and 12-13.*
        - *Baz scope includes lines 9-11.*
    - Please identify any variables/refs and which scope each belongs to?
        - *foo = 'bar' is global, foo = 'baz' is in the bar scope, and foo = 'bam' is in the baz scope.*
        - *bar() is in the global scope*
        - *baz() is in the bar scope*
        - *bam is not defined anywhere*

5. When line 13 invokes the `baz` function, which `foo` will be assigned a value of `bam`? More specifically, `bam` will be assigned to the `foo` in ??? scope. Give a brief description in your own words to support your conclusion.
    - *'bam' will be assigned to the 'foo' in the bar scope, because the foo in the bar scope is shadowing the 'foo' in the global scope. Baz only exists in the scope of 'bar', and foo is assigned to 'baz' within that scope.*

6. Which scope, if any, will the variable `bam` on line 11 be registered to when the first stage of execution occurs on this file? Provide a brief description in your own words to support your conclusion.
    - *'bam' will not be registered to any scope because this code is running in strict mode and bam is not declared anywhere. If bam was declared, it would be registered to the scope of baz. If the code was not running in strict mode, bam would be registered to the global scope, because the engine would create the variable after not finding the declaration in any of the lower scopes.*

7. For each line, 16 through 19, what is the return value for each?
    - *Line 16: returns 'undefined'*
    - *Line 17: returns 'bar'*
    - *Line 18: returns an error, 'bam is not defined'*
    - *Line 19: returns an error, 'baz is not defined'*