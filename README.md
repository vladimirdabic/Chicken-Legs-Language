# Chicken Legs Language

**Why the name? Didn't really have any other ideas ¯\\\_(ツ)_/¯**

CLL plans to be:
- [x] Compiled
- [x] Stack-based
- [x] Statically typed (Type checking is really basic)
- [x] Self-hosted

This project is only for fun and learning. I'm not aiming to create a great language, just one that works.

Initially Python was used as a bootstrap for the language. Now the language its fully self hosted.

## Examples
Hello World:
```
%include "std.cll"

global proc main() -> dword {
   printf("Hello World\n");
   return 0;
}
```

## Quick Start

### Compilation

CLL is a 64 bit compiler.\
CLL generates assembly code, compiles it with [nasm](https://www.nasm.us/), and then links it with [TDM-GCC](https://jmeubank.github.io/tdm-gcc/download/).\
I only tested it with TDM-GCC, any Windows GCC 64 bit variant should work as well.

```console
> cll -c hello_world.cll -o hello_world.exe
[INFO] Generating assembly
[INFO] Generated assembly .\main.cll.asm
[CMD] nasm -fwin64 .\main.cll.asm -o .\main.cll.o
[CMD] gcc -m64 -g .\main.cll.o -o .\main.exe
> .\hello_world.exe
Hello World
```

### Usage
There's already a release package for the compiler.\
You can download it and extract it anywhere. Make sure the include folder is in the same directory as the compiler exectuable.\
You can add it to your PATH system variable.

```console
Usage: cll [OPTIONS] <input.cll>
OPTIONS:
    -o <output>    Provide output path
    -a             Only generates the ASM without compiling
    -c             Clean mode (Deletes the generated .asm and .o file)
    -r             Runs the program after compilation
    -h             Print this help to stdout
```

Example usage:
```
> cll -c -r main.cll -o main.exe
```

By default the compiler searches files to include in `./` (Current working directory), `/include/` (In the compiler's directory) and `/` (Also in the compiler's directory).