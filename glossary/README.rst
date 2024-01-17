Glossary
========

Here is a concise glossary of computer science terms meant to be read in
order. In some cases, a narrow definition is given for simplicity's
sake.

Bit
    A **binary** digit. The smallest unit of information represented by one
    of two states (usually 0 or 1).

Binary
    A base 2 positional numeral system in which each **bit** position
    denotes a power of 2. k bits of information can represent 2 to the
    power of k different numbers. For example, using 3 bits (so 8
    possible combinations) you can count from 0 to 7: 000, 001, 010,
    011, 100, 101, 110, 111.

Hexadecimal
    A base 16 positional numeral system often used to represent four
    **bits**. **Hexadecimal** uses digites to represent values from 0 to
    9, and letters (from "A" to "F") to represent values from 10 to 15.
    For example, a **byte** can have values ranging from 00000000 to
    11111111 (0 to 255 decimal) in **binary** form, which can be
    conveniently represented as 00 to FF in hexadecimal.

Byte
    8 bits. A **byte** usually represents a character. For instance,
    "01000001" represents the letter "A".

File
    A sequence of **bytes** stored under a **filename**.

Filename
    A name used to identify a **file** in a **file system**.
    **Filenames** may include an extension which indicates the file's
    format (e.g., ".txt" for plain text, ".pdf" for Portable Document
    Format, etc.).

File system
    A structure used by **operating systems** to control how data is
    stored and retrieved. Most file systems are organized into a single
    inverted tree of **directories** similar to a genealogical tree.

Directory
    A cataloging structure which contains references to **files** and
    **directories**. Also known as "folder".

Root directory
    The first or top-most **directory** in a hierarchy. Conventionally
    referred to as "/".

Pathname
    The full name of the **path** from the **root** through the tree of
    **directories** to a particular **file**. The slash character
    separate the components of the name. For example: "/usr/bin".

Absolute path
    A **path** that begins at the **root** of the **directory** tree.
    Paths that start with a slash are always **absolute**.

Relative path
    A **path** that is **relative** to the **working directory**.

Working directory
    The **directory** associated with the current process.

Unix
    A family of **operating systems** that derive from the original
    Unix, whose development started in 1969 at the Bell Labs research
    center. Linux and Mac are descended from Unix.

Operating system (OS)
    A **program** that controls the resources of a computer. An **OS**
    lets users run programs; it controls the peripheral devices (discs,
    terminals, printers, and the like) connected to the machine; and it
    provides a **file system** that manages the long-term storage of
    information such as programs, data, and documents.

Program
    A set of instructions that the computer executes (or "runs") to
    achieve a particular objective. Technically, programs are **files**
    with execute permission. Programs can be **compiled** or
    **interpreted**.

Compiled program
    A **program** written in **machine code**. **Compiled programs** are
    most often translated from **source code** by a compiler. For
    example, programs written in the C **programming language** are
    compiled.

Interpreted program (or script)
    A **program** written in an interpreted or scripting **programming
    language**, such as JavaScript or Python. Interpreted programs are
    not translated into **machine code** before being executed. Instead,
    an interpreter translates and executes **source code** line by line.

Machine code
    **Binary** representation of a computer **program**.

Source code
    Text written in a human-readable **programming language**. Source
    code is written using a **text editor**.

Programming language
    A system of notation for writing computer **programs**.

Text editor
    A **program** that can edit **plain text** files. **Text editors**
    have a graphical **interface** (e.g., Visual Studio Code) or a
    **command-line** interface (e.g., Vim).

Plain text
    Text without styling information such as color, size, font, etc.

Interface
    How two or more things interact. In particular, how humans interact
    with machines (user interface), or how parts of a **program**
    exchange information.

Command-line
    A text-based **user interface** used to interact with an **operating
    system** by typing commands into a **terminal**. Commands are
    **interpreted** by a **shell**.

Terminal (or console)
    Typically synonymous with "terminal emulator": a program that allows
    users access to the **command-line interface**.

Shell
    A **program** that **interprets** and passes commands to an
    **operating system**. There are many differents **shells**: sh,
    bash, dash, zsh, fish, etc.