# Running C online

Use this when the computer doesn't have a compiler.

## 1. Pick a site

- [OnlineGDB](https://www.onlinegdb.com/online_c_compiler): lets you type input while it runs, and has a debugger.
- [Programiz](https://www.programiz.com/c-programming/online-compiler/): simple, and it also waits for input.
- [OneCompiler](https://onecompiler.com/c): you enter input before running.
- [Compiler Explorer](https://godbolt.org/): shows the machine code your C becomes. Fun from Week 2 onwards.

## 2. Paste your whole file

Include the `#include` lines and `main`, exactly as on your laptop.

## 3. Typing input

On OneCompiler, your program can't stop and wait for you to type. Put your answers in the **STDIN** box before pressing Run, one per line:

```
20
1.75
```

For games like Day 4's guessing game, use OnlineGDB or Programiz, which wait for input.

## Differences from your laptop

| On your laptop | On these sites |
|---|---|
| You run `gcc` then the program | You press Run |
| You choose the warnings with `-Wall -Wextra` | Some sites show fewer warnings |
| Files you write stay on disk | Files may disappear when you close the tab |
| You can use several `.c` files | Usually just one file |

Days 1–12 work fine online. From Day 13, you need several files, libraries or networking, so use your laptop.

Remember to copy your code somewhere before closing the tab, or it may be lost.
