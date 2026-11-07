# Week 1: Days 1–7

Do [SETUP.md](SETUP.md) first.

Every program this week starts like this:

```c
#include <stdio.h>

int main(void)
{
    // your code goes here

    return 0;
}
```

- `#include <stdio.h>` brings in `printf` and the other input and output functions.
- `main` is where the program starts. `return 0;` tells the system it finished without problems.
- Every statement ends with `;`, and blocks go inside `{ }`.

Compile with `gcc file.c -o file -Wall -Wextra`, then run `./file` (or `.\file` in PowerShell).

---

# Day 1: Printing and variables

**Goal:** a program that prints facts about you.

## `printf`

```c
printf("Hello\n");
printf("A");
printf("B\n");     // AB, then a new line
```

`\n` means new line. Without it, everything ends up on one line.

## Variables

In C, you must give every variable a **type**:

```c
int age = 20;            // whole number
double height = 1.75;    // decimal number
char initial = 'A';      // one character, in single quotes
```

There's no built-in text type. You'll meet strings properly on Day 6.

## Printing variables

`printf` uses **format specifiers** as placeholders:

```c
printf("Age: %d\n", age);
printf("Height: %f\n", height);      // 1.750000
printf("Height: %.2f\n", height);    // 1.75
printf("Initial: %c\n", initial);
printf("%c is %d\n", initial, age);  // several at once, in order
printf("Text: %s\n", "hello");       // a piece of text
```

| Specifier | Type |
|---|---|
| `%d` | `int` |
| `%f` | `double` |
| `%c` | `char` |
| `%s` | text (a string) |
| `%%` | a real `%` sign |

Using the wrong one, like `%d` for a `double`, prints rubbish. `-Wall` warns you about it.

## Comments

```c
// one line
/* several
   lines */
```

## Exercise: about me

Make variables for your age, your height in metres, and the first letter of your name. Print one line for each, with the height to 2 decimal places. Then print a sentence that uses all three.

| Variables | Expected result |
|---|---|
| 20, 1.75, `'A'` | `A is 20 years old and 1.75 m tall.` |

**Bonus:** print a box of `*` around your sentence, using `printf` for each line.

## Check yourself

1. What does `\n` do?
2. What specifier prints a `double` to 1 decimal place?
3. What's the difference between `'A'` and `"A"`?
4. What does `return 0;` mean at the end of `main`?

---

# Day 2: Input and maths

**Goal:** a tip calculator.

## Maths

```c
printf("%d\n", 7 + 2);     // 9
printf("%d\n", 7 / 2);     // 3: int divided by int drops the decimal
printf("%d\n", 7 % 2);     // 1: the remainder
printf("%f\n", 7.0 / 2);   // 3.500000
```

**`7 / 2` is `3` in C.** If both sides are `int`, the decimal part is thrown away. Make one side a `double` to keep it:

```c
int a = 7;
int b = 2;
double result = (double)a / b;   // 3.5: the cast converts a first
```

`(int)4.9` gives `4`. A cast cuts off, it doesn't round.

## Reading input with `scanf`

```c
int age;
printf("Age? ");
scanf("%d", &age);

double price;
printf("Price? ");
scanf("%lf", &price);
```

- Use `%d` for `int`, and **`%lf`** for `double` (with `scanf` only, `printf` uses `%f`).
- The **`&`** is required. It gives `scanf` the address of the variable, so it can store the number there. You'll understand why on Day 8. For now: forgetting `&` usually crashes the program.
- Typing `abc` for a number leaves the variable unchanged. You'll handle that on Day 4.

## Short forms

```c
total = total + 5;   // same as:
total += 5;

count = count + 1;   // same as:
count++;
```

## Exercise: tip calculator

Ask for the bill amount, the tip percentage and the number of people. Print the tip, the total and what each person pays, all to 2 decimal places.

| Bill | Tip % | People | Tip | Total | Each |
|---|---|---|---|---|---|
| 100 | 10 | 2 | 10.00 | 110.00 | 55.00 |
| 50 | 15 | 3 | 7.50 | 57.50 | 19.17 |
| 80 | 0 | 1 | 0.00 | 80.00 | 80.00 |

**Watch out:** if the tip percentage is an `int`, `15 / 100` is `0`. Make it a `double`.

**Bonus:** try 0 people. What prints? Look up `inf` in C.

## Check yourself

1. What does `7 / 2` give in C, and why?
2. What specifier does `scanf` need for a `double`?
3. What is the `&` in `scanf("%d", &age)` for?
4. What does `(int)9.99` give?

---

# Day 3: Decisions

**Goal:** a grade calculator.

## `if`, `else if`, `else`

```c
if (score >= 90)
{
    printf("A\n");
}
else if (score >= 80)
{
    printf("B\n");
}
else
{
    printf("Keep going\n");
}
```

The **first match wins**, so put the largest check first. Never put `;` straight after `if (...)`: `if (x > 3);` ends the `if` right there.

## Comparisons and logic

```c
x == 5      // equal (= assigns, == compares)
x != 5      // not equal
x >= 5      // also <, >, <=
age >= 13 && age <= 19   // and
day == 6 || day == 7     // or
!finished                // not
```

C has no `true` or `false` by default: `0` means false, and anything else means true. For proper `bool`, add `#include <stdbool.h>`.

**`if (x = 5)` compiles**, but assigns 5 and is always true. `-Wall` warns you about it.

## `switch`

```c
switch (choice)
{
    case 1:
        printf("Start\n");
        break;
    case 2:
    case 3:
        printf("Stop\n");
        break;
    default:
        printf("Unknown\n");
}
```

`switch` works on whole numbers and `char`s, not on text. **Forgetting `break` runs the next case too.** That's called fall-through.

## Exercise: grade calculator

Ask for a score from 0 to 100 and print the grade: 90+ is `A`, 80+ is `B`, 70+ is `C`, 60+ is `D`, and anything lower is `F`. Print `Invalid` for anything below 0 or above 100.

| Input | Expected result |
|---|---|
| 95 | A |
| 90 | A |
| 89 | B |
| 60 | D |
| 59 | F |
| 0 | F |
| 101 | Invalid |
| -5 | Invalid |

**Bonus:** a menu. Print `1. Add  2. Subtract  3. Quit`, read a number, and use `switch` to say what was picked. Remove one `break` and see what changes.

## Check yourself

1. What does C treat as false?
2. Why does `if (x = 5)` always run?
3. What happens if you forget `break` in a `switch`?
4. Why must `>= 90` come before `>= 80`?

---

# Day 4: Loops

**Goal:** a number guessing game.

## `for`: when you know how many times

```c
for (int i = 1; i <= 5; i++)
{
    printf("%d\n", i);
}
```

This prints 1 to 5. The three parts are the start, the check that keeps it going, and the step after each run.

## `while`: until something changes

```c
int lives = 3;

while (lives > 0)
{
    printf("Lives: %d\n", lives);
    lives--;
}
```

If you forget `lives--`, it never ends. Press **Ctrl+C** to stop it.

## `do`/`while`: run at least once

```c
int answer;

do
{
    printf("Type 1 to continue: ");
    scanf("%d", &answer);
} while (answer != 1);
```

## `break` and `continue`

```c
for (int i = 1; i <= 10; i++)
{
    if (i == 3)
    {
        continue;   // skip to 4
    }
    if (i == 6)
    {
        break;      // leave the loop
    }
    printf("%d ", i);   // 1 2 4 5
}
```

## Random numbers

```c
#include <stdlib.h>
#include <time.h>

srand(time(NULL));             // once, at the start of main
int secret = rand() % 100 + 1; // 1 to 100
```

`rand() % 100` gives 0 to 99, so `+ 1` makes it 1 to 100. Without `srand(time(NULL))`, you get the same "random" numbers every run.

## Checking that input worked

`scanf` returns how many values it read. If someone types `abc`, it returns 0, and the bad text stays waiting, so a loop asking again would spin forever. This clears it:

```c
if (scanf("%d", &guess) != 1)
{
    while (getchar() != '\n') { }   // throw away the rest of the line
    printf("Numbers only\n");
    continue;
}
```

## Exercise: number guessing game

1. Pick a secret number from 1 to 100.
2. Keep asking for a guess until the player gets it.
3. After each wrong guess, print `Too high` or `Too low`.
4. Count the guesses, and print the total when the player wins.

While testing, print `secret` at the start, and remove that line when you're done.

| Secret | Input | Expected result |
|---|---|---|
| 50 | 75 | Too high |
| 50 | 25 | Too low |
| 50 | 50 | You win, 3 guesses |
| 50 | abc | Numbers only, and the game carries on |

**Bonus 1:** give the player only 7 guesses, then reveal the number.

**Bonus 2:** ask `Play again? (1/0)` at the end, using `do`/`while` around the whole game.

## Check yourself

1. When would you pick `while` over `for`?
2. What range does `rand() % 6 + 1` give?
3. Why do you need `srand(time(NULL))`?
4. What does `scanf` return if the user types letters for `%d`?

---

# Day 5: Functions

**Goal:** split your code into reusable, named pieces.

## Writing a function

```c
#include <stdio.h>

int add(int a, int b);     // prototype: tells the compiler it exists
void greet(void);

int main(void)
{
    greet();
    int total = add(2, 3);
    printf("%d\n", total);
    return 0;
}

int add(int a, int b)
{
    return a + b;
}

void greet(void)
{
    printf("Hi\n");
}
```

- **Return type:** `void` returns nothing, and `int` promises to return an `int`.
- **Prototypes:** C reads top to bottom. If a function is defined below `main`, put its prototype (the first line plus `;`) above `main`. Without it, you get `implicit declaration of function`.
- `(void)` means the function takes no parameters.

## Arguments are copies

```c
void double_it(int n)
{
    n = n * 2;    // changes the copy only
}
```

Calling `double_it(x)` doesn't change `x`. To change the caller's variable you need a pointer, which is Day 8. For now, return the new value instead.

## Scope

A variable made inside a function or a `{ }` block only exists there. Two functions can each have their own `count` without clashing.

## Exercise: calculator

Write `add`, `subtract`, `multiply` and `divide`, each taking two `double`s and returning a `double`. Write `read_number(const char *prompt)`, which prints the prompt and returns the `double` the user types. (`const char *` is how C passes text. You'll learn why on Day 9.)

Then ask for two numbers and an operator, read it with `scanf(" %c", &op)`, use a `switch` to pick the function, and print the result to 2 decimal places.

The space before `%c` matters. It skips the Enter key still waiting from the last `scanf`.

| Input | Expected result |
|---|---|
| 6, +, 3 | 9.00 |
| 6, -, 3 | 3.00 |
| 6, *, 3 | 18.00 |
| 7, /, 2 | 3.50 |
| 6, /, 0 | See bonus |

**Bonus:** print a clear error instead of dividing by 0.

## Check yourself

1. Why do you need a prototype for a function defined below `main`?
2. Why doesn't `double_it(x)` change `x`?
3. What happens to code after `return` in the same block?
4. Why put a space in `scanf(" %c", &op)`?

---

# Day 6: Arrays and strings

**Goal:** work with lists of values and text.

## Arrays

```c
int scores[3] = {90, 75, 60};

printf("%d\n", scores[0]);   // 90: counting starts at 0
scores[1] = 80;

int count = sizeof(scores) / sizeof(scores[0]);   // 3

for (int i = 0; i < count; i++)
{
    printf("%d\n", scores[i]);
}
```

An array's size is fixed. **C doesn't check the index.** `scores[3]` here reads whatever happens to be next in memory, or crashes. It's your job to stay inside `0` to `count - 1`.

## Strings

A string is an array of `char` that ends with a hidden **`'\0'`** character, which marks the end.

```c
#include <string.h>

char name[] = "Alex";     // 5 chars: A l e x \0
printf("%s\n", name);
printf("%zu\n", strlen(name));   // 4: doesn't count the \0
printf("%c\n", name[0]);         // A
```

You can't use `=` or `==` on strings:

```c
char copy[20];
strcpy(copy, name);              // copy into it
if (strcmp(name, "Alex") == 0)   // 0 means equal
{
    printf("Same\n");
}
```

## Reading a line of text

```c
char line[100];
printf("Sentence? ");
fgets(line, sizeof(line), stdin);
line[strcspn(line, "\n")] = '\0';   // remove the Enter at the end
```

`fgets` keeps the `\n` from the Enter key, so the next line removes it. Don't use `scanf("%s")` for text: it stops at the first space.

**Mixing `scanf` and `fgets`:** `scanf("%d")` leaves the Enter behind, and the next `fgets` reads that empty line straight away. After a `scanf`, clear the line with `while (getchar() != '\n') { }`.

## Characters

```c
#include <ctype.h>

tolower('A');    // 'a'
toupper('b');    // 'B'
isalpha('7');    // 0: not a letter
isdigit('7');    // non-zero: a digit
isspace(' ');    // non-zero: a space
```

## Exercise: text analyzer

Read a sentence with `fgets`, then print:
1. The number of characters.
2. The number of words. Count each place where a non-space character follows a space or the start.
3. The number of vowels (a, e, i, o, u), counting capitals too.
4. The sentence reversed, with a `for` loop counting down.

| Input | Characters | Words | Vowels | Reversed |
|---|---|---|---|---|
| `Hello World` | 11 | 2 | 3 | `dlroW olleH` |
| `C is fun` | 8 | 3 | 2 | `nuf si C` |

**Bonus:** say whether the input is a palindrome, ignoring capitals. `Level` should say yes.

## Check yourself

1. What's the index of the last item in an array of 10?
2. What is `'\0'` for?
3. Why can't you compare strings with `==`?
4. Why does `fgets` need the `strcspn` line after it?

---

# Day 7: Project: console quiz game

No new topics today. You're combining everything, without a walkthrough.

## Requirements

1. Ask for the player's name with `fgets`, and remove the `\n`.
2. Store at least 5 questions and their answers in two arrays of strings, at matching positions:
   ```c
   const char *questions[] = {"Capital of France?", "2 + 2?"};
   ```
3. Loop through the questions and ask each one.
4. Compare answers while ignoring capitals. Write your own `same_ignoring_case` function, using `tolower`.
5. Say whether each answer was right, and show the correct one if not.
6. At the end, print the score and percentage to 1 decimal place.
7. Print a rank: 100% is `Perfect`, 60% or above is `Passed`, and anything else is `Try again`.
8. Use at least 2 functions of your own, such as `ask_question` and `print_rank`.

## Watch out

- `score / total * 100` with two `int`s gives 0 for most scores. Use `(double)score / total * 100`.
- An answer buffer like `char answer[100]` must be big enough for anything the player might type.

## Test it

| Scenario (5 questions) | Expected result |
|---|---|
| All correct | 100.0%, Perfect |
| 3 correct | 60.0%, Passed |
| 2 correct | 40.0%, Try again |
| All wrong | 0.0%, Try again |
| Answer typed as `PARIS` when correct is `Paris` | Counts as correct |

## Bonus

- Also ignore spaces at the start and end of the answer. Write a `trim` function.
- Ask whether to play again.

**Well done: that's Week 1.**
