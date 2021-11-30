# TRABALHO REALIZADO NA SEMANA #6

- First, we run the server and test if it is working. After the server loads, we can do:

- echo hello | nc 10.9.0.5 9090 (after we also must press ctrl+c to finish the task in this case) -> if the server is up and running, we will receive a returned properly.

### Task 1: Crashing the program

>- For task 1 we will have to exploit the printf() and the format string. In our string we will add “%n” such as when the function prinft() is run and tries to print the string it will overwrite the return address to exit the function, meaning our program is now stuck (essentially crashing the program). Also, what has crashed is the program format.c not the server itself.
>
>- An explanation for this is that “%n” in a strings loads the variable where the pointer in located and change the value of the variable to the number of characters printed by printf() so far (before the occurrence of “%n”).
>
>![week6_0](https://cdn.discordapp.com/attachments/913904956468252695/915279478559748156/unknown.png)

### Task 2: Printing out the Server Program's Memory

>>A. The goal for task 2.a is to read the first 4 bytes of our string (the one we send to the server). For this we change our string to have the 4 bytes we want to read in the beginning (in our case we chose 0xAABBCCDD). After that, we write “%x” as many times as needed until we reach the beginning of our string, in which the content of our string is read by the printf().
>>
>>- In our case the amount of “%x” needed was 64. This number can be obtained by trial and error, however a better way to find it is to use gdb and its position and where we are in the stack.
>>
>>![week6_1](https://cdn.discordapp.com/attachments/913904956468252695/915282120258228264/week6_task2a.jpg)
>
>>B.	For task 2.b we needed to read the secret message stored in the heap area.
>>
>>- The server already gives us the address for the message, as such we can utilize of our own string and what we did in task 2.a to perform task 2.b.
>>
>>- First, we write the address of the secret message in the beginning of our string (in this case 0x080b4008).
>>
>>- Second, we know that to access the begging of our string we must use “%x” 64 times, however since this time we want to read the content of the address and not the address itself, we will do “%x” 63 times and “%s” on the 64th time, since “%s” interprets the number as an address and reads what it is in there.
>>
>>![week6_2](https://cdn.discordapp.com/attachments/913904956468252695/915282967813836911/week6_task2b.jpg)
>>
>>- The secret message was: “A secret message”.
>>
>

### Task 3: Modifying the Server Program's Memory

>>A. For this first task we needed to change the secret variable into something else.
>>- Like we have done for task 2.b we can access the address by making it the beginning of our string into it (in this case the address is 0x080e5068).
>>
>>- We know we can access it by using “%x” 64 times. To change its values from 0x11223344 to something else we can do “%x” 63 times plus “%n”. The explanation for it is the same we used to crash the server, we can write to the address the pointer is pointing to, in this case it was pointing to where the secret variable was located.
>>
>>![week6_3](https://cdn.discordapp.com/attachments/913904956468252695/915285305819537458/week6_task3a.jpg)
>
>
>
>


