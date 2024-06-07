# Web Explotation Laboratory 1
### This laboratory work is based on web explotation tecnhiques


## user1
**Pass:	WelcomeToCodwer**

![image](https://github.com/cbr1N/codwer/assets/95069685/40ca05f2-1b2c-4582-96bb-6cb2d235951b)

![image](https://github.com/cbr1N/codwer/assets/95069685/7669b6a1-4704-4d8d-882c-f2659867928f)

I accessed the car rental management system running on port 81 of a local server (`localhost:81`). This was a web-based application where users could input details to find car rental availability.

![image](https://github.com/cbr1N/codwer/assets/95069685/fd141896-f73f-4538-a743-e7f1829010a8)

![image](https://github.com/cbr1N/codwer/assets/95069685/6787ba98-b70a-421d-afc2-496c191d31b0)

I examined the web page source code and noticed URLs with parameters that suggested potential manipulation points. I discovered a URL exploit that included base64 encoding (`.php?page=php://filter/convert.base64-encode/resource=flag`). This indicated a potential method to view server-side files through base64-encoded filters.

![image](https://github.com/cbr1N/codwer/assets/95069685/31865c83-53d5-4658-9c59-ed270b97eefa)

I manipulated the URL to exploit a Local File Inclusion (LFI) vulnerability by using PHP filters to encode the contents of the flag.php file in base64. This allowed me to access the contents of `flag.php` without directly viewing the file on the server.

![image](https://github.com/cbr1N/codwer/assets/95069685/cd55ff41-1e26-4d54-ad19-a13c5b57872f)

After successfully obtaining the base64-encoded string of the `flag.php` file, I used a command line to decode it (`echo "base64_string" | base64 --decode`). This revealed the PHP code that contained the flag, which was a password or token used in my exercise.

## user2
**Pass: CWA{D15CL053_Y0UR_F1L35**
![image](https://github.com/cbr1N/codwer/assets/95069685/48a253b3-5790-46df-863d-db350588d541)

![image](https://github.com/cbr1N/codwer/assets/95069685/268c8bb3-b10b-4b02-a9cb-270f3f8ce5b5)

I accessed a website where I encountered a registration form. Here, I created a user account with a simple username and password.

![image](https://github.com/cbr1N/codwer/assets/95069685/1c72c819-43a1-4151-8845-cfceba2dfc4d)

After registering, I navigated through different user profiles on the site using the Insecure Direct Object References (IDOR) vulnerability.

![image](https://github.com/cbr1N/codwer/assets/95069685/493a34ef-738f-42cf-86b9-d58b01e51b1f)

![image](https://github.com/cbr1N/codwer/assets/95069685/2a121f1a-585e-4275-9296-e0d4a00adc17)

On the profile page of the user named '`flaggiver`', I found the description containing the flag.



## user3
**Pass: CWA{1_d0n7_0r64n1z3_r4v35**

![image](https://github.com/cbr1N/codwer/assets/95069685/14cd3aaf-9da2-4976-97cc-1a1d8c3cd8a1)

![image](https://github.com/cbr1N/codwer/assets/95069685/7e16b0fb-b178-48d8-b4eb-9ce675bcb415)

The application displays a basic login form where I can enter a username and password.

![image](https://github.com/cbr1N/codwer/assets/95069685/8412d2a0-6b14-4691-bdfe-4a69a1ac7b1c)

After viewing the source code I can see the useraname and password of a `user`.

![image](https://github.com/cbr1N/codwer/assets/95069685/4259cb8f-dbf6-4135-bfd9-2e26dc2540b0)

I use this information to log in.

![image](https://github.com/cbr1N/codwer/assets/95069685/7f44a5d6-9411-432a-8930-728e1369e08e)

Right now I am a user. If the challenge has to do with JWT then the next step is to inspect this user's jwtToken.

![image](https://github.com/cbr1N/codwer/assets/95069685/02345a5a-109b-4e4d-aa22-077ecc8c4a2a)

I don't need this key because I will use the `jwt.io` website.

![image](https://github.com/cbr1N/codwer/assets/95069685/01d12204-c9de-4c76-af3e-d37c3143fb87)

I notice that the role is set to "`user`". This role is likely what controls access to different parts of the application.

![image](https://github.com/cbr1N/codwer/assets/95069685/27cdfe68-7f77-489e-847d-8ca9afbbbb90)

In the JWT, I change the role field from "`user`" to "`admin`" in hopes of elevating my privileges within the application. 

![image](https://github.com/cbr1N/codwer/assets/95069685/6cf95677-5940-4095-ab9b-06b2e2bb046d)

After modifying the JWT and updating it in my browser cookies, I refresh or navigate through the application to trigger a re-evaluation of my session.
The application now recognizes me as an "`admin`" based on the altered JWT, granting access to the admin page.

![image](https://github.com/cbr1N/codwer/assets/95069685/756c3e6c-5189-4721-a909-f5f3bad1536a)



## user4
**Pass: CWA{Jw7_5ucc355fullY_D3cod3d}**
![image](https://github.com/cbr1N/codwer/assets/95069685/2aac6272-672f-4974-b854-5b7b5c3ec6e6)

![image](https://github.com/cbr1N/codwer/assets/95069685/2015f711-010f-4b2e-89cc-b35347ed4e4c)

I unzip the contents of the contents of the application.

![image](https://github.com/cbr1N/codwer/assets/95069685/2b7b0f94-ef46-4a6e-8bce-1fdd3d14521c)

I access the `Task3` directory and within it the Controllers directory. I ope the `AuthController.cs` file to read its contents.

![image](https://github.com/cbr1N/codwer/assets/95069685/3eadf9a9-cbce-46c0-9e13-3c50fe07015f)

The `AuthController.cs` file contains routes for `Login()` and `SuperSecretPage()` methods.
Notably, the `SuperSecretPage()` method lacks proper authorization checks (`[Authorize] attribute`), making it potentially accessible without appropriate security credentials. This is a security vulnerability as it allows unauthorized access to what seems to be a sensitive part of the application.

![image](https://github.com/cbr1N/codwer/assets/95069685/d485f322-da07-41a0-8cfe-985cce76548a)

Accessing the `localhost:84/supersecret` URL in a browser shows a message about a "`Policy escape`" and displays the flag. The message warns that simple users can see the page, indicating a security flaw where restricted content is viewable without proper permissions.

## root
**Pass: CWA{Endp01nt_P0l1c3s_Appl13d_Succ3ssfully}**

![image](https://github.com/cbr1N/codwer/assets/95069685/54f1f9fa-ac36-49bc-ba50-fd22f8a2af98)


## Lessons learned
Understanding Web Vulnerabilities: This laboratory work provided practical insights into various web exploitation techniques such as `Local File Inclusion (LFI)`, `Insecure Direct Object References (IDOR)`, `JSON Web Token (JWT) manipulation`, and improper authorization handling in web applications. These examples demonstrated how attackers can exploit these vulnerabilities to gain unauthorized access or information.

Authentication and Authorization Flaws: Exploring vulnerabilities in authentication and authorization mechanisms, such as weak session management (`JWT manipulation`) and absent security checks (lack of proper `[Authorize]` attributes), highlighted the critical need for robust security protocols in web applications.

## Useful links

- [https://token.dev]
  
- [https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion]

- [https://github.com/lutfumertceylan/top25-parameter/blob/master/lfi-parameters.txt]
  
- [https://hacktricks.boitatech.com.br/pentesting/pentesting-web/php-tricks-esp/php-useful-functions-disable_functions-open_basedir-bypass]
  
- [https://jwt.io]
