# Binary Bomb: Phase Solutions

Welcome to the **Binary Bomb** repository! This repository contains solutions for the Binary Bomb challenge, which is designed to enhance your understanding of x86-64 assembly, debugging, and reverse engineering techniques. This README provides detailed solutions for each phase of the bomb using insights gathered from various analysis files.

## Table of Contents

1. [Overview](#overview)
2. [Tools Needed](#tools-needed)
3. [Understanding the Binary Bomb](#understanding-the-Binary Bomb)
4. [Phase-by-Phase Solutions](#phase-by-phase-solutions)
   - [Phase 1](#phase-1)
   - [Phase 2](#phase-2)
   - [Phase 3](#phase-3)
   - [Phase 4](#phase-4)
   - [Phase 5](#phase-5)
   - [Phase 6](#phase-6)
   - [Secret Phase](#secret-phase)
5. [Conclusion](#conclusion)

## Overview

The **Binary Bomb** challenge involves a binary executable that simulates a "bomb" with multiple phases, each requiring a specific input to "defuse" it. Providing the wrong input causes the bomb to "explode," necessitating a retry. The objective is to reverse engineer the binary and determine the correct inputs for each phase using various debugging and reverse engineering tools.

## Tools Needed

To successfully defuse the bomb, you will need the following tools:

- **GNU Debugger (gdb)**: For step-by-step execution and inspection of binary code.
- **objdump**: To disassemble the binary and analyze the assembly code.
- **strings**: To find readable strings within the binary.
- **Hex editor**: (optional) To view and manipulate the binary at the byte level.

## Understanding the Binary Bomb

The **Binary Bomb** challenge consists of several phases, each requiring a specific input to pass. If the wrong input is entered, the bomb "explodes," and you need to start again. The goal is to defuse the bomb by figuring out the correct inputs for each phase.

## Phase-by-Phase Solutions

### Phase 1

**Objective**: Find the correct input string.

**Resources Used**: `gdb bomb.txt`, `strings.txt`

**Solution**:
- Using `strings bomb`, readable strings are extracted from the binary. One of the strings is a quote: "And they have no disregard for human life."
- Use `gdb` to set a breakpoint at the beginning of the `phase_1` function. Step through the disassembled code (`disas` command) and observe the comparison between the input string and a stored value.
- The correct string is identified from memory comparison and matches the extracted string.
- **Answer**: `And they have no disregard for human life.`

### Phase 2

**Objective**: Solve a mathematical sequence.

**Resources Used**: `gdb bomb.txt`

**Solution**:
- Set a breakpoint at `phase_2` and run the program in `gdb`.
- Step through the code and notice a pattern that doubles the previous number.
- Based on the observed pattern, the sequence follows powers of two.
- **Answer**: `1 2 4 8 16 32`

### Phase 3

**Objective**: Understand a switch-case statement and provide the correct inputs.

**Resources Used**: `User.txt`, `Untitled-3.txt`

**Solution**:
- Use `gdb` and `objdump` to analyze `phase_3`.
- This phase involves a series of comparisons using `cmp` and `jmp` instructions.
- Disassembled code reveals multiple comparisons and conditional jumps. Through careful analysis, the values that do not trigger a `jmp` to the bomb explosion (`explode_bomb`) function are identified.
- Correct input values `2 r 572` are derived by meeting all the comparison checks without triggering the explosion.
- **Answer**: `2 r 572`

### Phase 4

**Objective**: Reverse a function that requires precise inputs to avoid recursion overflow.

**Resources Used**: `Untitled-3.txt`

**Solution**:
- In `gdb`, examine the recursive function calls in `phase_4`.
- The correct inputs are identified by satisfying all conditions for return values without triggering infinite recursion.
- Debugging through `gdb` shows that using values `99 3 DrEvil` prevents the bomb from exploding.
- **Answer**: `99 3 DrEvil`

### Phase 5

**Objective**: Analyze an array and provide the correct values based on pointer arithmetic.

**Resources Used**: `gdb bomb.txt`

**Solution**:
- The `phase_5` function manipulates an array using pointers.
- The disassembly reveals index calculations that map input to desired output values.
- The correct inputs are identified to match expected outputs through debugging and analyzing memory contents.
- **Answer**: `5 115`

### Phase 6

**Objective**: Follow linked list pointers and sort values in the correct order.

**Resources Used**: `gdb bomb.txt`

**Solution**:
- Using `gdb`, trace the linked list manipulation in `phase_6`.
- Understand the sequence of pointer traversal and sorting required to arrange the nodes correctly.
- Correct inputs are identified to successfully sort the list without triggering the bomb.
- **Answer**: `4 2 3 5 1 6`

### Secret Phase

**Objective**: Enter a secret phase and provide the correct value.

**Resources Used**: `strings.txt`

**Solution**:
- The string “Wow! You've defused the secret stage!” indicates there is a hidden phase.
- Analyze the binary for any hidden functions and identify the conditions for entering this secret phase.
- Inputting `20` defuses the bomb in this secret stage.
- **Answer**: `20`

## Conclusion

By carefully analyzing each phase using reverse engineering techniques and debugging tools, we successfully defused the **Binary Bomb**. This challenge provides an excellent opportunity to develop skills in binary analysis, low-level debugging, and reverse engineering.

Feel free to explore the repository further and try your own approaches to defusing the bomb!

Happy Defusing!
