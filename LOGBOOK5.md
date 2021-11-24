# TRABALHO REALIZADO NA SEMANA #5

### Task 1: Getting Familiar with Shellcode

- When running the code we are able to get to the root shell with both the 32bit and 64bit (the a32.out and a64.out). This is because our system is 64bit but it also have compatibility with 32bit.
- What the code does is copy the shellcode (string of the code that calls the shell) to the stack (in char code[500]).
- Then we forced the code to be and int and were able to call the codeshell using func(). SO, with this we are able to have access to root shell.

### Task 2: Understanding the Vulnerable Program

- This task was a preparation for task 3. We first had to turn off some protections linux has by default. Then we had to give onwership to stack.c to root and give the current user of calling the program with root premissions.
- For task 3 we needed stack-L1 so we checked that it had a buffer of size 517.

### Task 3: Launching Attack on 32-bit Program (Level 1)

- Lorem ipsu

# CTF

- Lorem ipsu
