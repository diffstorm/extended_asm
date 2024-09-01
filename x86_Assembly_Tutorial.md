# x86 Assembly Tutorial

## Introduction
x86 Assembly is a low-level programming language for the x86 architecture, widely used in personal computers. This tutorial covers the most common x86 instructions with examples.

## Basics of x86 Assembly

### Registers
- **General Purpose Registers**:
  - **EAX**: Accumulator for operands and results data.
  - **EBX**: Base register.
  - **ECX**: Counter for loops.
  - **EDX**: Data register.
- **Index and Pointer Registers**:
  - **ESI**: Source Index.
  - **EDI**: Destination Index.
  - **EBP**: Base Pointer.
  - **ESP**: Stack Pointer.
- **Segment Registers**: CS, DS, SS, ES, FS, GS.
- **EFLAGS**: Status flags.

### Instruction Set

#### 1. Data Movement Instructions

**MOV (Move)**
```assembly
MOV EAX, EBX  ; EAX = EBX
MOV EAX, [EBX]  ; EAX = value at memory address in EBX
MOV [EBX], EAX  ; value at memory address in EBX = EAX
MOV EAX, 10  ; EAX = 10
```

**PUSH (Push onto Stack)**
```assembly
PUSH EAX  ; Push EAX onto stack
```

**POP (Pop from Stack)**
```assembly
POP EAX  ; Pop top of stack into EAX
```

**LEA (Load Effective Address)**
```assembly
LEA EAX, [EBX+4*ECX]  ; Load effective address into EAX
```

**XCHG (Exchange)**
```assembly
XCHG EAX, EBX  ; Swap values in EAX and EBX
```

#### 2. Arithmetic Instructions

**ADD (Add)**
```assembly
ADD EAX, EBX  ; EAX = EAX + EBX
```

**SUB (Subtract)**
```assembly
SUB EAX, EBX  ; EAX = EAX - EBX
```

**IMUL (Integer Multiply)**
```assembly
IMUL EBX  ; EAX = EAX * EBX
IMUL EAX, EBX, 10  ; EAX = EBX * 10
```

**IDIV (Integer Divide)**
```assembly
IDIV EBX  ; Divide EDX:EAX by EBX, quotient in EAX, remainder in EDX
```

**INC (Increment)**
```assembly
INC EAX  ; EAX = EAX + 1
```

**DEC (Decrement)**
```assembly
DEC EAX  ; EAX = EAX - 1
```

#### 3. Logic Instructions

**AND (Bitwise AND)**
```assembly
AND EAX, EBX  ; EAX = EAX & EBX
```

**OR (Bitwise OR)**
```assembly
OR EAX, EBX  ; EAX = EAX | EBX
```

**XOR (Bitwise XOR)**
```assembly
XOR EAX, EBX  ; EAX = EAX ^ EBX
```

**NOT (Bitwise NOT)**
```assembly
NOT EAX  ; EAX = ~EAX
```

#### 4. Shift and Rotate Instructions

**SHL (Shift Left Logical)**
```assembly
SHL EAX, 1  ; EAX = EAX << 1
```

**SHR (Shift Right Logical)**
```assembly
SHR EAX, 1  ; EAX = EAX >> 1
```

**SAR (Shift Arithmetic Right)**
```assembly
SAR EAX, 1  ; EAX = EAX >> 1 (arithmetic shift)
```

**ROL (Rotate Left)**
```assembly
ROL EAX, 1  ; Rotate EAX left by 1 bit
```

**ROR (Rotate Right)**
```assembly
ROR EAX, 1  ; Rotate EAX right by 1 bit
```

#### 5. Control Flow Instructions

**CMP (Compare)**
```assembly
CMP EAX, EBX  ; Compare EAX and EBX (sets flags)
```

**TEST (Test)**
```assembly
TEST EAX, EBX  ; Perform AND operation and set flags, but don't store result
```

**JMP (Jump)**
```assembly
JMP LABEL  ; Jump to LABEL
```

**JE/JZ (Jump if Equal/Zero)**
```assembly
JE LABEL  ; Jump to LABEL if Zero Flag is set
```

**JNE/JNZ (Jump if Not Equal/Not Zero)**
```assembly
JNE LABEL  ; Jump to LABEL if Zero Flag is not set
```

**JG/JNLE (Jump if Greater/Not Less or Equal)**
```assembly
JG LABEL  ; Jump to LABEL if greater
```

**JL/JNGE (Jump if Less/Not Greater or Equal)**
```assembly
JL LABEL  ; Jump to LABEL if less
```

**CALL (Call Procedure)**
```assembly
CALL FUNCTION  ; Call FUNCTION and save return address
```

**RET (Return from Procedure)**
```assembly
RET  ; Return to address saved by CALL
```

### Example Program: Sum of Array
```assembly
section .data
array db 10, 20, 30, 40  ; Array of 4 bytes

section .text
global _start

_start:
    xor EAX, EAX  ; Clear EAX (accumulator)
    xor EBX, EBX  ; Clear EBX (index)

sum_loop:
    add AL, [array + EBX]  ; Add byte from array to AL (low byte of EAX)
    inc EBX  ; Increment index
    cmp EBX, 4  ; Compare index to 4 (array length)
    jl sum_loop  ; If index < 4, repeat loop

    ; Exit program
    mov EAX, 1  ; sys_exit
    xor EBX, EBX  ; Return 0
    int 0x80  ; Interrupt to invoke syscall
```

## Conclusion
This tutorial introduced basic x86 Assembly instructions with some usage examples. To become proficient, practice writing and debugging x86 Assembly code.

## :snowman: Author
Eray Öztürk ([@diffstorm](https://github.com/diffstorm))
