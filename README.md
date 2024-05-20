# xv6 Copy on Write (CoW) Implementation

This project adds Copy on Write (CoW) functionality to the xv6 operating system kernel. CoW is a memory management technique that allows multiple processes to share the same memory pages until one of them tries to modify the shared memory. At that point, a copy of the memory page is created, ensuring that each process has its own writable copy.

## Overview

The CoW implementation in xv6 involves modifying the fork system call to create a new page table for the child process and implement CoW semantics for memory pages. Additionally, a user library function named `enable_cow(int enable)` and the corresponding system call are added to control CoW functionality dynamically.

## Implementation Details

- **Modified fork System Call:** 
  - Create a new page table for the child process.
  - Implement CoW semantics for memory pages, allowing shared access until a write operation occurs.
  
- **User Library Function:** 
  - Implement `enable_cow(int enable)` to dynamically enable or disable CoW functionality at runtime.
  
- **Page Fault Handling:** 
  - Handle page faults when a process attempts to write to a read-only memory page.
  - Create a copy of the page and update page tables accordingly.

## Testing

Thorough testing is essential to ensure the correctness and performance of the CoW implementation. The provided test program `cowtest.c` contains test cases to validate the CoW functionality in various scenarios, including shared memory access and write operations.

To test the CoW implementation:
1. Compile the xv6 kernel with the CoW feature enabled.
2. Run the `cowtest` program to execute the test cases.
3. Verify the test results to ensure correct behavior and performance.

## Usage

To enable or disable CoW functionality at runtime, use the `enable_cow(int enable)` user library function. Pass `1` to enable CoW and `0` to disable it.

```c
#include "types.h"
#include "user.h"

int main() {
    // Enable CoW
    enable_cow(1);

    // Perform operations with CoW enabled

    // Disable CoW
    enable_cow(0);

    // Perform operations with CoW disabled

    return 0;
}
```

## Disclaimer
This project should not be used for university coursework projects. The contributors are not responsible if individuals are caught for plagiarism or academic dishonesty while using this project for such purposes.

