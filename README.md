# Extended Assembly Usage Examples for ARM, MIPS, x86, and x64
This repository provides code examples and explanations for using extended assembly in assembly language programming for ARM, MIPS, x86, and x64 architectures. Extended assembly is a feature that allows you to embed assembly code within a high-level programming language (like C or C++) for architecture-specific tasks. This README will guide you through the basics of extended assembly for these four popular architectures.

### Table of Contents
- Introduction
- Extended Assembly Overview
- ARM Assembly
- MIPS Assembly
- x86 Assembly
- x64 Assembly
- Examples
- Conclusion

## Introduction
Extended assembly allows you to mix assembly code with C/C++ code, which is helpful when you need to perform low-level tasks or interact with hardware directly. This can be particularly useful in embedded systems development, kernel-level programming, or when optimizing critical code sections.

In extended assembly, you can use special inline assembly syntax to embed assembly instructions directly into your C or C++ code. Each architecture has its own syntax, registers, and conventions, which will be covered in the following sections.

## Extended Assembly Overview
In extended assembly, you typically use the `asm` or `__asm__` directive followed by the assembly code enclosed in double-quotes. Within the assembly code, you can reference C/C++ variables using operand specifiers like `%0`, `%1`, etc., and input/output constraints.

```c
asm volatile(
    "assembly code"
    : output operands
    : input operands
    : clobbers
);
```

**assembly code**: The actual assembly instructions.

**output operands**: Constraints that specify where the assembly code will store its results.

**input operands**: Constraints that specify where the assembly code takes its inputs from.

**clobbers**: List of registers and memory locations that the assembly code modifies.

## Constraints
Operands and constraints help connect the assembly code with C/C++ variables. They specify which registers or memory locations are used for inputs and outputs.

Output constraints start with `"=r"` for general-purpose registers.
Input constraints start with `"%0"`, `"%1"`, etc., and are typically followed by `"r"` for general-purpose registers.
Now, let's explore extended assembly examples for ARM, MIPS, x86, and x64 architectures.

## ARM Assembly
ARM is a widely-used architecture in the embedded and mobile device development.

### Example 1: Add Two Integers
Here's an example of using extended assembly to add two integers in ARM:
```c
#include <stdio.h>

int main() {
    int result;
    int input1 = 10, input2 = 20;

    asm volatile(
        "add %0, %1, %2"
        : "=r" (result)
        : "r" (input1), "r" (input2)
    );

    printf("Result: %d\n", result);
    return 0;
}
```
In this example, we use the `add` instruction to add two integers and store the result in the `result` variable.

### Example 2: Load and Store Operations
In this example, we perform load and store operations in ARM assembly:
```c
#include <stdio.h>

int main() {
    int value;
    int* address = (int*)0x1000;

    asm volatile(
        "ldr %0, [%1]" // Load value from memory
        : "=r" (value)
        : "r" (address)
    );

    printf("Value at address 0x1000: %d\n", value);

    int new_value = 42;
    asm volatile(
        "str %0, [%1]" // Store value into memory
        :
        : "r" (new_value), "r" (address)
    );

    printf("New value at address 0x1000: %d\n", *address);

    return 0;
}
```
In this example, we use `ldr` to load a value from memory and `str` to store a value into memory.

### Example 3: Branching in Assembly
Here's an example that demonstrates conditional branching in ARM assembly:
```c
#include <stdio.h>

int main() {
    int value = 10;

    asm volatile(
        "cmp %0, #10\n\t"
        "beq equal\n\t"
        "bne not_equal\n"
        "equal:\n\t"
        "mov %0, #42\n"
        "not_equal:\n"
        : "+r" (value)
    );

    printf("Value: %d\n", value);
    return 0;
}
```
In this example, we compare value to 10 and use conditional branch instructions (`beq` and `bne`) to change the value accordingly.

## MIPS Assembly
MIPS architecture is commonly used in routers and some older gaming consoles.

### Example 1: Add Two Integers
Here's an example of using extended assembly to add two integers in MIPS:
```c
#include <stdio.h>

int main() {
    int result;
    int input1 = 10, input2 = 20;

    asm volatile(
        "add %0, %1, %2"
        : "=r" (result)
        : "r" (input1), "r" (input2)
    );

    printf("Result: %d\n", result);
    return 0;
}
```
In this MIPS example, we use the `add` instruction, which is similar to ARM.

### Example 2: Load and Store Operations
In this example, we perform load and store operations in MIPS assembly:
```c
#include <stdio.h>

int main() {
    int value;
    int* address = (int*)0x1000;

    asm volatile(
        "lw %0, (%1)" // Load value from memory
        : "=r" (value)
        : "r" (address)
    );

    printf("Value at address 0x1000: %d\n", value);

    int new_value = 42;
    asm volatile(
        "sw %0, (%1)" // Store value into memory
        :
        : "r" (new_value), "r" (address)
    );

    printf("New value at address 0x1000: %d\n", *address);

    return 0;
}
```
In this MIPS example, we use `lw` to load a value from memory and `sw` to store a value into memory.

### Example 3: Branching in Assembly
Here's an example that demonstrates conditional branching in MIPS assembly:
```c
#include <stdio.h>

int main() {
    int value = 10;

    asm volatile(
        "beq %0, $zero, equal\n\t"
        "bne %0, $zero, not_equal\n"
        "equal:\n\t"
        "li %0, 42\n"
        "not_equal:\n"
        : "+r" (value)
    );

    printf("Value: %d\n", value);
    return 0;
}
```
In this example, we use branch instructions like `beq` and `bne` to conditionally change the value.

## x86 Assembly
x86 architecture is widely used in desktop and server environments.

### Example 1: Add Two Integers
Here's an example of using extended assembly to add two integers in x86:
```c
#include <stdio.h>

int main() {
    int result;
    int input1 = 10, input2 = 20;

    asm volatile(
        "add %0, %1"
        : "=r" (result)
        : "r" (input1), "r" (input2)
    );

    printf("Result: %d\n", result);
    return 0;
}
```
In this x86 example, we use the `add` instruction, which adds two integers.

### Example 2: Read and Write to Port
In this example, we read from and write to an I/O port in x86 assembly:
```c
#include <stdio.h>

int main() {
    int value;
    unsigned short port = 0x3F8; // COM1 serial port

    // Read from I/O port
    asm volatile(
        "in %0, %1"
        : "=a" (value)
        : "d" (port)
    );

    printf("Read from port 0x3F8: %d\n", value);

    int data = 65; // ASCII 'A'
    
    // Write to I/O port
    asm volatile(
        "out %1, %0"
        :
        : "a" (data), "d" (port)
    );

    printf("Wrote 'A' to port 0x3F8\n");

    return 0;
}
```
In this x86 example, we use `in` to read from an I/O port and `out` to write to an I/O port.

### Example 3: String Manipulation
Here's an example that demonstrates string manipulation in x86 assembly:
```c
#include <stdio.h>
#include <string.h>

int main() {
    char dest[20];
    const char* src = "Hello, World!";
    
    asm volatile(
        "cld\n\t"
        "rep movsb"
        :
        : "S" (src), "D" (dest), "c" (strlen(src))
    );

    printf("Copied String: %s\n", dest);
    return 0;
}
```
In this example, we use the `rep movsb` instruction to copy a string from `src` to `dest`.

## x64 Assembly
x64 is an extension of x86 architecture used in modern 64-bit systems.

### Example 1: Add Two Integers
Here's an example of using extended assembly to add two integers in x64:
```c
#include <stdio.h>

int main() {
    int result;
    int input1 = 10, input2 = 20;

    asm volatile(
        "add %0, %1, %2"
        : "=r" (result)
        : "r" (input1), "r" (input2)
    );

    printf("Result: %d\n", result);
    return 0;
}
```
This x64 example is quite similar to the x86 example, but it's adapted to the 64-bit architecture.

### Example 2: Syscall to Print
In this example, we make a system call to print `"Hello, World!"` in x64 assembly:
```c
#include <stdio.h>

int main() {
    const char* message = "Hello, World!\n";

    asm volatile(
        "mov rdi, %0" // Load message address into rdi
        "mov rax, 1" // Syscall number for write
        "mov rsi, 1" // File descriptor (1 for stdout)
        "mov rdx, 13" // Message length
        "syscall" // Make the syscall
        :
        : "r" (message)
        : "rdi", "rax", "rsi", "rdx"
    );

    return 0;
}
```
In this x64 example, we use inline assembly to make a system call to print a message.

### Example 3: SIMD (Single Instruction, Multiple Data)
Here's an example that demonstrates the use of SIMD instructions in x64 assembly:
```c
#include <stdio.h>
#include <immintrin.h> // Intel Intrinsics Library

int main() {
    int data[8] = {1, 2, 3, 4, 5, 6, 7, 8};
    int result[8];

    __m256i* vdata = (__m256i*)data;
    __m256i* vresult = (__m256i*)result;
    __m256i vadd = _mm256_set1_epi32(10);

    asm volatile(
        "vmovaps ymm0, [%1]\n\t"
        "vaddps ymm1, ymm0, [%2]\n\t"
        "vmovaps [%0], ymm1"
        :
        : "r" (vresult), "r" (vdata), "r" (&vadd)
        : "ymm0", "ymm1"
    );

    printf("Result: %d %d %d %d %d %d %d %d\n", result[0], result[1], result[2], result[3], result[4], result[5], result[6], result[7]);
    return 0;
}
```
In this example, we perform SIMD addition on an array of integers using AVX instructions.

## Additional Examples and Instructions
To showcase a wider range of extended assembly usage, here are some additional examples with different assembly instructions:

### ARM Assembly - Swap Values
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20;

    asm volatile(
        "mov %0, %1\n\t"
        "mov %1, %2\n\t"
        "mov %2, %0"
        : "+r" (a), "+r" (b)
    );

    printf("Swapped: a=%d, b=%d\n", a, b);
    return 0;
}
```
This example swaps the values of `a` and `b` using ARM assembly's `mov` instruction.

### MIPS Assembly - Load Immediate
```c
#include <stdio.h>

int main() {
    int value;

    asm volatile(
        "li %0, 42"
        : "=r" (value)
    );

    printf("Value: %d\n", value);
    return 0;
}
```
This MIPS example loads the immediate value `42` into a variable using the `li` instruction.

### x86 Assembly - Bitwise AND
```c
#include <stdio.h>

int main() {
    int result;
    int input1 = 0b1010, input2 = 0b1100;

    asm volatile(
        "and %0, %1, %2"
        : "=r" (result)
        : "r" (input1), "r" (input2)
    );

    printf("Result (AND): %d\n", result);
    return 0;
}
```
In this x86 example, we use the `and` instruction to perform a bitwise AND operation.

### x64 Assembly - Calculate Square
```c
#include <stdio.h>

int main() {
    int number = 5;
    int square;

    asm volatile(
        "imul %0, %0"
        : "+r" (number)
    );

    square = number;

    printf("Square: %d\n", square);
    return
```

### ARM Assembly - Calculate Factorial
This example calculates the factorial of a number:
```c
#include <stdio.h>

int factorial(int n) {
    int result;

    asm volatile(
        "mov r1, %1\n"
        "mov r0, #1\n"
        "loop_start:\n"
        "mul r0, r0, r1\n"
        "subs r1, r1, #1\n"
        "bne loop_start\n"
        : "=r" (result)
        : "r" (n)
        : "r0", "r1"
    );

    return result;
}

int main() {
    int num = 5;
    int result = factorial(num);

    printf("Factorial of %d is %d\n", num, result);
    return 0;
}
```
In this example, we calculate the factorial of a number using ARM assembly instructions in a C function.

### MIPS Assembly - Calculate Fibonacci Sequence
This example calculates the Fibonacci sequence:
```c
#include <stdio.h>

void fibonacci(int n) {
    int a = 0, b = 1, i, c;

    asm volatile(
        "li $t0, 2\n"          // Loop counter
        "li $t2, 0\n"          // Initialize a
        "li $t3, 1\n"          // Initialize b
        "li $v0, 1\n"          // Syscall code (print integer)

        "loop:\n"
        "add $t1, $t2, $t3\n"  // Calculate c = a + b
        "move $a0, $t1\n"      // Load c into $a0 for printing
        "syscall\n"            // Print c
        "move $t2, $t3\n"      // Shift a to b
        "move $t3, $t1\n"      // Shift b to c
        "addi $t0, $t0, -1\n"  // Decrement loop counter
        "bnez $t0, loop\n"     // Branch if loop counter != 0
    );

    printf("\n");
}

int main() {
    int terms = 10;
    printf("Fibonacci Sequence (%d terms):\n", terms);
    fibonacci(terms);
    return 0;
}
```
In this example, we use extended assembly to calculate and print the Fibonacci sequence in MIPS architecture.

### x86 Assembly - Calculate Power
This example calculates the power of a number:
```c
#include <stdio.h>

int power(int base, int exponent) {
    int result;

    asm volatile(
        "movl %1, %%eax\n"    // Load base into eax
        "movl %2, %%ecx\n"    // Load exponent into ecx
        "movl $1, %%edx\n"    // Initialize result to 1

        "loop_start:\n"
        "mul %%eax\n"         // Multiply result by base
        "loop loop_start\n"
        
        "movl %%eax, %0\n"    // Store the result in output variable
        : "=r" (result)
        : "r" (base), "r" (exponent)
        : "eax", "ecx", "edx"
    );

    return result;
}

int main() {
    int base = 2, exponent = 5;
    int result = power(base, exponent);

    printf("%d^%d = %d\n", base, exponent, result);
    return 0;
}
```
In this example, we calculate the power of a number using x86 assembly instructions in a C function.

### x64 Assembly - Find Maximum
This example finds the maximum of two integers:
```c
#include <stdio.h>

int find_maximum(int a, int b) {
    int max_value;

    asm volatile(
        "cmp %1, %2\n"
        "cmovge %0, %1\n"
        "cmovl %0, %2\n"
        : "=r" (max_value)
        : "r" (a), "r" (b)
        : "cc"
    );

    return max_value;
}

int main() {
    int num1 = 42, num2 = 29;
    int max = find_maximum(num1, num2);

    printf("The maximum of %d and %d is %d\n", num1, num2, max);
    return 0;
}
```
In this example, we find the maximum of two integers using x64 assembly instructions within a C function.

## Conclusion
Extended assembly allows you to combine the power of low-level assembly with the convenience of high-level programming languages. Understanding the syntax and conventions for different architectures is essential for writing efficient and architecture-specific code. Explore the examples provided in this repository and adapt them to your specific needs.
