# MIPS Assembly Tutorial

## Introduction
MIPS Assembly is a low-level programming language for MIPS architecture, commonly used in academic environments and some embedded systems. This tutorial covers the most common MIPS instructions with examples.

## Basics of MIPS Assembly

### Registers
- **General Purpose Registers ($0 - $31)**
  - **$0 ($zero)**: Always holds the value 0.
  - **$v0, $v1**: Return values from functions.
  - **$a0 - $a3**: Arguments to functions.
  - **$t0 - $t9**: Temporary registers.
  - **$s0 - $s7**: Saved registers.
  - **$sp**: Stack Pointer.
  - **$ra**: Return Address.

### Instruction Set

#### 1. Data Processing Instructions

**ADD (Add)**
```assembly
add $t0, $t1, $t2  ; $t0 = $t1 + $t2
```

**ADDI (Add Immediate)**
```assembly
addi $t0, $t1, 10  ; $t0 = $t1 + 10
```

**SUB (Subtract)**
```assembly
sub $t0, $t1, $t2  ; $t0 = $t1 - $t2
```

**MULT (Multiply)**
```assembly
mult $t1, $t2      ; Multiply $t1 by $t2, result in hi and lo registers
mflo $t0           ; Move the lower 32 bits of the result to $t0
```

**DIV (Divide)**
```assembly
div $t1, $t2       ; Divide $t1 by $t2, quotient in lo, remainder in hi
mflo $t0           ; Move quotient to $t0
mfhi $t1           ; Move remainder to $t1
```

**AND (Bitwise AND)**
```assembly
and $t0, $t1, $t2  ; $t0 = $t1 & $t2
```

**OR (Bitwise OR)**
```assembly
or $t0, $t1, $t2   ; $t0 = $t1 | $t2
```

**XOR (Bitwise XOR)**
```assembly
xor $t0, $t1, $t2  ; $t0 = $t1 ^ $t2
```

**NOR (Bitwise NOR)**
```assembly
nor $t0, $t1, $t2  ; $t0 = ~($t1 | $t2)
```

**SLT (Set on Less Than)**
```assembly
slt $t0, $t1, $t2  ; $t0 = 1 if $t1 < $t2, else $t0 = 0
```

**SLTI (Set on Less Than Immediate)**
```assembly
slti $t0, $t1, 10  ; $t0 = 1 if $t1 < 10, else $t0 = 0
```

#### 2. Load/Store Instructions

**LW (Load Word)**
```assembly
lw $t0, 0($t1)  ; Load word from memory address in $t1 into $t0
```

**SW (Store Word)**
```assembly
sw $t0, 0($t1)  ; Store word in $t0 into memory address in $t1
```

**LB (Load Byte)**
```assembly
lb $t0, 0($t1)  ; Load byte from memory address in $t1 into $t0 (sign-extended)
```

**SB (Store Byte)**
```assembly
sb $t0, 0($t1)  ; Store byte in $t0 into memory address in $t1
```

**LUI (Load Upper Immediate)**
```assembly
lui $t0, 0x1234  ; Load 0x12340000 into $t0
```

#### 3. Branch Instructions

**BEQ (Branch if Equal)**
```assembly
beq $t0, $t1, LABEL  ; If $t0 == $t1, branch to LABEL
```

**BNE (Branch if Not Equal)**
```assembly
bne $t0, $t1, LABEL  ; If $t0 != $t1, branch to LABEL
```

**J (Jump)**
```assembly
j LABEL  ; Jump to LABEL
```

**JR (Jump Register)**
```assembly
jr $ra  ; Jump to address in $ra (used for function return)
```

**JAL (Jump and Link)**
```assembly
jal FUNCTION  ; Jump to FUNCTION and save return address in $ra
```

#### 4. Shift and Rotate Instructions

**SLL (Shift Left Logical)**
```assembly
sll $t0, $t1, 2  ; $t0 = $t1 << 2 (shift left by 2 bits)
```

**SRL (Shift Right Logical)**
```assembly
srl $t0, $t1, 2  ; $t0 = $t1 >> 2 (logical shift right by 2 bits)
```

**SRA (Shift Right Arithmetic)**
```assembly
sra $t0, $t1, 2  ; $t0 = $t1 >> 2 (arithmetic shift right by 2 bits)
```

#### 5. Pseudo Instructions

**LI (Load Immediate)**
```assembly
li $t0, 100  ; Load immediate value 100 into $t0
```

**MOVE (Move Register)**
```assembly
move $t0, $t1  ; $t0 = $t1
```

**NOP (No Operation)**
```assembly
nop  ; No operation (used for delay slots)
```

### Example Program: Sum of Array
```assembly
.data
array: .word 10, 20, 30, 40  # Array of 4 elements
array_end: 

.text
.globl main

main:
    la $t0, array    # Load address of array into $t0
    li $t1, 0        # Initialize sum to 0

loop:
    lw $t2, 0($t0)   # Load word from array into $t2
    add $t1, $t1, $t2  # Add array element to sum
    addi $t0, $t0, 4  # Move to the next element
    bne $t0, array_end, loop  # If not end, repeat loop

    # Exit program
    li $v0, 10
    syscall
```

## Conclusion
This tutorial introduced basic MIPS Assembly instructions with usage examples. To become proficient, practice writing and debugging MIPS Assembly code.

## :snowman: Author
Eray Öztürk ([@diffstorm](https://github.com/diffstorm))
