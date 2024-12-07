# Fancy Names Challenge - Hack The Box

## Overview
The "Fancy Names Challenge" from Hack The Box involves exploiting a binary that mimics a game setup. Players can choose names, adjust stats like strength and health, and even create custom stats. The binary contains a vulnerability due to improper handling of memory allocations, specifically related to how freed memory is reused.

## Vulnerability
The main flaw lies in the binary's memory allocation for user inputs, such as custom names, which uses `malloc`. The vulnerability is a result of the incorrect reuse of freed memory, potentially allowing an attacker to manipulate memory management, overwrite function pointers, and execute arbitrary code.

## Exploit
The provided exploit script in Python uses the `pwntools` library to interact with the binary over a network. It demonstrates how to:
- Leak memory addresses to determine the location of libc and calculate offsets.
- Use heap manipulation techniques to perform a tcache poisoning attack.
- Overwrite the `__malloc_hook` with a one-gadget address to execute arbitrary code and retrieve the flag.

## Requirements
- Python 3
- pwntools library
- An instance of the challenge binary and the corresponding libc version running on a remote server or locally.

## Setup and Execution
1. Ensure Python 3 and pwntools are installed on your system.
2. Modify the script with the correct remote address and port if running against a remote target.
3. Run the script using the command: `python3 exploit.py`.

## Files
- `exploit.py`: Contains the full exploit code to interact with the binary and exploit the vulnerability.
- `fancy_names`: The vulnerable binary (provided by Hack The Box).
- `.glibc/libc.so.6`: The version of libc used by the binary, necessary for accurate offset calculations.

## Note
This exploit is for educational purposes only. Make sure you have permission to attack the target and are not violating any laws or terms of service.

