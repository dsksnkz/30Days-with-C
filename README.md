# 30 Days with C

A 30-day C course, built to work with no AI help. Plan on 1–2 hours a day.

**Progress:** not started. **Next up: Day 1.**

## Where to go

| File | What it's for |
|---|---|
| [SETUP.md](SETUP.md) | Start here: install a C compiler on Windows, macOS or Linux |
| [WEEK1.md](WEEK1.md) | Full lessons for Days 1–7 |
| [ROADMAP.md](ROADMAP.md) | Goals, key ideas and exercises for Days 8–30 |
| [ERRORS.md](ERRORS.md) | What common compiler errors and crashes mean |
| [ONLINE.md](ONLINE.md) | Running C in a browser |
| [prompt.md](prompt.md) | A tutor prompt that gives hints, never answers |
| [my-code/](my-code/) | The code you write, one folder per day |

## Why C

C is small, fast and close to the machine. Linux, Windows, Python and most other languages are built on it. It doesn't protect you from mistakes, so you'll learn how memory really works. That makes every other language easier afterwards.

## Getting stuck without AI

Work through these in order:

1. **Read the first error.** Note the file, line and column, like `hello.c:5:12: error: ...`. Fix only that one, then compile again.
2. **Look it up** in [ERRORS.md](ERRORS.md).
3. **Check the line above too.** A missing `;` or `}` is often reported one line late.
4. **Read the warnings.** Always compile with `-Wall -Wextra`. In C, a warning is often a real bug.
5. **Use `printf`** to print your variables and see what they really hold.
6. **Search the message**, for example `C error: expected ';' before`. Good sources are [cppreference](https://en.cppreference.com/w/c) and Stack Overflow.
7. **Still stuck after 20 minutes?** Write down the problem, move on, and bring it back later.

## Starting each day

```bash
cd my-code
mkdir Day01
cd Day01
```

Write `lesson.c` in your editor, then compile and run it:

```bash
gcc lesson.c -o lesson -Wall -Wextra
./lesson
```

These commands work in Windows PowerShell, macOS and Linux. On Windows, the program is called `lesson.exe`, and `.\lesson` runs it.

Compile again every time you change the code. Running the old program shows the old behaviour.

## The daily routine

1. **Learn (20–30 min):** read the lesson and run the examples.
2. **Build (45–60 min):** do the exercise without copying.
3. **Test:** run every test value, especially the boundaries.
4. **Break it (10 min):** change something, read the error, and fix it.
5. **Answer the check-yourself questions** from memory.

## Saving your work

From the repo folder:

```bash
git add .
git commit -m "Finish Day 1"
git push
```

To get this repo on another computer:

```bash
git clone https://github.com/dsksnkz/30Days-with-C
```

## The plan

| Week | Topic | Project |
|---|---|---|
| 1 | Fundamentals | Console quiz game |
| 2 | Pointers, structs and memory | Library management system |
| 3 | Files and data structures | Expense tracker that saves its data |
| 4 | Professional tools: debugging, build systems, testing, networking | Tiny web server |
| Days 28–30 | Putting it all together | Task manager with a web interface |
