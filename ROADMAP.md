# Roadmap: Days 8–30

Each day lists what to learn, the main ideas, and what to build. Look the topics up on [cppreference](https://en.cppreference.com/w/c) or in a good book like *C Programming: A Modern Approach* (K. N. King). Searching `C <topic name>` also works well.

Keep compiling with `-Wall -Wextra`. From Day 11, add `-g -fsanitize=address,undefined` while testing: it catches memory bugs the moment they happen. (On Windows with MSYS2, sanitizers aren't available. Use WSL for them, or rely on careful testing.)

## Week 2: Pointers, structs and memory

**Day 8: Pointers.** A pointer holds the address of another variable. Learn `&` (address of), `*` (the value at an address), and `NULL`. This is why `scanf` needs `&`.
```c
int x = 5;
int *p = &x;
*p = 10;        // x is now 10
```
**Build:** a `swap(int *a, int *b)` function that really swaps two variables, and `min_max(int arr[], int n, int *min, int *max)`, which hands back two answers through pointers.

**Day 9: Pointers and arrays.** An array name becomes a pointer to its first item. Learn pointer arithmetic (`p + 1`), why functions need the length passed with an array, `const`, and why strings are `char *`.
**Build:** your own `my_strlen`, `my_strcpy` and `my_strcmp` using pointers only, no `[ ]`. Compare their results with the real ones.

**Day 10: Structs.** Group related data into one type. Learn `struct`, `typedef`, the `.` and `->` operators, and arrays of structs.
```c
typedef struct
{
    char title[100];
    int year;
} Book;
```
**Build:** an array of 5 `Book`s. Print them all, find the oldest, and sort them by year with a simple loop.

**Day 11: Dynamic memory.** Learn the stack vs. the heap, `malloc`, `calloc`, `realloc` and `free`, and always checking for `NULL`. Every `malloc` needs exactly one `free`.
**Build:** ask how many numbers to store, `malloc` exactly that much, fill it, print the average, and `free` it. Run it with `-fsanitize=address`, or `valgrind ./program` on Linux, to prove nothing leaks.

**Day 12: Strings, safely.** Learn `strncpy`, `snprintf`, `strtok`, `strtol` and `strstr`. Learn what a **buffer overflow** is and why `gets` was removed from C.
**Build:** a `read_int(const char *prompt)` function using `fgets` and `strtol`, which keeps asking until it gets a valid number in range. You'll use it in every project from now on.

**Day 13: Multi-file programs and Make.** Split code into `.c` and `.h` files. Learn header guards, `static` functions, and compiling several files together. Write a `Makefile` so `make` builds everything.
**Build:** move your `Book` code into `book.h` and `book.c`, keep `main` in `main.c`, and build it with `make`.

**Day 14: Project: library management system.** A `Book` struct (title, author, borrowed or not) and a `Library` that holds a dynamic array of them, growing with `realloc`. Support adding, borrowing, returning, listing and searching. A book that's already borrowed can't be borrowed again. Use a menu loop and `read_int`, and make sure there are no leaks.

## Week 3: Files and data structures

**Day 15: File I/O.** Learn `fopen`, `fclose`, `fprintf`, `fscanf`, `fgets` on files, the modes `"r"`, `"w"` and `"a"`, and checking for `NULL` when a file is missing.
**Build:** a journal that adds a dated line to `journal.txt` each run, and can print every entry. Use `time` and `strftime` for the date.

**Day 16: Linked lists.** Each node holds data and a pointer to the next one. Learn insert at the front, insert at the end, delete, search, and freeing the whole list.
**Build:** a to-do list as a linked list with add, remove by number, and list. Check it for leaks.

**Day 17: Enums, unions and bits.** Learn `enum`, `union`, `switch` over an enum, and the bit operators `&`, `|`, `^`, `~`, `<<` and `>>`.
**Build:** a permissions checker that stores read, write and run as bits in one `unsigned int`, with functions to set, clear and test each one.

**Day 18: Function pointers and sorting.** A function pointer stores which function to call. Learn `qsort` with your own compare function, and `bsearch`.
**Build:** sort an array of `Book`s by title, then by year, using `qsort` and two compare functions. Search for a title with `bsearch`.

**Day 19: Hash tables.** Learn how a hash function turns a key into an index, and how to handle collisions with chaining.
**Build:** a word counter: read a text file, count each word in your own hash table, and print the 10 most common.

**Day 20: Binary files and command-line arguments.** Learn `int main(int argc, char *argv[])`, `fwrite` and `fread` for whole structs, and `"rb"` and `"wb"`.
**Build:** `copy source.txt dest.txt`, your own file-copying tool. Print a usage message if the arguments are wrong.

**Day 21: Project: expense tracker.** Add, list and delete expenses (date, category, amount), with totals per category. Save to a CSV file with `fprintf`, and load it on startup. Close the program, reopen it, and check that the data is still there. Handle a missing or broken file without crashing.

## Week 4: Professional tools

**Day 22: Debugging with GDB.** Compile with `-g`. Learn `break`, `run`, `next`, `step`, `print`, `backtrace` and `watch`. Find a segfault's exact line with `backtrace`. (On macOS, use `lldb`, whose commands are almost the same.)
**Build:** take three buggy programs (write them yourself, or break old ones on purpose) and find each bug using only the debugger, no `printf`.

**Day 23: Testing.** Learn `assert` from `<assert.h>`, how to write small test functions that return pass or fail, and testing edge cases: empty input, one item, the maximum size.
**Build:** a `test.c` for your expense tracker's functions, with a `make test` target that runs it.

**Day 24: CMake and libraries.** Learn `CMakeLists.txt`, `cmake -B build` and `cmake --build build`, which work on every system. Learn linking with `-l`, such as `-lm` for `<math.h>`.
**Build:** convert the library system from Make to CMake, and add a function that uses `sqrt` from the maths library.

**Day 25: SQLite.** Learn basic SQL (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) and the SQLite C API: `sqlite3_open`, `sqlite3_prepare_v2`, `sqlite3_bind_*`, `sqlite3_step`. Always bind values, never paste them into the SQL text.
**Build:** move the expense tracker from CSV to an SQLite database.

**Day 26: Sockets.** Learn what TCP is, and `socket`, `bind`, `listen`, `accept`, `recv`, `send` and `close`. On Windows, use WSL for this week: native Windows sockets (Winsock) work differently.
**Build:** an echo server that sends back whatever a client types. Test it with `nc localhost 8080` or `telnet`.

**Day 27: Project: tiny web server.** Read an HTTP request, work out the path, and reply with a proper status line (`200 OK` or `404 Not Found`) and headers. Serve `.html` files from a folder. Open it in your browser at `http://localhost:8080`.

## Final stretch: capstone

**Day 28: Design.** Plan a task manager that stores tasks in SQLite and has a web interface from your Day 27 server. Split it into `db.c`, `http.c`, `tasks.c` and `main.c`, with headers and CMake.
**Build:** the project structure, the database table, and the functions to add and list tasks.

**Day 29: Finish the features.** Add creating, listing, completing and deleting tasks from the browser, plus input checks and clear errors. Test every function, and run it with sanitizers to check for leaks and overflows.

**Day 30: Ship it.** Clean up the warnings, write a good README with build steps for Windows, macOS and Linux, and push it to GitHub.

**That's the course. Well done!**
