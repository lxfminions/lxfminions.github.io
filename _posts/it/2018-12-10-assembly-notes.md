---
layout: post
title: Assembly Lauages
categories: [it]
tags: [Assembly, x86_64]
date: 2018-12-08
---
{% include tip.html content="Notes of x86_64 Assembly Language Programming with Ubuntu" %}

## Why Learn Assembly Langage
- Gain a better understanding of architecture issues
- Understanding the tool chain---about the process of high language to machine language
- Improve algorithm development skills
- Improves understanding of functions/procedures
- Gain an understanding of I/O buffering
- Understand compiler scope
- Introduction to multi-processing concepts

## Architecture Overview
### Data stroage size
Storage | Size(bits) | Size(bytes)
--------|------------|------------
 Byte   |   8-bits   |   1 byte
 Word   |   16-bits  |   2 bytes
 Double-word | 32-bits | 4 bytes
 Quadword | 64-bits | 8 bytes
 Double quadword | 128-bits | 16 bytes

### Central Processing Unit (CPU)
  The Arithmetic Logic Unit (ALU) which is the part of the chip that actually **performs the arithmetic and logical calculations.** In order to support the ALU, **[processor registers](https://en.wikipedia.org/wiki/Arithmetic_logic_unit)** and cache memory are also included "on the die" (term for inside the chip).


#### CPU Registers
A CPU register is a temporary storage or working location built into the CPU itself (separate from memory).
1. General Purpose Registers (GPRs)
  - `rax` stands for 64-bits, `eax` stands for the lowest 32-bits,
  `ax` stands for the lowest 16-bits, and `al` stands for the lowest 8-bits.
  In the `ax` register, `ah` stands for the highest 8-bits.
  - 16 GPRs, `r{a,b,c,d}x`, `r{s,d}i`, `r{b,s}p`, `r{8,9,10,11,12,13,14,15a}[d,w,b]`

2. Dedicated purposed as belows:
  - Instruction Pointer Register (RIP): point ot **the next instruction to be execued.**
  - Stack Pointer Register (RSP): point to the current top of the stack.
  - Base Pointer Register (RBP): as a base pointer during function calls.

3. Flag Register (rFlags): used for status and CPU control information. The
**rFlag** register is <span style="color: red">updated by the CPU after each intruction and not accessible by programs.</span>

Name | Symbol | Bit | Use
-----|--------|-----|----
Carry| CF | 0 | Used to indicate if the previous operation resulted in a carry
Parity | PF | 2 | Used to indicate if the last byte has an even number of 1's
Adjust | AF | 4 | Used to support Binary Coded Decimal operations
Zero | ZF | 6 | Used to indicate if the previous operation resulted in a zero result
Sign | SF | 7 | Used to indicate if the result of the previous operation resulted in a 1 in the most significant bit (indicating negative in the context of signed data)
Direction | DF | 10 | Used to spicify the direction (increment or decrement) for some string operators
Overflow | OF | 11 | Used to indicate if the previous operation resulted in an overflow

### Main Memory
1. Memory is **byte addressable**. So, it can be view as a series of bytes, one after another.
2. x86-64 is little-endian architecture. This means **the least significant Byte (LSB)** is store in the lowest memory address. **The most significant Byte (MSB)** is store in the highest memory location.


## Data Representation
### Integer Representation
- For pepresenting **unsigned values** within the range of a given storage size, standard binary is used.
- For representing **signed values** within the range, **two's complement** is used.
  
#### How to find the two's complement for negative values?
1. Byte Example
   
 9 (8+1)= | 0000 1001
 ---------|----------
 Step 1 | 1111 0110
 Step 2 | 1111 0111
 -9(in hex) | F7

2. Word Example
   
18 (16+2)= | 0000 0000 0001 0010
-----------|--------------------
Step 1 | 1111 1111 1110 1101
Step 2 | 1111 1111 1110 1110
-18 | 0xFFEE

#### The best explaination about the two's complement for me
More detail infomation, refer to [What is "2's complement"?](https://stackoverflow.com/questions/1049722/what-is-2s-complement) in Stackoverflow.

Here is my understanding about two's complement.
##### Symmetry

9 (8+1)= | 0000 1001
---------|----------
Step 1   | 1111 0110
Step 2   | 1111 0111
-9(in hex) | F7

Similarly, do the same operation for -9.

-9(2's complement) = | 1111 0111
---------------------|----------
Step 1 | 0000 1000
Step 2 | 0000 1001
9 (in binary) | 0000 1001

Wow! 9 after doing the above operation is -9, and in reverse -9 in two's complement does is 9.

##### **Exception**
Since it's binary, there have to be an even number of possible can be paired with its negative.
But there's only one zero. Negating a zero gets you zero. So there's one more combination, the
number with **1** in the sign bit and **0** everywhere else. The corresponding positive number would
not fit in the number of bits being used.

##### How are we to understand that to mean -9?   
The awser is that we change the meaning of the high-order bit (the leftmost one). This bit will be a **1**
for all negative numbers. The change will be to change the sign of its contribution to the value of the number
it appears in. So now our **1111 0111** is understood to represent
$$ -1 \times 2^7 + 1 \times 2^6 + 1 \times 2^5 + 1 \times 2^4 + 
   0 \times 2^3 + 1 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 = -9 $$

So, **-128** or **1000 0000** in two's complement means
$$  -1 \times 2^7 + 0 \times 2^6 + 0 \times 2^5 + 0 \times 2^4 + 
   0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 0 \times 2^0 $$