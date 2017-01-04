| Title  | Debugger Support            |
|--------|-----------------------------|
| Author | Collaborators               |
| Status | DRAFT                       |
| Date   | 2017-01-04                  |


# Introduction

The debugger is one of the key features inside an IDE. 

Our goal is to implement source-level debugger, which is a challenge.
Source-level debugger means the developer can control the flow of
execution (e.g., breakpoints)  on the source code itself.

Key features for a useful debugger:

* Variable resolver with 'watch' capability
* Expression interpreter
* Step by step execution
* For functions support in a programming language: step-into, step-over
* Breakpoints and conditional breakpoints

When we talk about a debugger, we can identify two different components:
* Debugger **engine**
  * Implemented per programming language.
  * Input: AST object.
  * Exposes methods that implement a well-defined interface.
* Debugger **front-end**
  * Should be agnostic to the underlying engine via the well-defined interface.
  * Can be implemented once inside the web codebase.
  * Communicates with the developer via DOM events.
  * In response to DOM events, controls the execution flow of the engine
    via the well-defined interface.

# Interface between engine & front-end

One way to define the interface between the engine component and the front-end
component is to make it very similar to the popular GDB (GNU Debugger), which
is the standard debugger for the GNU operating system and works for many
programming languages like C&C++.

# API definition

**TBD**


# Debugger front-end

The debugger front-end can be implemented once as a web component that
communicates with a debugger engine that implements the well-defined interface.

This way, the same debugger front-end can be used to debug programs written
in various programming languages.

Since the debugger is a web component, it makes sense to learn from Google's
Chrome DevTools Debugger front-end.

Core features:

* Set breakpoints and conditional breakpoints
* Investigate the values of variables
* Step through the code:
  * Resume (run the code until next breakpoint or exit)
  * Relevant for programming languages with functions support:
    * Step over
    * Step into
    * Step out
    * Call stack


## References

* http://www.yolinux.com/TUTORIALS/GDB-Commands.html
* https://developer.chrome.com/devtools
* https://github.com/ChromeDevTools/devtools-frontend
