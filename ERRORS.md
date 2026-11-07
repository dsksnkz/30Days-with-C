# Common errors

An error looks like this: `hello.c:5:12: error: expected ';' before 'return'`. That's the file, line 5, column 12, and the message.

**Fix the first error first.** One mistake can cause many errors further down. **Errors** stop the build. **Warnings** don't, but in C they're very often real bugs, so fix them too.

C also has a third kind of problem: code that compiles and then **crashes or gives random results**. That's covered at the bottom.

## Setup problems

| Message | Fix |
|---|---|
| `'gcc' is not recognized` (Windows) | Add `C:\msys64\ucrt64\bin` to PATH (see [SETUP.md](SETUP.md)), then reopen Terminal |
| `gcc: command not found` (macOS, Linux) | Install the compiler. See [SETUP.md](SETUP.md) |
| `./hello: No such file or directory` | It didn't compile, or you're in the wrong folder. Check for errors, then run `ls` |
| `'.' is not recognized` (Windows cmd) | Use `hello` or `.\hello` in cmd and PowerShell |
| The old version still runs | You forgot to compile again after saving |

## Compiler errors

| Message | What it usually means | Fix |
|---|---|---|
| `expected ';' before ...` | Missing semicolon | Add `;` at the end of the line above |
| `expected '}' at end of input` | A `{` was never closed | Match up your braces; indenting helps |
| `'x' undeclared` | A typo, or it's out of scope | Check spelling, and that it's inside the right `{ }` |
| `implicit declaration of function 'printf'` | A missing `#include` | Add `#include <stdio.h>` (or `<string.h>`, `<stdlib.h>`...) |
| `implicit declaration of function 'add'` | Your function is defined below `main` | Add a prototype above `main` |
| `redefinition of 'x'` | You declared the same variable twice | Remove the type from the second one |
| `conflicting types for 'add'` | The prototype and the function don't match | Make them the same |
| `too few arguments to function` | Calling it with the wrong number of arguments | Match the parameters |
| `assignment to expression with array type` | `name = "Alex";` on a `char` array | Use `strcpy(name, "Alex");` |
| `undefined reference to 'sqrt'` | A linker error: a library is missing | Add `-lm` at the end of the gcc command |
| `undefined reference to 'main'` | No `main`, or a typo in it | Check for `int main(void)` |
| `multiple definition of ...` | The same function is in two files | Put only prototypes in `.h` files |

## Warnings to never ignore

| Warning | Meaning |
|---|---|
| `format '%d' expects argument of type 'int', but argument has type 'double'` | Wrong `printf` or `scanf` specifier. See Day 1 |
| `format '%d' expects argument of type 'int *'` | You forgot the `&` in `scanf` |
| `suggest parentheses around assignment used as truth value` | `if (x = 5)`. You meant `==` |
| `'x' is used uninitialized` | The variable holds random rubbish. Give it a value |
| `control reaches end of non-void function` | A path through your function has no `return` |
| `comparison of integer expressions of different signedness` | Comparing `int` with `size_t`. Usually harmless, but check for negative values |
| `unused variable 'x'` | Often a scope mistake or a typo |

## Crashes while running

| Symptom | Common causes | How to find it |
|---|---|---|
| `Segmentation fault` | Using a `NULL` pointer, an index past the end of an array, a missing `&` in `scanf`, or using memory after `free` | Compile with `-g -fsanitize=address` and run again: it prints the exact line. Or use `gdb` (Day 22) |
| `Floating point exception` | Dividing an `int` by 0 | Check before dividing |
| `double free or corruption` | Calling `free` twice on the same pointer, or writing past the end of a `malloc` block | Set pointers to `NULL` after `free`, and check sizes |
| `stack smashing detected` | Writing past the end of a local array, often a string | Use `fgets` and `snprintf` with `sizeof` |
| Program waits forever | `scanf` is waiting for input, or an infinite loop | Press Ctrl+C. Check the loop condition |

## Compiles but gives the wrong answer

| Symptom | Likely cause |
|---|---|
| A decimal result comes out as 0 | `int / int`. Cast one side to `double` |
| A number is huge or random | The variable was never given a value, or a wrong specifier |
| `%f` prints 0.000000 for a number you read | You used `%f` instead of `%lf` in `scanf` |
| A `switch` runs several cases | A missing `break` |
| An `if` always runs | `=` instead of `==`, or a `;` straight after `if (...)` |
| A loop never ends on bad input | `scanf` failed and the bad text is still waiting. See Day 4 |
| `fgets` reads an empty line | A `scanf` left the Enter behind. See Day 6 |
| String comparison never matches | You used `==`. Use `strcmp(a, b) == 0` |
| String has a strange extra character | Missing `'\0'`, or the `\n` from `fgets` |
| A loop runs one time too many | `<=` where you meant `<` |
| A function doesn't change your variable | Arguments are copies. Pass a pointer (Day 8) |
