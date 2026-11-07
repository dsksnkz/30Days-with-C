# Setup

You need a **C compiler** and an editor. This course uses **GCC** (or Clang, which accepts the same commands), so every system runs the same commands.

## Windows

Use **MSYS2**, which gives you GCC on Windows.

1. Install it from [msys2.org](https://www.msys2.org/), or in Terminal run: `winget install MSYS2.MSYS2`
2. Open **MSYS2 UCRT64** from the Start menu, and run:
   ```bash
   pacman -S mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-gdb make
   ```
   Press Enter to accept the defaults.
3. To use `gcc` from PowerShell or VS Code too, add `C:\msys64\ucrt64\bin` to your PATH:
   **Start → "Edit environment variables for your account" → Path → Edit → New**, paste the folder, then **OK**.
4. **Close and reopen Terminal.**

On Windows, compiled programs end in `.exe`. Run them with `.\hello` in PowerShell, or `./hello` in the MSYS2 shell.

**Alternative:** if you already use **WSL** (Linux inside Windows), follow the Linux steps inside it. WSL is also the easiest way to do Days 25–30, which use networking features that work differently on Windows.

## macOS

```bash
xcode-select --install
```

This installs Clang. On macOS, `gcc` is really Clang, and that's fine: every command in this course works with it.

## Linux

| Distribution | Command |
|---|---|
| Ubuntu, Debian, Mint | `sudo apt install build-essential gdb valgrind` |
| Fedora | `sudo dnf install gcc gdb make valgrind` |
| Arch | `sudo pacman -S base-devel gdb valgrind` |

## Check it worked

```bash
gcc --version
```

If you see a version number, you're ready.

## Pick an editor

**VS Code** works on every system. Get it from [code.visualstudio.com](https://code.visualstudio.com/), then install the **C/C++** extension. Any editor is fine, though: Notepad++, Neovim, CLion or Code::Blocks all work.

This course compiles from a terminal, which works the same everywhere. VS Code has one built in: **View → Terminal**.

## Your first program

Make a folder, and create `hello.c` in it:

```c
#include <stdio.h>

int main(void)
{
    printf("Hello, C\n");
    return 0;
}
```

Then compile and run it:

```bash
gcc hello.c -o hello -Wall -Wextra
./hello
```

`-o hello` names the program. `-Wall -Wextra` turns on warnings. Always use them.

## Git (for saving your work)

- **Windows:** `winget install Git.Git`, or download from [git-scm.com](https://git-scm.com/).
- **macOS:** it comes with `xcode-select --install`.
- **Linux:** install `git` with your package manager.

No compiler at all? See [ONLINE.md](ONLINE.md).
