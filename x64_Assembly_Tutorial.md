# x64 Assembly Tutorial

## Introduction
x64 Assembly is a low-level programming language for the x86-64 architecture, widely used in modern computers. This tutorial covers the most common x64 instructions with examples.

## Differences Between x86 and x64 Assembly

While x86 and x64 Assembly languages share many similarities, there are several critical differences due to the architectural enhancements in x64. Understanding these differences is essential when transitioning from 32-bit (x86) to 64-bit (x64) programming.

### 1. **Register Extensions**

- **Register Size**: 
  - In x86, the general-purpose registers (EAX, EBX, ECX, etc.) are 32 bits wide. In x64, these registers are extended to 64 bits (RAX, RBX, RCX, etc.).
  - The 64-bit versions of registers are prefixed with an `R`, such as RAX, RBX, and so on.

- **Additional Registers**:
  - x64 introduces additional general-purpose registers: R8 through R15, providing more flexibility and reducing the need to frequently spill variables to memory.

### 2. **Addressing and Memory Access**

- **Addressable Memory**:
  - x86 is limited to 4 GB of addressable memory due to its 32-bit address space.
  - x64, with its 64-bit address space, can theoretically address up to 16 exabytes, though current implementations typically use 48 bits, allowing for up to 256 TB of addressable memory.

- **Pointer Size**:
  - In x86, pointers (e.g., addresses of variables or functions) are 32 bits.
  - In x64, pointers are 64 bits, which means data structures involving pointers, such as arrays of pointers, consume more memory in x64.

### 3. **Calling Conventions**

- **Function Parameters**:
  - x86 typically passes function parameters on the stack.
  - x64 uses registers for the first six integer or pointer arguments (RDI, RSI, RDX, RCX, R8, and R9 on Linux/macOS; RCX, RDX, R8, and R9 on Windows). Additional arguments are passed on the stack.

- **Stack Management**:
  - In x86, the caller is generally responsible for cleaning up the stack after a function call (cdecl convention).
  - In x64, the calling convention is more standardized: the callee cleans up the stack (except for variadic functions).

### 4. **Instruction Set Extensions**

- **Instruction Set**:
  - x64 includes all x86 instructions, plus additional instructions designed to take advantage of the 64-bit architecture, such as new instructions for manipulating 64-bit integers and pointers.
  - The x64 instruction set also deprecates some older x86 instructions, particularly those related to segment registers, which are largely unused in 64-bit mode.

### 5. **Performance Considerations**

- **Performance**:
  - x64 can provide performance improvements due to its ability to handle more data per instruction (64-bit operations) and due to the additional registers available.
  - However, x64 binaries can be slightly larger because instructions that reference 64-bit addresses or registers are longer.

### 6. **System Calls and Interrupts**

- **System Call Mechanisms**:
  - In x86, system calls are typically performed using the `int 0x80` interrupt.
  - In x64, the `syscall` instruction is used instead, which is more efficient.

- **Calling Conventions for System Calls**:
  - x64 has a different set of registers for system calls compared to x86. For example, the system call number is placed in `RAX`, and parameters are passed in `RDI`, `RSI`, `RDX`, `R10`, `R8`, and `R9`.

### 7. **Segmentation and Memory Models**

- **Segmentation**:
  - x86 uses segmentation for memory management, with segment registers like CS, DS, SS, and ES playing a role in determining the address space.
  - x64 largely abandons segmentation in favor of a flat memory model, where all segment registers are usually set to the same base address, simplifying memory access and addressing.

### 8. **Compatibility Mode**

- **Backward Compatibility**:
  - x64 CPUs can run x86 code in a special compatibility mode, allowing 32-bit applications to run on 64-bit systems without modification.
  - However, x64-specific code cannot be run on x86-only processors.

## Basics of x64 Assembly

### Registers
- **General Purpose Registers**:
  - **RAX, RBX, RCX, RDX**: Extended versions of the 32-bit registers.
  - **RSI**: Source Index.
  - **RDI**: Destination Index.
  - **RBP**: Base Pointer.
  - **RSP**: Stack Pointer.
  - **R8 - R15**: Additional general-purpose registers.
- **Segment Registers**: CS, DS, SS, ES, FS, GS.
- **RFLAGS**: Status flags.

### Instruction Set

#### 1. Data Movement Instructions

**MOV (Move)**
```assembly
MOV RAX, RBX  ; RAX = RBX
MOV RAX, [RBX]  ; RAX = value at memory address in RBX
MOV [RBX], RAX  ; value at memory address in RBX = RAX
MOV RAX, 10  ; RAX = 10
```

**PUSH (Push onto Stack)**
```assembly
PUSH RAX  ; Push RAX onto stack
```

**POP (Pop from Stack)**
```assembly
POP RAX  ; Pop top of stack into RAX
```

**LEA (Load Effective Address)**
```assembly
LEA RAX, [RBX+4*RCX]  ; Load effective address into RAX
```

**XCHG (Exchange)**
```assembly
XCHG RAX, RBX  ; Swap values in RAX and RBX
```

#### 2. Arithmetic Instructions

**ADD (Add)**
```assembly
ADD RAX, RBX  ; RAX = RAX + RBX
```

**SUB (Subtract)**
```assembly
SUB RAX, RBX  ; RAX = RAX - RBX
```

**IMUL (Integer Multiply)**
```assembly
IMUL RBX  ; RAX = RAX * RBX
IMUL RAX, RBX, 10  ; RAX = RBX * 10
```

**IDIV (Integer Divide)**
```assembly
IDIV RBX  ; Divide RDX:RAX by RBX, quotient in RAX, remainder in RDX
```

**INC (Increment)**
```assembly
INC RAX  ; RAX = RAX + 1
```

**DEC (Decrement)**
```assembly
DEC RAX  ; RAX = RAX - 1
```

#### 3. Logic Instructions

**AND (Bitwise AND)**
```assembly
AND RAX, RBX  ; RAX = RAX & RBX
```

**OR (Bitwise OR)**
```assembly
OR RAX, RBX  ; RAX = RAX | RBX
```

**XOR (Bitwise XOR)**
```assembly
XOR RAX, RBX  ; RAX = RAX ^ RBX
```

**NOT (Bitwise NOT)**
```assembly
NOT RAX  ; RAX = ~RAX
```

#### 4. Shift and Rotate Instructions

**SHL (Shift Left Logical)**
```assembly
SHL RAX, 1  ; RAX = RAX << 1
```

**SHR (Shift Right Logical)**
```assembly
SHR RAX, 1  ; RAX = RAX >> 1
```

**SAR (Shift Arithmetic Right)**
```assembly
SAR RAX, 1  ; RAX = RAX >> 1 (arithmetic shift)
```

**ROL (Rotate Left)**
```assembly
ROL RAX, 1  ; Rotate RAX left by 1 bit
```

**ROR (Rotate Right)**
```assembly
ROR RAX, 1  ; Rotate RAX right by 1 bit
```

#### 5. Control Flow Instructions

**CMP (Compare)**
```assembly
CMP RAX, RBX  ; Compare RAX and RBX (sets flags)
```

**TEST (Test)**
```assembly
TEST RAX, RBX  ; Perform AND operation and set flags, but don't store result
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
    xor RAX, RAX  ; Clear RAX (accumulator)
    xor RBX, RBX  ; Clear RBX (index)

sum_loop:
    add AL, [array + RBX]  ; Add byte from array to AL (low byte of RAX)
    inc RBX  ; Increment index
    cmp RBX, 4  ; Compare index to 4 (array length)
    jl sum_loop  ; If index < 4, repeat loop

    ; Exit program
    mov RAX, 60  ; syscall: exit
    xor RDI, RDI  ; exit code 0
    syscall  ; Invoke syscall
```

## Conclusion
This tutorial introduced basic x64 Assembly instructions with some examples. To become proficient, practice writing and debugging x64 Assembly code.

## :snowman: Author
Eray Öztürk ([@diffstorm](https://github.com/diffstorm))
