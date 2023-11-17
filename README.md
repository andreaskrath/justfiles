# Purpose
Oftentimes the same commands are useful regardless of which language you are working in. The idea behind this repository is to provide multiple different **justfiles** to help provide a consistent developer experience regardless of which language you are working with.

However, it is also important to emphasize that this idea does not translate well to every single programming language, and are therefore intended for a subset of programming languages.

# Framework
The intention is for each `justfile` to provide a shared set of commands, as well as more language specific commands that may be useful.

The shared commands are:
- **run** - executes the program
- **build** - builds the program (in debug/non-optimized mode)
- **test** - executes the test cases for the project

There are also two additional shared commands, which are only defined for some languages:
- **bench** - runs benchmarks for the project
- **doc** - generates documentation and opens it in a browser

The reason why these latter two commands are only available in some languages, is because the language must provide some constructs to help facilitate this command in a meaningful way.
For example, Golang and Rust provides a `bench` command in their compiler, meaning the justfile for these languages would contain a `bench` command.

# Modification
It is important to mention and emphasize that these justfiles use extremely generic commands, and when appropriate you should modify the contents of the justfile to better fit the project you are working on.

