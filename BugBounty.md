# codwer.academy Bug Bounty
### This writeup is about bug bounty and some new information may be added

## Basic Insecure Direct Object References (IDOR) vulnerability

### Example1

![image](https://github.com/cbr1N/codwer/assets/95069685/3dfaaeea-285a-48b3-9b56-bd27f6e082ed)

Here I am viewing my own submission, its ID being 84. But we can actually change it from 84 to, for example, 24.

![image](https://github.com/cbr1N/codwer/assets/95069685/ae59882c-28ec-4ae2-836e-d3352d31f741)

And now I can view someone else's submission. I shouldn't be able to do that, hence the vulnerability.
I will use it for future exploitations.

### Example2

![image](https://github.com/cbr1N/codwer/assets/95069685/7bf169b3-a2a7-4699-94ea-aaba331875ad)

Here I intercepted a GET request for viewing my own submissions. If I change the userId from 51 to 32, I will be able to see the submissions of the user with thier id set to 32.

![image](https://github.com/cbr1N/codwer/assets/95069685/dd77fb38-c43f-465a-b95b-d4d5c1ad4ed0)

![image](https://github.com/cbr1N/codwer/assets/95069685/e293bba6-8bd8-48d3-9d58-04ecdbedbf25)

Not only am I able to view the user's submissions, I am also able to freely delete them. The method is verified and I did delete someone else's submission (with consent of course).

### Example3

![image](https://github.com/cbr1N/codwer/assets/95069685/e9f69bc3-0e97-47f5-9ad6-23f79290fa8a)

Here I created a submission with a file attachement. The vulnerability lies in downloading this file.

![image](https://github.com/cbr1N/codwer/assets/95069685/b8fc4981-1b80-440b-865b-e3a4d75abbb7)

Here I intercept another GET request. If I change the ID of the file from 31 to 8, it downloads the contents of the 8th file submitted to the website.

![image](https://github.com/cbr1N/codwer/assets/95069685/725f872e-0e0d-42ed-b21d-203b2e422685)

![image](https://github.com/cbr1N/codwer/assets/95069685/db38c1c4-e6cd-4ce8-8316-94c6e7f028e7)

Here are the content's of the 8th file. As you can see the name and contents are different from the file I posted.

## Brute Force Attacks

This is not an actual vulnerability, more of a sugestion. I tried brute forcing my way through the log in page using the admin@codwer.com mail. After my attempt with hydra I got this.

![image](https://github.com/cbr1N/codwer/assets/95069685/c027bce0-9f83-4b6f-b7c8-b9d291fa62da)

This is the most basic method to deal with such attacks, but there are many downs.

- An attacker can cause a denial of service (DoS) by locking out large numbers of accounts.

- Because you cannot lock out an account that does not exist, only valid account names will lock. An attacker could use this fact to harvest usernames from the site, depending on the error responses.

- An attacker can cause a diversion by locking out many accounts and flooding the help desk with support calls.

- An attacker can continuously lock out the same account, even seconds after an administrator unlocks it, effectively disabling the account.

- Account lockout is ineffective against slow attacks that try only a few passwords every hour.

- Account lockout is ineffective against attacks that try one password against a large list of usernames.

- Account lockout is ineffective if the attacker is using a username/password combo list and guesses correctly on the first couple of attempts.

- Powerful accounts such as administrator accounts often bypass lockout policy, but these are the most desirable accounts to attack. Some systems lock out administrator accounts only on network-based logins.

- Even once you lock out an account, the attack may continue, consuming valuable human and computer resources.

## Scans 
### Here I am using different tools to scan for vulnerabilities

![image](https://github.com/cbr1N/codwer/assets/95069685/2fdaba85-0900-4664-b9d9-ffe63f7fced7)

Here I used nikto for a general fast scan. 

The anti-clickjacking X-Frame-Options header is not present. This header helps protect against clickjacking attacks.
The X-Content-Type-Options header is not set. This header prevents the browser from interpreting files as a different MIME type than what is specified by the server.

![image](https://github.com/cbr1N/codwer/assets/95069685/12131d82-776c-4e4c-bc1e-f53f6a1efea1)

After using wapiti and using my own JWT token I got this new vulnerability.

X-XSS-Protection is not set: This header is used to configure the built-in reflective XSS protection found in some web browsers. Without this header, the website may be more susceptible to cross-site scripting (XSS) attacks, where attackers can inject client-side scripts into web pages viewed by other users.
