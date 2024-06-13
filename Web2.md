# Web Exploitation Laboratory 2
### This laboratory work is based on web exploitation tecnhiques


## user1
**Pass:	WelcomeToCodwer**
![image](https://github.com/cbr1N/codwer/assets/95069685/1e245add-1f82-4e7f-80ff-cc61b218c289)

![image](https://github.com/cbr1N/codwer/assets/95069685/5dac2c89-50da-4d25-a8a3-e4833728538c)

![image](https://github.com/cbr1N/codwer/assets/95069685/ef9780d1-e66e-44d3-87b8-678bdbe2a340)

![image](https://github.com/cbr1N/codwer/assets/95069685/695aa46d-0e70-40c0-8fe0-9ea3bf3eadbf)

![image](https://github.com/cbr1N/codwer/assets/95069685/bf4e1e43-561a-4321-a36d-26224dbae655)




## user2
**Pass: CWA{F1L3_UPLO4D_TURN5_T0_RC3}**

![image](https://github.com/cbr1N/codwer/assets/95069685/88332b49-106b-4931-872f-c2984fd115fd)

![image](https://github.com/cbr1N/codwer/assets/95069685/46678105-af26-41c6-960f-3ac666cfe68e)

![image](https://github.com/cbr1N/codwer/assets/95069685/16a5e4e5-41f0-41bf-b86f-9efe57358374)

![image](https://github.com/cbr1N/codwer/assets/95069685/e3f1a00b-7d4b-4b56-a5a0-1edc83b27097)

![image](https://github.com/cbr1N/codwer/assets/95069685/d92e2b29-48ff-4220-8271-22d0676b64c1)

![image](https://github.com/cbr1N/codwer/assets/95069685/60325d41-94df-44a5-b347-6c8b72660aae)

![image](https://github.com/cbr1N/codwer/assets/95069685/9926849b-7b55-455f-9674-ae04b9786b54)

![image](https://github.com/cbr1N/codwer/assets/95069685/6e282a16-c536-40ae-bd10-48d3acae755c)

## user3
**Pass: CWA{1_d0n7_0r64n1z3_r4v35**

![image](https://github.com/cbr1N/codwer/assets/95069685/c76f2d53-1b5f-47de-8935-7a38a81e0427)




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
