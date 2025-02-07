# Malloc-Free-Simulator

## **Overview**
This project implements a **custom memory allocator** that provides `malloc()` and `free()` functionality within a fixed **4KB** memory block. The allocator manages memory allocation and deallocation using a **linked-list-like approach** to track free and occupied memory blocks.

## **Files**
- **`mymalloc.h`** – Defines the memory block and function prototypes.
- **`mymalloc.c`** – Implements `mymalloc()` and `myfree()` with memory management logic.
- **`memgrind.c`** – Runs multiple test cases to evaluate allocator performance.
- **`testplan.txt`** – Documents test cases and expected behaviors.

## **Memory Allocation and Freeing**
### **Allocation (`mymalloc`)**
- Prevents allocation of sizes `< 1 byte` or `> 4094 bytes` (to accommodate metadata).
- Splits larger free blocks if necessary to optimize memory usage.
- Returns a pointer to the allocated memory or prints an error if allocation fails.

### **Deallocation (`myfree`)**
- Marks memory blocks as free.
- Merges adjacent free blocks to reduce fragmentation.
- Prevents double freeing and freeing unallocated memory.

## **Testing (`memgrind.c`)**
The `memgrind` program includes multiple test cases to evaluate performance and edge cases:

- **Test A**: Repeatedly allocates and frees small memory blocks.
- **Test B**: Allocates and frees memory in a loop with arrays.
- **Test C**: Randomly allocates or frees memory until full.
- **Test D**: Allocates variable-sized blocks and deallocates them.
- **Test E**: Tests invalid memory operations (e.g., freeing unallocated memory, double frees).
- **Test F**: Demonstrates block merging after freeing.
- **Test G**: Determines the maximum number of 1-byte allocations possible.

## **Running the Tests**
Compile and run the program using:
```sh
gcc -o memgrind memgrind.c mymalloc.c
./memgrind
```

## **Expected Errors and Edge Cases**
- **Invalid allocations** (negative or zero sizes, exceeding max limit).
- **Double free** detection.
- **Merging adjacent free blocks** after deallocation.
- **Memory exhaustion** handling when allocation fails.
