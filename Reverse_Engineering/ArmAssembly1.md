# CTF Challenge: ArmAssembly1

## Table of Content

- commands-executed:  strings chall_1.S , cat chall_1.S  
- flag : picoCTF{00000D2A}


### Chain of thought / Learning:
- We are again dealing with assembly files, so what I'm gonna start with is strings command to get a rough image.
- Then I am gonna use a disassembler objdump to get a better idea of what the program is about.
- Okay, for some reason objdump command is not working. So the deal is objdump cannot disassemble assembly files; I'm gonna need to convert it into bytecode, which is easy since I havegcc. gcc keeps showing errors.
- Watching the YouTube video given in the PDF, I need to know about the basics of assembly language.
- **Command Line Arguments in C**: Command-line arguments are the values given after the name of the program in the command-line shell of Operating Systems. 
  - argc - number of command-line arguments
  - argv - argument vector pointing to those values.
  - argv[0] is always the name of the program; the rest are the values passed to the main function.
- -ldr x0, [x29, 16] - this line loads a register x0 argv[0] to the memory address of x29. Importance of x0: whenever you call the function, the first argument called resides in x0.
- add x0, x0, 8 - this is basically moving to the next argument in the argv, and the ldr x0 is loading it to the register x0. 8 is the width of a 64-bit pointer.
- bl atoi: used man atoi to know about the command - converts ASCII to integers for the program.
- str w0, [x29, 44]: w0 is the 32-bit space for x0, 32 bits as ato` returns a string of size 4 bytes.`x29 is typically used as the frame pointer register, basically the address where it is being stored.
- bl func - now it loads x0 and calls the function. We need to figure out what the function does.


  ```assembly
  sub     sp, sp, #32       ; creating space in the stack
  str     w0, [sp, 12]      ; storing the value of w0 12 bits above the stack pointer
  mov     w0, 79            ; okay, so this is where w0 is being assigned the value 79.
  str     w0, [sp, 16]      ; we have another argument for this at sp+16, 79
  mov     w0, 7             ; we give w0 = 7
  str     w0, [sp, 20]      ; store it at sp+20
  mov     w0, 3             ; w0 = 3 and store it at sp+24
  str     w0, [sp, 24]
  ldr     w0, [sp, 20]      ; w0 = value at sp+20 = 7
  ldr     w1, [sp, 16]      ; w1 = value at sp+16 = 79
  lsl     w0, w1, w0        ; we perform a left shift - syntax: lsl destination, source, amount of shift;
                            ; in this case, `lsl 7, 79, 7` means we shift 79 to the left by 7 bits and store it in w0,
                            ; so 79 shifted left by 7 bits is 10112.
  str     w0, [sp, 28]      ; w0 = 10112 is now at sp+28
  ldr     w1, [sp, 28]      ; w1 = 10112
  ldr     w0, [sp, 24]      ; w0 = 3
  sdiv    w0, w1, w0        ; `sdiv` - signed division, syntax: sdiv destination, dividend, divisor;
                            ; essentially 10112 % 3 = 3370 is stored in w0
  str     w0, [sp, 28]      ; now where 10112 was stored, 3370 is stored.
  ldr     w1, [sp, 28]      ; w1 = 3370 
  ldr     w0, [sp, 12]      ; the value at sp+12 is the value which is passed to the function
                            ; which I need to figure out - let's say it’s x
  sub     w0, w1, w0        ; we subtract w1 - w0 and store the result in w0; w0 = 3370 - x
  str     w0, [sp, 28]      ; sp+28 = 3370 - x 
  ldr     w0, [sp, 28]      ; w0 = 3370 - x
  add     sp, sp, 32     
  ret                        ; returns 3370 - x
  .size   func, .-func
  .section .rodata
  .align  3

  cmp     w0, 0             ; it compares the two values and sets flags accordingly
                          ; - w0 == 0: zero flag set
                          ; - w0 < 0: zero flag clear, negative set
                          ; - w0 > 0: zero and negative flags clear
  
  bne     .L4               ; branch if not equal - i.e., if w0 != 0 it’ll run .L4.
                          ; .L4 runs the "you lose" output, so to continue to .LC0 for "you win",
                          ; we need 3370 - x = 0, i.e., x = 3370
  adrp    x0, .LC0       
  add     x0, x0, :lo12:.LC0
  bl      puts
  b       .L6
-we got what we needed i.e 3370 now just convert it into hexadecimal 32 bit and we have our answer 0x00000D2A
 
#### Output:
```console

┌──(anonymous㉿Anonymous)-[~/Downloads]
└─$ strings chall_1.S         
        .arch armv8-a
        .file   "chall_1.c"
        .text
        .align  2
        .global func
        .type   func, %function
func:
        sub     sp, sp, #32
        str     w0, [sp, 12]
        mov     w0, 79
        str     w0, [sp, 16]
        mov     w0, 7
        str     w0, [sp, 20]
        mov     w0, 3
        str     w0, [sp, 24]
        ldr     w0, [sp, 20]
        ldr     w1, [sp, 16]
        lsl     w0, w1, w0
        str     w0, [sp, 28]
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 24]
        sdiv    w0, w1, w0
        str     w0, [sp, 28]
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 12]
        sub     w0, w1, w0
        str     w0, [sp, 28]
        ldr     w0, [sp, 28]
        add     sp, sp, 32
        ret
        .size   func, .-func
        .section        .rodata
        .align  3
.LC0:
        .string "You win!"
        .align  3
.LC1:
        .string "You Lose :("
        .text
        .align  2
        .global main
        .type   main, %function
main:
        stp     x29, x30, [sp, -48]!
        add     x29, sp, 0
        str     w0, [x29, 28]
        str     x1, [x29, 16]
        ldr     x0, [x29, 16]
        add     x0, x0, 8
        ldr     x0, [x0]
        bl      atoi
        str     w0, [x29, 44]
        ldr     w0, [x29, 44]
        bl      func
        cmp     w0, 0
        bne     .L4
        adrp    x0, .LC0
        add     x0, x0, :lo12:.LC0
        bl      puts
        b       .L6
.L4:
        adrp    x0, .LC1
        add     x0, x0, :lo12:.LC1
        bl      puts
.L6:
        nop
        ldp     x29, x30, [sp], 48
        ret
        .size   main, .-main
        .ident  "GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
        .section        .note.GNU-stack,"",@progbits
┌──(anonymous㉿Anonymous)-[~/Downloads]
└─$ objdump -d chall_1.S               
objdump: chall_1.S: file format not recognized


```
