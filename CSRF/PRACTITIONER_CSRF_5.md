## Detailed Writeup of Csrf Practitioner Lab(**CSRF where token is duplicated in cookie**)

Date:- 18 January 2026
Level:- Practitioner

Here i am solving the where Csrf is duplicated a cookie means **there are two csrf token in the server** because a minimum unit of 2 is needed for duplication.

At first,we are provided the credentials given below are:-
#Username:Password

wiener:peter

At first, i get logged in to my account dashboard using the credentiasl given to us.Then i saw a email update feild in which i enter the test email and capture the request ton **Burp Suite Professional** and then i send the request to **Burp Repeater**.

The request contain four main feild stated:-
-Email and Csrf token together

-Session Cookie and Csrf value together

I tried to change the request by modifying the csrf to one end it gets failed, then i change the another token value independently and it gets also failed the request.

After trying i change the both csrf value simultaneously and it Pass The Request and get to know the vunerablity on the server that is get not verifyingthe value of csrf tokens but only verifying that the both token value should be same.

Then I created a Html field by **CSRF Poc Generator** but it is giving us the **POST** method,so i just added the **GET** request by making anathor request on the search option on server.

i Capture the request and edit my html feild as shown below:-

<html>
  <body>
    <form action="https://0a4c00fb036b0ab381038e0a0032001c.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="testinghhh&#64;evil&#46;com" />
      <input type="hidden" name="csrf" value="g1M17F5b9avMGTblxYSzt21iEZIEG" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0a4c00fb036b0ab381038e0a0032001c.web-security-academy.net/?search=hi%0d%0aSet-Cookie:%20csrf=g1M17F5b9avMGTblxYSzt21iEZIEG%3b%20SameSite=None"
        onerror="document.forms[0].submit()">
  </body>
</html>

I added different-different header like
-img src
-SameSite
-onerror

Here
**img src** is used for injecting csrf token feild to call in form.
**SameSite** is used as **none** so that we can easily call request fron anathor server too.
**onerror** is used for submitting the form forcefully as we know that this image is not available in reality.

Then i open the exploit server and store the above payload and send it to victim user by modifying the mail id and Boom! we just solved the lab.

**Key-Learning**:-A server should always validate the csrf authentication as well as the value string of token on it.

Thankyou!!!