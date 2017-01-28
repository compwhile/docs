| Title  | While interperter - Design        |
|--------|-----------------------------------|
| Author | Collaborators                     |
| Status | DRAFT                             |
| Date   | 2017-01-28                        |

## 1. Background
* compwhile support generic system to execute programms.
* A program in language `S` can be executed if it has an implementation of `S-plugin`.

## 2. Components of a language plugin
* **S-Parser**
    * **Goal**: Lexical analysis to create an AST for compilation and
      interpretation purposes.
    * **Input**: String of ASCII symbols.
    * **Output**: Abstract syntax tree.
* **S-Interperter**
    * **Goal**: Execute a program `p ∈ S-prog` on value `d ∈ S-data`.
    * **Input**: `p ∈ S-prog` and `d ∈ S-data`.
    * **Output**: The result of executing `p` on input `d`:  `〚p〛d`.

## 3. `parser.build(src)`
* The source code of the program is passed to the parser in the language plugin.
* The output of the build method is an AST of the source code to be used later
  by the interperter (at runtime).

## 4. `interperter.run(ast, input)`
* The AST of the program is passed to the interpeter in the language plugin
  with input.
* The output of the run method is the value of executing the abstract syntax
  tree `tree` on value `input`.

## 5. WHILE-plugin
* The WHILE-plugin will be implemented as part of release v0.1.0.
* The plugin contains the following components (implementing the generic
  definitions listed above):
    * WHILE-parser.
    * WHILE-interperter.
