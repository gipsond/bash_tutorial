# `bash`/Linux Tutorial

by David Gipson

TA for Dr. Nandakumar's 422C

## The Shell

- Type command, hit `Enter` to execute
- This is the **B**ourne **A**gain **Sh**ell (`bash`)
  - Based on the Bourne **sh**ell (`sh`)
  - May also see alternatives: `zsh` or `ksh` ... or `fish`?
- `ssh` (**s**ecure **sh**ell)
  - `ssh USERNAME@kamek.ece.utexas.edu`

## Reading (navigating the file system)

![image](Linux%20Filesys.png)

### The home directory (`~`)

### Directories

- Each has a name
- Same as a "folder" on Windows
- Can contain files and directories
- Each file or directory is in a directory, except `/`.

### `ls` (**l**i**s**t)

- `-l` provides (**l**ong) details
- `-a` shows **a**ll files, including hidden "dotfiles"
- `-h` makes details, esp. file size, **h**uman-readable

### Files

- Contain binary data
- Like directories, have names
  - names can end in a **file extension** that indicates what format they have or what program is intended to use them

### Working directory

- `pwd` (**p**rint **w**orking **d**irectory)
- `cd` (**c**hange working **d**irectory)
  - Paths
    - If you want to move somewhere not in the working directory
    - `.`
    - `..`
    - `/`
    - `~`
    - Can also `ls` with path

### Side note: Tab completion

### Reading files

- `cat` (con**cat**enate [will explain later])
  - Can use paths here too
- `less` (opposite of `more`)
  - Scrollable
    - `k` and `j`
    - `Page Up` and `Page Down`
    - `Control-u` and `Control-d`
    - `g` and `G`
  - `/` to search
    - type search
    - press `Enter`
    - press `n` to find next
    - press `Shift-n` (`N`) to find previous
  - `q` to quit

### Quick break to explain `man`

- Some experienced users will ask you to "RTFM"
- Same controls as `less`

## Writing (creating new files/directories)

### `touch`

- Updates the "last updated" ("**touch**ed") timestamp
- As a side effect, creates a file (if it doesn't exist)

### `mkdir` (**m**a**k**e **dir**ectory)

### `chmod` (**ch**ange file **mod**e)

- Change permissions (**r**ead, **w**rite, and e**x**ecute)
- set in form of 9 bits:

  ```none
  876   543    210
  rwx   rwx    rwx
  ^user ^group ^others
  ```

- Octal mode
  - octal => 3 bits, so 3 octal digits gives 9 bits
  - Ex: `chmod 700 FILE` sets user read, write, and execute bits; resets the rest
- Symbolic mode
  - Ex: `chmod g+w FILE` adds write permissions for the group

### Moving

#### `cp` (**c**o**p**y)

- `cp FILES DIRECTORY`
- `-t DIRECTORY FILES` (**t**arget directory first)

#### `mv` (**m**o**v**e)

- `-t` same as `cp`

## Deleting

### `rm` (**r**e**m**ove)

- `-i` (**i**nteractive)
  - Prompts before removal
- `-r` (**r**ecursive)
  - Delete directory and all contents
- `-f` (**f**orce)
  - Never prompts, ignores missing files

### `rmdir` (**r**e**m**ove **dir**ectory)

## Editing

### `nano`

- controls are all intuitive or shown on-screen

### `vim`

- notoriously "unintuitive"
- same controls as `less`
- `i` for **i**nsert mode (or `a` for **a**ppend, `o` for **o**pen new line)
  - Can type "normally"
  - `Esc` to return to normal mode
- also uses finer "motions"
  - `hjkl` - "arrow keys" but on the home row
  - `^` - start of line
  - `$` - end of line
  - `w` - **w**ord
  - `e` - **e**nd of word
  - `f` - **f**ind in line
    - `;` to find next
    - `,` to find previous
  - `t` - "**t**o" (find in line exclusive)
  - `gg` - start of file
  - `G` - end of file
  - `NUMBER G` - jump to line number `NUMBER`
- `d` then a motion to **d**elete
  - or `dd` to delete line
  - or `c` to **c**hange (delete and insert)
- `x` to delete character under cursor
- can add number before command or motion to repeat it
- most importantly... to leave, use:
  - `:q` - **q**uit (without writing/saving)
  - `:wq` - **w**rite and **q**uit
- briefly, `.vimrc`
  - `:set rnu`
  - `:set nu`
- side note: there are plugins for most editors which allow `vim` bindings, so worth learning
- [OpenVim](https://www.openvim.com/tutorial.html)
- `vimtutor`

### `emacs`

- I don't know much about it personally, but it's widely used too

## Running Programs

- Just type the name!
  - Will search `PATH`
    - `which gcc`
    - `echo $PATH`
    - In fact, most of the commands we've used so far are just programs in `/usr/bin`
  - If not on path, type path to program starting with `./`.
    - `./a.out`

### `grep` (**g**lobal **r**egular **e**xpression **p**rint)

- print lines that match a regular expression
- `grep PATTERN FILES`
- `-i` (case **i**nsensitive)
- `-n` (line **n**umbers)
- `-v` (in**v**erse match)
  - print lines that *don't* match
- `-c` (show **c**ount)

### Redirecting Program I/O

- `>` - redirect `stdout`
- `>>` - redirect/append `stdout`
- `<` - redirect `stdin`
- `|` - pipe `stdout`
  - runs two programs concurrently and redirects I/O
  - `wc` (**w**ord **c**ount)
    - `wc -l` prints just **l**ines
  - `yes`
    - `Control-c` to interrupt process
    - `clear`
- `2>` redirect `stderr`

### Globs

- `cat` with glob
  - now it actually con**cat**enates!

### `diff`

- `-y` - show side-by-side

### `javac` and `java`

- `javac HelloWorld.java` to compile
- `java HelloWorld` to run

### `find`

- searches for files and does something with them (print by default)
- `find DIRECTORIES -name "NAME"`

### `exit`

### `scp`

- From local to remote host
  - `scp Project1_EID.zip USERNAME@kamek.ece.utexas.edu:~/422C`
- From remote to local host
  - `scp USERNAME@kamek.ece.utexas.edu:~/422C/Project1_EID.zip ~/Documents`

## More Info

- `alias`
- scripting
  - make a `.sh` file with the commands you want to run
  - logic
    - `if-then`
    - `&&`
- EE 461S: Operating Systems
