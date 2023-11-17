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

# Script
To increase the ease of use, I have constructed a simple shell function that fetches the contents of a justfile in this repo and puts it in a local justfile in the current working directory of where the function is called.

```sh
just_get() {
  lang=$1

  if [ -z "$1" ]; then
    echo "Please specify the language of the justfile you are interesting in getting."
    return 1
  fi

  repo_url="https://raw.githubusercontent.com/andreaskrath/justfiles/master/$lang/justfile"
  content="curl -s $repo_url"

  if [ $? -eq 0 ]; then
    echo "$content" > justfile
    echo "Fetched $lang justfile and saved as 'justfile'."
    echo "Make sure to check the contents of the justfile, and make appropriate modifications if necessary."
  else
    echo "Could not fetch $lang justfile from the repository. Ensure that '$lang' is spelled correctly and matches a justfile in the repository."
  fi
}  
```

For example, to get the justfile for Rust, you can write `just_get rust`.

**Note:** the script uses `curl` to get the text from the justfile, and must therefore either be installed or replaced by a similar tool for the script to work - in the latter case the script would also require adjusting.

