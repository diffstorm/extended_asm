# ARM Assembly Tutorial

## Introduction
ARM Assembly is a low-level programming language for ARM architecture. It provides direct control over hardware, making it essential for embedded systems programming. This tutorial covers common ARM instructions with examples.

## Basics of ARM Assembly

### Registers
- **General Purpose Registers (R0 - R12)**: Used for various calculations.
- **R13 (SP)**: Stack Pointer.
- **R14 (LR)**: Link Register.
- **R15 (PC)**: Program Counter.
- **CPSR**: Current Program Status Register.

### Instruction Set

#### 1. Data Processing Instructions

**ADD (Add)**
```assembly
ADD R0, R1, R2  ; R0 = R1 + R2
```

**SUB (Subtract)**
```assembly
SUB R0, R1, R2  ; R0 = R1 - R2
```

**RSB (Reverse Subtract)**
```assembly
RSB R0, R1, R2  ; R0 = R2 - R1
```

**MUL (Multiply)**
```assembly
MUL R0, R1, R2  ; R0 = R1 * R2
```

**MOV (Move)**
```assembly
MOV R0, R1  ; R0 = R1
```

**MVN (Move Not)**
```assembly
MVN R0, R1  ; R0 = ~R1 (bitwise NOT)
```

**AND (Bitwise AND)**
```assembly
AND R0, R1, R2  ; R0 = R1 & R2
```

**ORR (Bitwise OR)**
```assembly
ORR R0, R1, R2  ; R0 = R1 | R2
```

**EOR (Bitwise Exclusive OR)**
```assembly
EOR R0, R1, R2  ; R0 = R1 ^ R2
```

**BIC (Bit Clear)**
```assembly
BIC R0, R1, R2  ; R0 = R1 & ~R2
```

**CMP (Compare)**
```assembly
CMP R0, R1  ; Compare R0 with R1 (sets flags)
```

**CMN (Compare Negative)**
```assembly
CMN R0, R1  ; Compare R0 with -R1 (sets flags)
```

**TST (Test)**
```assembly
TST R0, R1  ; Test R0 & R1 (sets flags)
```

**TEQ (Test Equivalence)**
```assembly
TEQ R0, R1  ; Test R0 ^ R1 (sets flags)
```

#### 2. Load/Store Instructions

**LDR (Load Register)**
```assembly
LDR R0, [R1]  ; Load value at memory address in R1 into R0
```

**STR (Store Register)**
```assembly
STR R0, [R1]  ; Store value in R0 into memory address in R1
```

**LDRB (Load Register Byte)**
```assembly
LDRB R0, [R1]  ; Load byte at memory address in R1 into R0
```

**STRB (Store Register Byte)**
```assembly
STRB R0, [R1]  ; Store byte in R0 into memory address in R1
```

**LDM (Load Multiple)**
```assembly
LDMFD R13!, {R0-R3}  ; Load multiple registers (R0-R3) from memory and update the stack pointer
```

**STM (Store Multiple)**
```assembly
STMFD R13!, {R0-R3}  ; Store multiple registers (R0-R3) to memory and update the stack pointer
```

#### 3. Branch Instructions

**B (Branch)**
```assembly
B LABEL  ; Branch to LABEL
```

**BL (Branch with Link)**
```assembly
BL FUNCTION  ; Branch to FUNCTION and save return address in LR
```

**BX (Branch and Exchange)**
```assembly
BX LR  ; Branch to address in LR (used for function return)
```

#### 4. Shift and Rotate Instructions

**LSL (Logical Shift Left)**
```assembly
LSL R0, R1, #2  ; R0 = R1 << 2 (shift left by 2 bits)
```

**LSR (Logical Shift Right)**
```assembly
LSR R0, R1, #2  ; R0 = R1 >> 2 (shift right by 2 bits)
```

**ASR (Arithmetic Shift Right)**
```assembly
ASR R0, R1, #2  ; R0 = R1 arithmetic shift right by 2 bits
```

**ROR (Rotate Right)**
```assembly
ROR R0, R1, #2  ; R0 = R1 rotate right by 2 bits
```

**RRX (Rotate Right with Extend)**
```assembly
RRX R0, R1  ; R0 = R1 rotate right by 1 bit and carry flag
```

#### 5. Condition Codes
Instructions can be conditionally executed based on the CPSR flags:

- **EQ**: Equal (Z=1)
- **NE**: Not Equal (Z=0)
- **GT**: Greater Than (Z=0, N=V)
- **LT**: Less Than (N!=V)
- **GE**: Greater or Equal (N=V)
- **LE**: Less or Equal (Z=1 or N!=V)

Example:
```assembly
ADDEQ R0, R1, R2  ; If equal (Z=1), R0 = R1 + R2
```

### Example Program: Sum of Array
```assembly
AREA SUM_ARRAY, CODE, READONLY
ENTRY
    LDR R1, =ARRAY  ; Load address of ARRAY
    MOV R2, #0      ; Initialize sum to 0

LOOP
    LDR R3, [R1], #4  ; Load array element and post-increment R1 by 4
    ADD R2, R2, R3    ; Add element to sum
    CMP R1, #ARRAY_END  ; Compare current address with end of array
    BNE LOOP          ; If not end, repeat loop

    B END

ARRAY DCD 10, 20, 30, 40  ; Array of 4 elements
ARRAY_END EQU ARRAY + 16

END
    B END
END
```

## Conclusion
This tutorial introduced basic ARM Assembly instructions with examples. To become proficient, practice writing and debugging ARM Assembly code.

## :snowman: Author
Eray Öztürk ([@diffstorm](https://github.com/diffstorm))