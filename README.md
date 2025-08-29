# Reverse-Engineering

> You can't reverse engineer what you don't under stand

## Terminiologies

### Process and Memory

- Each process have an ID associated with it and we use that to manipulate the process and the resource around it

| 32-Bit Process        | 64-Bit Process        |
| --------------------- | --------------------- |
| Address Size: 4 Bytes | Address Size: 8 Bytes |
| WORD: 2 Bytes         | WORD: 2 Bytes         |
| DWORD: 4 Bytes        | DWORD: 4 Bytes        |
| QWORD: 8 Bytes        | QWORD: 8 Bytes        |

> DWORD = Double word
> QWORD = QUAD word

- Memory consists of multiple blocks which are called pages
- Each page has certain properties such as:
  - Range of addresses: 0X0000 - 0XFFFF
  - Security Flags: RWX
  - Page Type: Commited || Reserved

### Shellcode

- Assembly code that acheives a specific purpose

  - Think of it as a payload that executes a shell command

- Our main goal is to bypass anti-viruses and EDRs and Avoid Detection which is the reason for using shellcode
- We'll encyrpt the shell code with something like RC4 encryption and in runtime it gets decrypted and executed

### Windows API

- The `ddl` provided by windows API have tons of functions
- It also provides custom type definition
- Some windows APIs return a pointer to a structure, we'll need a predefined struct to store the data returned by a certain windows API

```c
BOOL Process32First(
    [in]     HANDLE hSnapshot,
    [in, out] LPPROCESSENTRY32 lppe
);

BOOL Process32Next(
    [in]     HANDLE hSnapshot,
    [in, out] LPPROCESSENTRY32 lppe
);
```

- It uses the LPPROCESSENTRY32 struct, if function succeeds it's filled information related to certain process like Process name and ID
- We can import these structs from windows header `#include <windows.h>`

## Tools

1. Process Hacker
2. Hex Editor
