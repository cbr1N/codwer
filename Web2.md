# Web Exploitation Laboratory 2
### This laboratory work is based on more web exploitation tecnhiques


## user1
**Pass:	WelcomeToCodwer**
![image](https://github.com/cbr1N/codwer/assets/95069685/1e245add-1f82-4e7f-80ff-cc61b218c289)

![image](https://github.com/cbr1N/codwer/assets/95069685/5dac2c89-50da-4d25-a8a3-e4833728538c)

Here I am given an application that shows the current date and time after clicking 'Show Time'.

![image](https://github.com/cbr1N/codwer/assets/95069685/ef9780d1-e66e-44d3-87b8-678bdbe2a340)

I noticed that the URL may have a command injection vunerability.

![image](https://github.com/cbr1N/codwer/assets/95069685/695aa46d-0e70-40c0-8fe0-9ea3bf3eadbf)

This was confirmed after ai wrote the ls command. After finding out about how the location of the flag is called, I cat the fleg.txt file.

![image](https://github.com/cbr1N/codwer/assets/95069685/bf4e1e43-561a-4321-a36d-26224dbae655)




## user2
**Pass: CWA{F1L3_UPLO4D_TURN5_T0_RC3}**

![image](https://github.com/cbr1N/codwer/assets/95069685/88332b49-106b-4931-872f-c2984fd115fd)

![image](https://github.com/cbr1N/codwer/assets/95069685/46678105-af26-41c6-960f-3ac666cfe68e)

Here I have a basic file upload interface on a local web server, which prompts users to upload a file.

![image](https://github.com/cbr1N/codwer/assets/95069685/16a5e4e5-41f0-41bf-b86f-9efe57358374)

I've created and edited a file named file and inserted PHP code that enables command execution via URL parameters.

![image](https://github.com/cbr1N/codwer/assets/95069685/e3f1a00b-7d4b-4b56-a5a0-1edc83b27097)

Then I uploaded the file to the server and got a confirmation that the file is uploaded to the server, which displays a path that suggests the files are accessible via a web browser.

![image](https://github.com/cbr1N/codwer/assets/95069685/d92e2b29-48ff-4220-8271-22d0676b64c1)

I modify the URL to execute basic shell commands (ls and cat) by exploiting the uploaded PHP script.

![image](https://github.com/cbr1N/codwer/assets/95069685/60325d41-94df-44a5-b347-6c8b72660aae)

As you can see there is no flag.txt file so I use the cat ../ command and try my luck with flag.txt.

![image](https://github.com/cbr1N/codwer/assets/95069685/9926849b-7b55-455f-9674-ae04b9786b54)

![image](https://github.com/cbr1N/codwer/assets/95069685/6e282a16-c536-40ae-bd10-48d3acae755c)

And here we have it, the password for the next user.

## user3
**Pass: CWA{F1L3_UPLO4D_TURN5_T0_RC3}**

![image](https://github.com/cbr1N/codwer/assets/95069685/c76f2d53-1b5f-47de-8935-7a38a81e0427)

![image](https://github.com/cbr1N/codwer/assets/95069685/0ca68040-f890-412a-83b9-0e12793c5248)

In this task I was given a Login application.

![image](https://github.com/cbr1N/codwer/assets/95069685/4c6a0e63-14d7-4f67-95fc-b1eb23075d6e)

I actually got the codwer user first but after trying my luck with naming the user admin and using an SQL injection, I got the password.

![image](https://github.com/cbr1N/codwer/assets/95069685/aed75af0-2f57-42a7-b98b-9b27151bdd64)


## user4
**Pass: CWA{SQL_1NJ3C71ON_3XP1oI7ED}**

![image](https://github.com/cbr1N/codwer/assets/95069685/223b4bdc-a24a-45ec-a712-6feb0aa2813a)

![image](https://github.com/cbr1N/codwer/assets/95069685/24241a13-6078-4917-9c6b-54d4b3c86342)

This task was the same as the pevious one but instead of a SQL injection I had to use a noSQL injection.

![image](https://github.com/cbr1N/codwer/assets/95069685/5f517686-dc1e-4675-b48f-8b78d37b09aa)

After trying some payloads I arrived at the conclussion that here I actually have to only insert the objects from those payloads because the message is sent in a string format by default. After writting the same payload for username and password I got the info about a user called codwer.

![image](https://github.com/cbr1N/codwer/assets/95069685/46d73748-fe8f-4f05-97ac-3782791c6af4)

So the next logical thing to do is to change the payload, only the username, to not equals codwer, so that I can get some other result, and that I got. This was the last task and the password is for root.


## root
**Pass: CWA{N0SQL_INJ3CT10N_15_4LM05T_TH3_S4M3}**

![image](https://github.com/cbr1N/codwer/assets/95069685/1def2562-460e-4af5-8001-e0cec60cd7b1)

## Lessons learned

In this laaboratory work I learned how a command injection, file upload and SQL|noSQL vulnerabilties work and how to exploit these flaws.

## Useful links

- [https://book.hacktricks.xyz/pentesting-web/command-injection]
  
- [https://book.hacktricks.xyz/pentesting-web/file-upload]

- [https://book.hacktricks.xyz/pentesting-web/sql-injection]
  
- [https://book.hacktricks.xyz/pentesting-web/nosql-injection]
