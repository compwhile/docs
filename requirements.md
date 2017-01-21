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
## 2. Features
* Edit your programs within a web IDE - no installation required.
* Syntax highlighting and error checking.
* Build and visualize the AST of your program.
* Execute your program.
* Write multiple programs using separate tabs.
* Save your program inside the web IDE to continue later.
* Visualize your input and output of trees.
* Solve programming exercises with immediate feedback.
## 3. Widgets
* File structure widget
  * This widget includes a tree structure of all saved programs and exercises.
  * Top section - User programs
    * All programs can be saved with the "save all" button.
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
      * Save - clicking rename will open the "add program" modal with updated values, but language as read-only field.
      * Reset - clicking delete will open a "are you sure?" modal. If approved,
        the program will be deleted.
* Code editing widget
  * Left panel of lines (extensible for future addons - ex: breakpoints).
  * Bottom panel for current line and column.
  * Right panel for code editing with syntax highlighting support.
* Utilities
  * AST tab
    * Visualization of the AST (should be empty and include build button if no build has been done yet).
    * Collapse panel to show the concrete syntax tree.
  * Input/Output tab
    * Change on one notation will affect all others.
    * Top section
      * Editable tree notation
      * Editable list notation
      * Interactive visualization (add / remove nils)
      * Shortcuts to create unary trees.
    * Bottom section
      * Read only tree notation
      * Read only list notation
      * Non-interactive visualization
  * Exercise tab
    * If the selected program is an exercise, this tab is enabled.
    * The tab includes instructions for the exercise, and output console for
      real time feedback (examples: build success / failed, tests failed, tests
      passed).
* Buttons widget
  * Save - 
  * Build
  * Run
  * Space for future buttons (Debug, Step-In, Step-Out, etc.)
* Build output widget
## 4. Editing Flow
* The user enters the compwhile.io website.
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
    * the user can run the program and the message "Build successeded" is displayed in the Build output widget.
    * The AST for that program can be viewed in the AST tab in the Utiliites
      widget.
* The user clicks the Run button.
  * I/O tab in the Utilities widget contains the output for the execution.
## 5. Other
* Run before build automatically triggers the build.
* Run with nil as input displays a message.
## 6. Open questions
* The following features are open questions and have a proposal in the
  proposals folder:
  * Deubgger
  * Share button
