# C-Grep

A lightweight command-line text searching utility written in C that recursively scans files in a directory and searches for a specified pattern, similar to the Unix `grep` command.

## Features

* Recursive directory traversal
* Search for text patterns in all files within a directory tree
* Case-sensitive search (default)
* Optional case-insensitive search using `--ignore-case`
* Displays:

  * File name
  * Line number
  * Matching line content
* Simple and portable implementation using standard C libraries

---

## Requirements

* GCC or any C99-compatible compiler
* POSIX-compliant operating system (Linux, macOS, BSD)

---

## Compilation

Compile the program using GCC:

```bash
gcc -o cgrep cgrep.c
```

or with additional warnings enabled:

```bash
gcc -Wall -Wextra -O2 -o cgrep cgrep.c
```

---

## Usage

```bash
./cgrep <pattern> <directory> [--ignore-case]
```

### Parameters

| Parameter       | Description                                 |
| --------------- | ------------------------------------------- |
| `<pattern>`     | Text pattern to search for                  |
| `<directory>`   | Directory where the search begins           |
| `--ignore-case` | Optional flag for case-insensitive matching |

---

## Examples

### Search for a pattern

```bash
./cgrep printf ./src
```

Output:

```text
Found in ./src/main.c: Line 15: printf("Hello World\n");
```

---

### Case-insensitive search

```bash
./cgrep hello ./documents --ignore-case
```

Matches:

```text
Hello
HELLO
hello
HeLLo
```

---

## Project Structure

```text
project/
│
├── cgrep.c
├── README.md
└── sample/
    ├── file1.txt
    └── file2.txt
```

---

## How It Works

### 1. Directory Traversal

The function:

```c
search_in_directory()
```

Uses:

```c
opendir()
readdir()
closedir()
```

to recursively explore all subdirectories.

---

### 2. File Processing

The function:

```c
search_in_file()
```

Reads each file line-by-line using:

```c
fgets()
```

and searches for the specified pattern.

---

### 3. Case-Insensitive Matching

When the `--ignore-case` option is used:

* Both the search pattern and the current line are converted to lowercase.
* Matching is performed using:

```c
strstr()
```

---

## Example Output

```text
Found in ./src/main.c: Line 23: int main() {
Found in ./src/utils.c: Line 45: main_buffer = malloc(1024);
Found in ./tests/test.c: Line 12: test_main();
```

---

## Limitations

* Maximum line length: 1024 characters
* Uses `d_type` from `struct dirent`, which may not be supported on some filesystems
* Does not support regular expressions
* Does not support whole-word matching
* Does not support binary files
* Does not highlight matching text

---

## Possible Improvements

Future enhancements may include:

* Regular expression support
* Match counting
* Colored output
* Whole-word matching
* File extension filters
* Binary file detection
* Parallel file scanning using threads
* Context lines before/after matches
* Output statistics

Example:

```bash
./cgrep --count TODO ./project
```

```text
12 matches found in 5 files
```

---

## Exit Codes

| Code | Meaning                                             |
| ---- | --------------------------------------------------- |
| 0    | Successful execution                                |
| 1    | Error (invalid arguments, file access issues, etc.) |

---

## License

This project is released under the MIT License.

---

## Author

Simple recursive grep implementation written in C for educational purposes and command-line text searching.
