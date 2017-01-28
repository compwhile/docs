| Title  | Requirments                 |
|--------|-----------------------------|
| Author | Collaborators               |
| Status | DRAFT                       |
| Date   | 2017-01-21                  |

## 1. Background
* compwhile is a web IDE for learning, visualizing and running computer
  programs.
* The project is open source, and it's goal is to enhance and level up your study of programming languages in Computability Theory course.
* compwhile aims to supprt WHILE and other theoretical languages presented in the book Computability and Complexity from a Programming Perspective (1997) by Neil Jones.
* MVP of this project: extensible web IDE for WHILE.

## 2. Features
* Edit your programs within a web IDE - no installation required.
* Syntax highlighting and error checking.
* Build and visualize the AST of your program.
* Execute your program.
* Write multiple programs using separate tabs.
* Save your program inside the web IDE to continue later.
* Visualize your input and output of trees.
* Solve programming exercises with immediate feedback.

## 3. Wireframe
![alt text](https://github.com/compwhile/docs/raw/master/wireframe.png "compwhile")

## 4. Widgets
* File structure widget
  * This widget includes a tree structure of all saved programs and exercises.
  * All programs and exercises can be saved with the "save all" button.
  * Top section - User programs
    * New program can be added with the "add program" button. A modal will be shown, and the user will need to input:
      * Program name.
      * Language (dropdown) - it will automatically add extension.
    * Left-Click on one of the programs, will affect all other widgets
      (including the exercise tab which will be disabled).
    * Right-Click on one of the programs, will open a dropdown menu with:
      * Rename - clicking rename will open the "add program" modal with updated values, but language as read-only field.
      * Delete - clicking delete will open a "are you sure?" modal. If approved,
        the program will be deleted.
  * Bottom section - Exercises
    * User cannot add new exercises.
    * Each exercise language is known from the extension (for example: ex01.while).
    * Left-Click on one of the exercises, will affect all other widgets
      (including the exercise tab which will be enabled).
    * Right-Click on one of the programs, will open a dropdown menu with:
      * Reset - clicking reset will open a "are you sure?" modal. If approved,
        the exercise will be returned to it's initial state.
* Code editing widget
  * Left panel of lines (extensible for future addons - ex: breakpoints).
  * Bottom panel for current line and column.
  * Right panel for code editing with syntax highlighting support and
    scrolling.
* Utilities
  * AST tab
    * Visualization of the AST (should be empty and include build button if no build has been done yet).
    * Collapse panel to show the concrete syntax tree.
  * Input/Output tab
    * Dropdown to select tree/list notation format.
    * Top section - Input
      * Editable tree/list notation
      * Interactive visualization (add / remove nils)
      * Shortcuts to create unary trees.
    * Bottom section - Output
      * Read only tree/list notation
      * Non-interactive visualization
  * Exercise tab
    * If the selected program is an exercise, this tab is enabled.
    * The tab includes:
      * Instructions for the exercise.
      * Output console for real time feedback (examples: build success / failed, tests failed, tests passed).
* Buttons widget
  * Save - save the current program in the browser.
  * Build - compile the current program.
  * Run - run the current program with selected input.
  * Space for future buttons (Debug, Step-In, Step-Out, etc.)
* Build output widget
  * Shows the output of the compiler after clicking Build in the Buttons
    widget.
  * Shows descriptive errors or build successfull messages.

## 5. Basic editing flow
* The user enters the compwhile.io website for the first time.
* A default program to be loaded into the user programs is "comp.while".
  * If there are no other user-programs, it will be the selected one.
  * If there are other user-programs (from previous use), the selected program will be the previously selected one.
* The user selects the program to work on via the File Structure widget.
* Once a program has been selected, all other widgets are affected.
* The user views and edits the source code in the Code Editing widget.
* The user setups the input for the program via the Utilities widget, Input
  tab.
* The user clicks the Build button in the Buttons widget and the Build output widgget is updated.
  * If an error occures, the user fixes the bug, then presses the Build button again.
  * If no error occured:
    * The message "Build succeeded" is displayed in the Build output widget, indicating the user can run the program.
    * The AST for that program can be viewed in the AST tab in the Utiliites
      widget.
* The user clicks the Run button.
  * I/O tab in the Utilities widget contains the output for the execution.
* The user saves the selected program by clicking Save in the Buttons widget.

## 6. Edge cases
* Run before build automatically triggers the build.
* Run without changing the default nil input will display a message.

## 7. v0.1.0 release
* First release will support only the WHILE lanaguage and it's core semantics:
  * Evaluation of expressions
  * Execution of commands
  * Variables and constants
  * Comments
  * Syntax sugar:
    * True / false
    * Partial if statement (of type command)
    * Lists
    * Inline procedure expansion
* Detailed requirements can be found in the [WHILE-interperter
  requirements](while-interperter/requirements.md) document.

## 8. Open questions
* The following features are open questions and (will) have a proposal in the
  proposals folder:
  1. WHILE syntax sugar: case statement
  2. Deubgger
  3. Share button
