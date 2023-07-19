# FIRMWARE REVERSING

## TASK DESCRIPTION:

Make a **CALCULATOR**  in `asm` 

```nasm
section .data
        operator1: db "+"
        operator2: db "/"
        operator3: db "*"
        operator4: db "-"
        text db "to add press +",10,0 
        text2 db "to sub press -",10,0
        text3 db "to mul press *",10,0
        text4 db "to div press /",10,0
        text5 db "Enter the 1st number",10,0
        text6 db "Enter the 2nd number",10,0
section .bss
        operation resb 4
        num1 resb 4
        num2 resb 4
        result resb 4
section .text
    global _start
_start:
    mov rax, text
    call _print

    mov rax, text2
    call _print

    mov rax, text3
    call _print

    mov rax, text4
    call _print

    call _getoperator

    mov rax, text5
    call _print
    call _getnum1

    mov rax, text6
    call _print
    call _getnum2

    call _userinput

_print:
    push rax
    mov rbx, 0
_printloop:
    inc rax
    inc rbx
    mov cl, [rax]
    cmp cl, 0
    jne _printloop

    mov rax, 1
    mov rdi, 1
    pop rsi
    mov rdx, rbx
    syscall
    ret

_getoperator:
    mov rax, 0
    mov rdi, 0
    mov rsi, operation
    mov rdx, 4
    syscall 
    ret 

_getnum1:
    mov rax, 0
    mov rdi, 0
    mov rsi, num1
    mov rdx, 4
    syscall 
    ret 


_getnum2:
    mov rax, 0
    mov rdi, 0
    mov rsi, num2
    mov rdx, 4
    syscall 
    ret



_userinput:
    mov rsi, operator1
    mov rdi, operation
    mov ecx, 1
    repe cmpsb
    je _add

_userinput1:
    xor rsi, rsi 
    xor rdi, rdi 
    mov rsi, operator2
    mov rdi, operation
    mov ecx, 1
    repe cmpsb
    je _same_numbers

_userinput2:
    xor rsi, rsi 
    xor rdi, rdi 
    mov rsi, operator3
    mov rdi, operation
    mov ecx, 1
    repe cmpsb
    je _multiply
_userinput3:
    xor rsi, rsi 
    xor rdi, rdi 
    mov rsi, operator4
    mov rdi, operation
    mov ecx, 1
    repe cmpsb
    je _sub

_add:
    xor rax, rax
    mov rax, [num1]
    sub rax, '0'

    xor rbx, rbx
    mov rbx, [num2]
    sub rbx, '0'

    add rax, rbx
    add rax, '0'
    mov [result], rax 
    call _printresult
    ret

_sub:
    xor rax, rax
    mov rax, [num1]
    sub rax, '0'

    xor rbx, rbx
    mov rbx, [num2]
    sub rbx, '0'

    sub rax, rbx
    add rax, '0'
    mov [result], rax 
    call _printresult
    ret

_multiply:
    xor rax, rax
    mov rax, [num1]
    sub rax, '0'

    xor rbx, rbx
    mov rbx, [num2]
    sub rbx, '0'

    mul rbx
    add rax, '0'
    mov [result], rax 
    call _printresult
    ret

_same_numbers:
    mov al, [num1]
    mov bl, [num2]

    cmp al, bl
    je _result_equal_1
    jne _division

_result_equal_1:
    mov rax, 1
    add rax, '0'
    mov [result], rax  
    jmp _printresult    


_division:
     xor rax, rax
    mov rax, [num1]
    sub rax, '0'

    xor rbx, rbx
    mov rbx, [num2]
    sub rbx, '0'

    div rbx
    add rax, '0'
    mov [result], rax
    call _printresult
    ret

_printresult:
    mov rax, 1
    mov rdi, 1
    mov rsi, result
    mov rdx, 4
    syscall 
    jmp _exit

_exit:
    mov rax, 60
    mov rdi, 0
    syscall
```

### CODE EXPLANATION:

- `section .data` - It contains the defined text and variables of the kind of operation thta has to be done

- `section .bss` - It is reserved for the integers and operation selection and result 4 bytes are reserved as an integer takes 4 bytes of memory

- `section .text` - The main code starts from here

- `mov rax, text` this command moves the contents of the variable **text** to rax register it then calls `_print` subroutine

- This is done for all the 5 texts

- Then `_getoperator` subroutine is called which takes in the desired operation that the user intends to do

- `_getnum1` & `_getnum2` takes in the 2 numerical inputs

- Then `_userinput` is called

### PRINT SUB-ROUTINE:

It saves the value of `rax` on the stack, initializes `rbx` to zero, and then loops through each character of the string until it encounters the null terminator (0).

### GETOPERATOR , GETNUM1, GETNUM2 SUB-ROUTINE

All these are subroutines to get standard input and to store it in a variable

### USERINPUT SUB-ROUTINE

- This is used to match the user input operation to the operations specified (add,sub,multiply,divide)

- It moves already defined operation1 to `rsi` and user input to `rdi`

- value of **1** is stored in `ecx` it acts as a counter for the number of iterations

- `repe cmpsb` instruction compares bytes at the memory locations pointed to by `rsi` and `rdi` and sets the Zero Flag (`ZF`) if the bytes are equal. It also increments `rsi` and `rdi` automatically after each comparison

- The comparison is repeated until a mismatch is found or `ecx` (which is set to **1**) iterations have been completed

- If all the bytes being compared are equal (`ZF = 1`)

- This same process is carried out in _userinput1 to 3 but the `rsi` and `rdi` registers are **xored** with eachother to clear the contents of it

### ADD, SUB, MULTIPLY

- `rax` is **xored** with itself to clear it and **num1** is moved into rax

- The same is done for `rbx` and **num2** is moved into that register

- Then according to the operation `rax` and `rbx` are added, subtracted or multiplied

- The result of the operation will be stored in `rax` register, this is moved to `result` variable and `_printresult` sub- routine is called

### DIVISION

- After the operation compare when the user input operation is division or `/` it calls the sub-routine `_same_numbers` 

- This sub-routine compares the 2 numbers and if they are equal it jumps to `_result_equal_1` which moves the value **1**  to `rax` and then calls the `_printresult` sub-routine

- If the numbers arent equal it jumps to `_division` sub-routine

- The value in `rax` register is divided by the value in `rbx` register and the **quotient** is stored in `rax` and the **remainder** is stored in `rbx` 

- The value stored in `rax` is moved into the variable `result` and then `_printresult` sub-rotine is called

### PRINT RESULT

- It prints the value stored in `result` 

- It the jumps to `_exit`

### EXIT

- The standard exit code is 60

- This subroutine exits from the calculator

  To compile and execute
  `nasm -f elf64 calculator.asm -o calculator.o`
  `ld calculator.o -o calculator`
  
