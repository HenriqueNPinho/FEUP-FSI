# TRABALHO REALIZADO NA SEMANA #5

### Task 1: Getting Familiar with Shellcode

- When running the code we are able to get to the root shell with both the 32bit and 64bit (the a32.out and a64.out). This is because our system is 64bit but it also have compatibility with 32bit.
- What the code does is copy the shellcode (string of the code that calls the shell) to the stack (in char code[500]).
- Then we forced the code to be an int and were able to call the codeshell using func(). SO, with this we are able to have access to root shell.

### Task 2: Understanding the Vulnerable Program

- This task was a preparation for task 3. We first had to turn off some protections linux has by default. Then we had to give onwership to stack.c to root and give the current user of calling the program with root premissions.
- For task 3 we needed stack-L1 so we checked that it had a buffer of size 517.

### Task 3: Launching Attack on 32-bit Program (Level 1)

- First we created a dummy badfile to gather information about stack-L1. Then we opened the debug file for stack-L1 (stack-L1-dbg) file in gdb to gather the information we needed. (See image below)

![task3_1](https://cdn.discordapp.com/attachments/903555414715670578/913194194229678080/task3_11.png)

- Then we ran the commands to gather info (things like "b bof", "run" and etc). From that we got the ebp (which in our case was 0xFFFFCA18) and the address of the start of the buffer (0xFFFFC9AC). (See images below)

![task3_2](https://cdn.discordapp.com/attachments/903555414715670578/913194194485522433/task3_22.png)
![task3_3](https://cdn.discordapp.com/attachments/903555414715670578/913194194720411688/task3_33.png)
![task3_4](https://cdn.discordapp.com/attachments/903555414715670578/913194195009802261/task3_44.png)
![task3_5](https://cdn.discordapp.com/attachments/903555414715670578/913194195265667122/task3_55.png)

- With the information collected we are now to actually create the actual badfile with the help of exploit.py, however first we need to change some infomation in it.

![task3_6](https://cdn.discordapp.com/attachments/903555414715670578/913194195508920341/task3_66.png)

- The information we changed and how we got/calculated them is:
- 1) start : We changed this infomration to "490", the reason for this number is because the buffer has a size of 517 and our shellcode has a size of 27bytes, and we decided to put our shellcode at the end of the buffer, and 517-27=490. 
-  (in this case, since we can point exactly to our shellcode, it is not necessary but if we put the shellcode at the end in normal condition, we are able to "miss" the pointer but have our code have 0s with means jump to the next instruction. Eventually we get to our shellcode).

- 2) ret: This is the return in which we want to change to point to our shellcode. We know that the buffer starts at 0xFFFFC9AC and that its size is 517. We put our shellcode 27bytes before the end so at 0xFFFFC9AC + 490 (in decimal). This gave our return address which was 0xFFFFCB96.

- 3) offset: This is where we need to inject our return adress that points to our shellcode. We now that return we want to change is after the ebp, we also know that the ebp has a size of 4 bytes. If we 0xFFFFCA18 (ebp address) - 0xFFFFC9AC (buffer address) we get that the ebp starts at 108 bytes after the buffer. Then we add the size of the ebd (the 4 bytes) and we get 112, which is the place of the return we want to modify.

Running the exploit:

- We open the terminal where exploit.py and stack-L1 is located. We run exploit.py creating the badfile we need to use the exploit. Then we run stack-L1 and get access to rootshell. (See image below) 

![task3_7](https://cdn.discordapp.com/attachments/903555414715670578/913194197522219069/task3_77.png)

# CTF

- Lorem ipsu
