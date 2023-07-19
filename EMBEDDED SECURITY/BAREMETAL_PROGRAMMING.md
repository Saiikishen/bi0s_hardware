# EMBEDDED SECURITY

## Implementing "Hello World" in baremental QEMU

### Challenge Description:

Implement a code to run "Hello World " on baremetal ARM processor iin QEMU

### CODE:

#### STARTUP.S

```nasm
.global _Reset
_Reset:
 LDR sp, =stack_top
 BL c_entry
 B .
```

#### CODE EXPLANATION:

- `.global _Reset`: This line declares the symbol `_Reset` as globally visible.`_Reset`  can be referenced by other object files

- `LDR sp, =stack_top`: This line loads the value of the `stack_top` symbol into the stack pointer register (sp). The `LDR` instruction is used to load a value from memory.

- `BL c_entry`: This line branches to the function labeled `c_entry` using the `BL` (branch with link) instruction. The `BL` instruction saves the return address in the link register (`lr`), allowing the program to return to the current point after executing the called function.

- `B .`: This line branches to the current location, effectively creating an infinite loop. The `.` represents the current address or label.

- This startup file calls `c_entry` and it runs in an infinite loop

#### LINKER

```c
ENTRY(_Reset)
SECTIONS
{
 . = 0x10000;
 .startup . : { startup.o(.text) }
 .text : { *(.text) }
 .data : { *(.data) }
 .bss : { *(.bss COMMON) }
 . = ALIGN(8);
 . = . + 0x1000;
 stack_top = .;
}
```

- `ENTRY(_Reset)` - Specifies the entry point of the program

- `SECTIONS` - We can define the various memory section

- `.` represents current memory address `.=0x10000` sets curent address to **0x10000** 

- `.startup` - this line crreates a section named **.startup** and places the contents of **startup.o** and its **.text** section which contains the executable code in it

- `.data` - contains initialised global and static variables

- `.bss`- contains unintialised global and static variables, **COMMON** indicates to the variables without a specific size

- `.=ALIGN(8)` - Alligns the current address to multiples of 8 bytes

- `.=.+0x1000` - increments the current address by **4KB** 

- `stack_top = .` - Used to obtain the top address of the stack

### TEST.C

```c
ENTRY(_Reset)
SECTIONS
{
 . = 0x10000;
 .startup . : { startup.o(.text) }
 .text : { *(.text) }
 .data : { *(.data) }
 .bss : { *(.bss COMMON) }
 . = ALIGN(8);
 . = . + 0x1000; /* 4kB of stack memory */
 stack_top = .;
}
```

- `volatile unsigned int * const UART0DR = (unsigned int *)0x101f1000;`
  
  - This line declares a pointer `UART0DR` to a memory address `0x101f1000`.
  
  - The `volatile` keyword indicates that the variable may be modified by external entities and should not be optimized by the compiler.
  
  - The `unsigned int *` cast is used to treat the memory address as a pointer to an unsigned integer.

- `void print_uart0(const char *s)`
  
  - This line defines a function named `print_uart0` that takes a pointer to a character string (`const char *s`) as its parameter.

- `while (*s != '\0')`
  
  - This line starts a loop that continues until the current character pointed to by `s` is not a null terminator (`'\0'`).

- `*UART0DR = (unsigned int)(*s);`
  
  - This line writes the current character pointed to by `s` to the memory address pointed to by `UART0DR`.

- `void c_entry()`
  
  - This function serves as the entry point for the bare-metal program.

### COMMANDS TO COMPILE:

- `arm-none-eabi-as -mcpu=arm926ej-s -g startup.s -o startup.o`

- `arm-none-eabi-gcc -c -mcpu=arm926ej-s -g test.c -o test.o`

- `arm-none-eabi-ld -T test.ld test.o startup.o -o test.elf`

- `arm-none-eabi-objcopy -O binary test.elf test.bin`

### SETTING UP QEMU AND RUNNING:

`qemu-system-arm -M versatilepb -m 128M -nographic -kernel test.bin`

### OUTPUT

`pulseaudio: set_sink_input_volume() failed
pulseaudio: Reason: Invalid argument
pulseaudio: set_sink_input_mute() failed
pulseaudio: Reason: Invalid argument
Hello world!`

`
