| Title  | While interperter - Requirements  |
|--------|-----------------------------------|
| Author | Collaborators                     |
| Status | DRAFT                             |
| Date   | 2017-01-28                        |

## 1. Background
* WHILE is the first programming language to be supported from the first
  release of compwhile.
* The language is an imperative programming language, therefore its computation
  is driven forward by commands that are assignments to variables.
* So support this behaviour, the language has basic imperative programming constructs as well as a rich data type (binary trees).
* This requirements document is based on multiple sources, listed in the
  references section.

## 2. Expressions
* An expression of the WHILE-language has value, a binary tree.
* There are two ways to build an expression (constructors):
  * Empty tree - there is the expression `nil`.
  * Nonempty tree - there is the expressions `cons E F` where `E` and `F` are
    also expressions (denoting binary trees).
* There are two ways to disassemble an expression (destructors):
  * `hd` - short for "head". Disassemble an expression into its left (head)
    subtree.
  * `tl` - short for "tail". Disassemble an expression into its right (tail)
    subtree.
  * Both `hd` and `tl` do not have any effect on the empty tree (as it does not
    have any subtrees), so it will evaluate again to `nil`.

## 3. Commands
* There are four types of commands:
  * Assignment
  * Conditional (if-then-else)
    * This command uses a boolean guard to determine control flow.
  * While loop
    * Like conditional, this command also uses a boolean guard to determine control flow.
  * Sequential composition
    * This command allows to form statement blocks inside while loops and
      conditionals.
* Unlike expressions, commands do not produce a value, but have side effects on
  the variables as they can change their values.

## 4. Programs
* A program consists of:
  * Name.
  * Fixed read statement for passing the input.
    * The passing of the input is via a variable, which is called input
      variable.
  * Statement block.
  * Fixed write statement to return the output.
    * The passing of the output is via a variable, which is called output
      variable.
* All variables are set to `nil` except `X` which is set to the input value.
* Example of a program:

  ```
  p:  read X
        C
      write Y
  ```

  * Where:
    * `p` denotes any valid program name.
    * `X` denotes any valid variable name (the variable will store the input).
    * `Y` denotes any valid variable name (the variable will store the output).
    * `C` denotes a command.
  * Please note:
    * With the support of sequential composition, `C` can be a list of commands
      separated by semicolons.
    * The input variable and the output variable can be the same:

    ```
    p:  read X
          C
        write X
    ```

## 5. BNF (Backus-Naur-Forn) for WHILE
```
E, F ∈ Expression ::=    X
                       | d                     # constant tree
                       | hd E                  # left subtree
                       | tl E                  # right subtree
                       | cons E F              # construct tree

C, D ∈ Command ::=       X := E                # assignment
                       | C ; D                 # sequential composition
                       | while E do C          # while loop
                       | if E then C else D    # conditional

Program ::= read X ; C; write Y

X, Y ∈ Variable                                # contains an element of D
d ∈ D                                          # D is the set of all binary trees
```
* `X`, `Y` are identifiers consist of characters.
* While loops are executed as long as E is not equal to `nil`.
* With the conditional command, C is executed if E is not equal to `nil`,
  otherwise D is executed.

## 6. Supported syntax sugars
* Boolean values (of type constant, D)
  * `false` - the empty tree `nil`.
  * `true` - the tree `(nil.nil)`.
* Partial if statement (of type Command)
  * `if E then C` - the command `if E then C else X := X`.
* List (of type Expression)
  * `list E₁ E₂ E₃` - the expression `(cons E₁ (cons E₂ (cons E₃ nil)))` (can
    be any n elements).
* Inline procedure expansion
  * WHILE-programs can call *other* WHILE-programs by means of macro expansion.
  * Given a program `p`, the program `q` can use the command `B := <p> A`.
  * Please note:
    * Recursive self-calls is not permitted.
    * Two programs cannot have the same name.
    * A is of type Variable, NOT Expression.
  * If `X` and `Y` are the input and output variables in `p`, the interpreter will make a copy `pp` of the body of `p` where `X` and `Y` are replaced by `A` and `B`, respectively.
  * Furtheremore, all variables in `pp` and renamed so that no variable of `pp`
    other then `A` and `B` occurs in `q`.
  * To finish, this command will be replaced by the body of `pp`.
  * Example:

```
succ: read X
        X := cons nil X               # X := X + 1
      write X

pred: read X
        X := tl X                     # X := X - 1
      write X

add:  read L
        X := hd L;                    # X gets the first number
        Y := tl L;                    # Y gets the second number
        while X do                    # while (x > 0)
          X := <pred> X;              # remove 1 from X
          Y := <succ> Y               # add 1 to Y
      write Y
```

* Need to be decided if will be implemented in v0.1.0:
  - Case statement (pattern matching).

## 7. Concrete definitions for compwhile implementation
* Identifiers
  * No identifier begins with a number.
  * A valid program name should only include ... length ...
  * A valid identifier for a variable should only include ... length ...
* Comments
  * A line can begin with `#` to make that line a comment.
  * Inline-comments are supported, starting from `#` to the rest of the line.

**TBD**
## 8. Refereneces
1. Bernhard Reus, The WHILE-Language, Limits of Computation From a Programming
   Perspective (pp. 29-63), Spring (2016).
2. [Computability and Complexity from a Programming Perspective](http://www.diku.dk/~neil/Comp2book.html) (1997) by Neil Jones.
