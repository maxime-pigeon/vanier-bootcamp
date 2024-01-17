# Command-line

> A command line is the simplest of interfaces, yet also the most
> challenging.
>
> Daniel J. Barrett

The services of an operating system are generally exposed to users
through interfaces, either graphical (GUI) or command-line-based (CLI).
While graphical user interfaces are easier to learn, they are
fundamentally restricted in what they allow you to do. A GUI must be
designed and programmed in advance to address a specific need. To freely
access and combine all the tools a computer provides, we must use a
CLI.

## Shell

A shell is a type of CLI. More precisely, it is a *command interpreter*
used to pass commands to an operating system. There are many differents
shells (sh, bash, dash, zsh, fish, etc.), but they are all programmed to
repeat the following steps over and over:

- Print a prompt.
- Read a command.
- Evaluate and run the command.

## Prompt

When you launch a shell, you will see a prompt that commonly appears
like this:

```sh
maximepigeon:~$
```

The prompt is the primary means of interacting with the shell. Typically,
it includes your username (e.g., maximepigeon) and the current working
directory (~), followed by a prompt sign ($).

In the following examples, input and output are differentiated by the
presence or absence of a prompt sign. For brevity, we will exclude the
username and working directory. When copying code, the prompt sign
should be omitted.

## Commands

A prompt *prompts* you to type *commands*, which are requests that the
shell will interpet. When you see the prompt, type your command and
press RETURN:

```sh
$ date
Tue 16 Jan 2024 17:26:39 EST
$
```

Most commands execute programs (in the following sections, "command" and
"program" are used interchangeably). Here, we instructed the shell to
execute the `date` program, which prints the current date and time. The
shell read our command, evaluated it, and printed the result on the next
line. Then, it prompted us for another command to execute. Read,
evaluate, print, read, evaluate, print... This loop is how you work with
the shell.

If you make a mistake typing the name of a command, and refer to a
non-existent command, you will be told that no command of that name can
be found:

```sh
$ datee
-bash: datee: command not found
```

### Arguments

We can also execute commands with *arguments*:

```sh
$ echo hello
hello
```

In this case, we instructed the shell to execute the `echo` program with
the argument `hello`. The `echo` program is a simple utility that prints
out the arguments provided to it.

### Quoting and Escaping

The shell parses commands by breaking down its input at whitespace. The
first word represents the program's name. Subsequent words are
treated as arguments.

If an argument needs to include spaces or special characters (e.g.,
'hello world'), you can enclose it in quotes (' or "), or you can escape
specific characters with a backslash (e.g., hello\ world).

## Navigation

### Current Working Directory

Shells keep track of the current working directory as part of their
internal state. To print the current working directory, execute the
command `pwd` (print working directory):

```sh
$ pwd
/Users/maximepigeon
```

You might be wondering why the output is different from the prompt,
which also displays the current working directory. In this case
"/Users/maximepigeon" is the *home directory*: the default location for
a user's personal files and settings. The tilde symbol (~) is a
shorthand for the home directory.

### Changing directory

The command `cd` (change directory) is used to navigate from one
directory to another. It takes as argument the path of the directory you
wish to navigate to. For example:

```sh
$ cd /Users
$ pwd
/Users
```

The `cd` command accepts both absolute and relative paths. Relative
paths are calculated from the current working directory. Paths can also
include the `.` (dot) and `..` (dot dot) symbols. The former refers to
the current directory, while the latter is a shorthand for the parent
directory. Executing `cd` without arguments always brings you back to
the home directory.

### Listing entries

Another useful command is `ls` (list). Unless a directory is given as
its first argument, `ls` prints the contents of the current directory:

```sh
$ ls
Applications    Library
Desktop         Movies
Developer       Music
Documents       Pictures
Downloads       Public
```

By combining the `pwd`, `cd` and `ls` commands, you should now be able
to navigate the file system using only the shell.

## File and Directory Manipulation

The shell also defines commands to manipulate files and directories.

### Creating

For instance, the `touch` command creates new files, while the `mkdir`
command is used to make new directories:

```sh
$ mkdir example
$ cd example
$ touch hello.txt
$ ls
hello.txt
```

### Moving and renaming

It is possible to move and rename files and directories. The `mv`
command takes, as its first argument, the current path of the entry you
wish to manipulate and, as its second argument, the new path you wish to
assign to the entry:

```sh
$ mv hello.txt bye.txt
$ ls
bye.txt
$ mkdir greetings
$ mv bye.txt greetings/bye.txt
$ ls
greetings/
$ ls greetings/
bye.txt
```

### Copying and removing

Other handy commands to know are `cp` to copy files and directories, and
`rm` to remove them. However, be careful with `rm` as you can easily
delete the content of your entire file system without being able to undo
it. It is recommended to test `rm` commands with `ls` before executing
them.

## Flags and options

Most commands accept flags and options that modify their behavior.
Flags are boolean arguments that start with either one or two hyphens
(-, \-\-). Options are similar to flags, but they accept values.

One of the most important flag to remember is `-h` or `--help`, which
prints a command's usage, what arguments it accepts, and what flags or
options are available:

```sh
$ mv -h
usage: mv [-f | -i | -n] [-hv] source target
       mv [-f | -i | -n] [-v] source ... directory
```

## Documentation

Not all commands provide the help flag. Depending on your distribution,
the built-in commands `ls` and `cd` do not. Fortunately, the shell has
other ways to get assistance. The `man`, `help`, and `info` commands
typically display the documentation of the command provided as an
argument.

```sh
example $ help cd
cd: cd [-L|-P] [dir]
    Change the current directory to DIR.  The variable $HOME is the
    default DIR.  The variable CDPATH defines the search path for
    the directory containing DIR.  Alternative directory names in CDPATH
    are separated by a colon (:).  A null directory name is the same as
    the current directory, i.e. `.'.  If DIR begins with a slash (/),
    then CDPATH is not used.  If the directory is not found, and the
    shell option `cdable_vars' is set, then try the word as a variable
    name.  If that variable has a value, then cd to the value of that
    variable.  The -P option says to use the physical directory structure
    instead of following symbolic links; the -L option forces symbolic links
    to be followed.
```

## Connecting programs

You may have noticed that the programs we have discussed so far are
relatively simple. They only do one thing: listing entries (`ls`),
printing arguments (`echo`), making directories (`mkdir`), etc. In fact,
"make each program do one thing well" is a fundamental aspect of the
Unix philosophy, and of the shell in general.

The shell's flexibility comes from its ability to connect these small
programs together through streams of text called STDIN (standard input)
and STDOUT (standard output). By default, STDIN corresponds to text
entered via the keyboard, and STDOUT to text printed on screen, but the
shell allows us to redirect those streams so that the output of program
becomes the input of another.

### Redirecting input

The simplest form of redirection is to send a program's output to a
file, instead of printing it on screen. To do so, we use the
*redirection operator* `>`, which overwrites the file's content, and the
operator `>>` which appends to it:

```sh
$ echo 3 > num.txt
$ echo 1 >> num.txt
$ echo 2 >> num.txt
$ cat num.txt
3
1
2
```

The `cat` command, as used above, concatenates files; it prints the
content of each file provided as an argument to the output stream. In
this example, we utilize it to display the content of "num.txt", which
now holds the output of the `echo` commands.

### Redirecting output

Similarly, STDIN can be redirected using the `<` operator. Take the `sort`
command as an example; it sorts its input by line. Rather than manually
typing text, we can redirect the input of `sort` to sort the content of
the "num.txt" file instead:

```sh
$ sort < num.txt
1
2
3
```

### Pipelines

We've discussed redirecting the shell's standard input and output to
files, but what about redirection from one program to another? For this
purpose, we utilize *pipes*. The `|` (pipe) operator allows you to
"chain" programs, making the output of one become the input of another.

For instance, the `find` command traverses a specified directory tree,
listing each path it contains. Another command, `grep`, scans the input
stream for lines matching a given pattern. By combining these commands,
we can display the paths of all files in the "example" directory that
have a '.txt' extension:

```sh
$ find . | grep .txt
./greetings/bye.txt
./num.txt
./hello.txt
```

Of course, we can connect more than two programs together. The `wc`
command displays the number of lines, words, and bytes contained in the
input stream. To know how many plain text files there is in the
"example" directory, we can pipe the output of `grep` to `wc`:

```sh
$ find . | grep .txt | wc -l
       3
```

## Variables

The shell can define variables and assign values to them. A shell
variable is like a variable in algebra; it has a name and a value. An
example is the shell variable `HOME`. Its value is the path to your home
directory.

To evaluate a variable, place a dollar sign ($) in front of the name:

```sh
$ echo $HOME
/Users/maximepigeon
```

### Environment variables

Variables like `USER` and `HOME` are predefined by the shell. Their
values are set automatically when you log in. Such predefined variables
are called "environment variables" and have uppercase names.

#### PATH

One important environment variable is `PATH`. When the shell first
encounters a simple command, such as `cat hello.txt`, it's just a string
of meaningless characters. Quick as a flash, the shell splits the string
into two words, "cat" and "hello.txt". In this case, the first word is
the name of a program on disk, and the shell must locate the program to
run it.

The program `cat`, it turns out, is an executable file in the directory
"/bin". You can verify a program's location with the command `which`:

```sh
$ which cat
/bin/cat
```

How does the shell know to locate `cat` in the "/bin" directory? Behind
the scenes, the shell consults a prearranged list of directories that it
holds in memory, called a *search path*. The list is stored as the value
of the environment variable `PATH`:

```sh
$ echo $PATH
/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

Directories in a search path are separated by colons (:). For a clearer
view, convert the colons to newline characters by piping the output to
the `tr` command, which translates one character into another:

```sh
$ echo $PATH | tr : "\n"
/opt/homebrew/bin
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```

The shell consults directories in your search path from first to last
when locating a program like `cat`. To install new programs, you need
only place their executable file in a directory included in the search
path.

## Resources

- [The Missing Semester of Your CS Education. Course overview + the shell.](https://missing.csail.mit.edu/2020/course-shell/)
- [Daniel J. Barrett. Efficient Linux at the Command Line.](https://www.oreilly.com/library/view/efficient-linux-at/9781098113391/)
- [GNU. Bash Reference Manual.](https://www.gnu.org/software/bash/manual/bash.html)
- [Brian W. Kernighan, Rob Pike. The UNIX Programming Environment.](https://archive.org/details/UnixProgrammingEnviornment)