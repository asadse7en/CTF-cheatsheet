# Reverse Engineering



* First, find the filetype using the `file` command.
* Use `strings <filename>` command to read the strings in the binary to get some clues. You can also grep for the file if the flag format is known `grep -i "flag{.*}"`
* You must have proficiency in C, Assembly Language, and computer architecture to solve RE challenges.
* Typically, a provided binary file can be in the form of a PE File (.exe or .dll), ELF File (.elf), APK File (.apk), .NET File (.exe), Java file, or Python File (.pyc or .py).



### Online Tools

1. [**dogbolt**](https://dogbolt.org/) **-** Multiple decompilers (ghidra, binary ninja, angr, snowman, hex-rays, dewolf etc)
2. [**online ELF viewer**](http://www.sunshine2k.de/coding/javascript/onlineelfviewer/onlineelfviewer.html)
3. [**elfy.io**](https://elfy.io/)
4. [**decompiler.com**](https://www.decompiler.com/) **-** online decompiler (EXE, DLL, JAR, APK SMX)
5. [**java decompiler**](http://www.javadecompilers.com/) **-**  .jar or .class decompiler
6. [**jdec.app**](https://jdec.app/) **-**  .jar or .class decompiler

## Reversing ELF

<details>

<summary>Installations</summary>

`sudo apt install ltrace`

`sudo apt install strace`

`sudo apt install ghidra`

`sudo apt install radare2`

</details>

* Use `ltrace ./<filename>` to identify library function calls in the binary.
* Use `strace ./<filename>` to observe system and signal function calls in the binary.
* Use `nm <filename>` command to know what symbol being called in the binary.
* Execute `readelf -a <filename>` to get full information about ELF files.
* Use `r2 -d <filename>` to decompile or debug the binary

<details>

<summary>r2 common commands</summary>

* **`aaa`**: Analyze all - auto analysis.

<!---->

* **`afl`**: List all functions.

<!---->

* **`pdf @function.name`**: Print disassembly of the current function.

<!---->

* `db 0x004006d5`: set breakpoint

<!---->

* `dc`: execute

<!---->

* `dr`: see memory addresses of registers

<!---->

* `px @rdi`: view registers rdi, rax, rdx

</details>

* Use [**IDA Pro**](https://hex-rays.com/ida-pro/)**,** [**Binary Ninja**](https://binary.ninja/)**,** [**Cutter**](https://cutter.re/)**,** or [**Ghidra**](https://ghidra-sre.org/) to perform static analysis on the binary.



### Reversing PE

