# TRABALHO REALIZADO NA SEMANA #6

- First, we run the server and test if it is working. After the server loads, we can do:

- echo hello | nc 10.9.0.5 9090 (after we also must press ctrl+c to finish the task in this case) -> if the server is up and running, we will receive a returned properly.

### Task 1: Crashing the program

>- For task 1 we will have to exploit the printf() and the format string. In >our string we will add “%n” such as when the function prinft() is run and >tries to print the string it will overwrite the return address to exit the >function, meaning our program is now stuck (essentially crashing the program). >Also, what has crashed is the program format.c not the server itself.
>
>- An explanation for this is that “%n” in a strings loads the variable where >the pointer in located and change the value of the variable to the number of >characters printed by printf() so far (before the occurrence of “%n”).

![week6_0](https://cdn.discordapp.com/attachments/913904956468252695/915279478559748156/unknown.png)

### Task 2: Printing out the Server Program's Memory

>A. The goal for task 2.a is to read the first 4 bytes of our string (the >one we send to the server). For this we change our string to have the 4 bytes >we want to read in the beginning (in our case we chose 0xAABBCCDD). After >that, we write “%x” as many times as needed until we reach the beginning of >our string, in which the content of our string is read by the printf().
>
>>- In our case the amount of “%x” needed was 64. This number can be obtained >>by trial and error, however a better way to find it is to use gdb and its >>position and where we are in the stack.
>
>![week6_1](https://cdn.discordapp.com/attachments/913904956468252695/915281546418745364/unknown.png)
