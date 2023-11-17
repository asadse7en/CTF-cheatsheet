# Reverse Engineering

* First, find the filetype using the `file` command.
* Use `strings <filename>` command to read the strings in the binary to get some clues. You can also grep for the file if the flag format is known `grep -i "flag{.*}"`
* You must have proficiency in C, Assembly Language, and computer architecture to solve RE challenges.

####

#### Ltrace

<details>

<summary>Installation</summary>

`sudo apt install ltrace`

</details>

**`ltrace`** It intercepts and displays dynamic function calls and parameters, offering insights into the program's functionality. by revealing a binary's library calls during execution.



#### R2

<details>

<summary>Installation</summary>

`sudo apt install radare2`

</details>

* **decompile: `r2 -d crackme aaaaaaaaaa`**
* **`aaa`**: Analyze all - auto analysis.
* **`afl`**: List all functions.
* **`pdf @function.name`**: Print disassembly of the current function.
* `db 0x004006d5`: set breakpoint
* `dc`: execute
* `dr`: see memory addresses of registers
* `px @rdi`: view registers rdi, rax, rdx
