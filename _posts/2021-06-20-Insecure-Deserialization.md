![](https://miro.medium.com/max/1108/1*zVwdJyQL6FH4L5WTcYH3yQ.png)

Hello and welcome to this blog, in this blog we're going to discover what insecure deserialization is ? we're going to take some code examples and some exploitation scenarios in PHP & Python, solving 2 labs from Portswigger as well, without wasting any time; let's go !

Serialization vs Deserialization:
=================================

-   Serialization: it's the process of converting objects to some form of data to save it in a file, database or memory, this data is sent and received in a stream of bytes, the purpose of serialization can be saving data to later uses or using it in order to send the data over a network, between different components of the application or over an API.

NOTE: programming languages support serialization, but every programming language has a different approach to deal with the process of serialization, however to make this process general and programming_language-independent; applications use formats like JSON and XML etc.., also serialization has some abbreviations in other programming languages, like marshalling in Ruby and pickling in Python !

-   Deserializaion: it's the reverse process of Serialization, the purpose of deserialization is restoring the object in a reserved manner in order to restore the object with its attributes etc.. exactly as it was in the first before serialization !

![](https://miro.medium.com/max/700/1*pRMxQpC0KkFPj2ko2aNzlQ.jpeg)

Serialization vs Deserialization

Insecure Deserializtion ?
=========================

What's Insecure Deserialization ? well, let's take it easy, did you remember the serialization ? we said that some data is serialized in order to use it, if this data is a user-controllable data and in Deserialization this data passes without validation, then it's absolutely an Insecure Deserialization.

An attacker can also replace the serialized object with another object from other classes as well, that's why this vulnerability is called for examples in PHP; Object Injection, however if an object is injected from unexpected class; an exception may arise.

Insecure Deserialization is used to achieve arbitrary code execution [RCE], Privilege Escalation (we'll see that in labs), access control bypass, Denial Of Service etc...

Mitigation
==========

some applications use some checks and validations in a blacklisting manner, however those checks can be bypassed with some additional effort, the right approach is never ever deserialize user-controllable data, if that isn't possible, digital signature is needed in order to add some integrity checks; encryption can also be used to prevent users from reading data and next to change it or just understand the pattern in which they're created !

Examples [Python & PHP]
=======================

Let's take some examples from PHP, can we exploit Insecure Deserialization (Object Injection) in PHP ?

Example 1 [Privilege Escalation]:
=================================

let's consider an application with user and admin privileges, a session cookie contains serialized object with role attribute, the value is user, however the application has already a mechanism to handle user and admin privileges, can we bypass it ? can we achieve a Privilege Escalation ?

this is the PHP code:

```php
<?php
    $user = unserialized($_COOKIE);
    if ($serialized['role'] == 'administrator') {

        // Admin Privileges Code
    }

    else {
      // User Privileges Code
    }
?>
```

well, here is the issue, the object is deserialized in unsafe manner, there is no validation or integrity check; an attacker could change the role attribute's value from user to administrator and he will achieve a full Privilege Escalation !!!

Example 2 [Price Parameter Tampering]:
======================================

in example 2, let's consider a shopping application where users can buy things, a cart cookie will contain a checkout attribute, the value is the total of items, let's say $1000, can we change this price with a flaw in application logic using an Insecure Deserialization ? let's do it :)

```php
<php?
    $cart = unserialized($_COOKIE);

    if ($cart) {
       $total_amount = $cart['checkout'];
    }

   // other code
?>
```

the issue in this example is that a user can control the total_amount without any validation, when the if condition is set to true (the cart cookie is sent in the HTTP request), total_amount variable is set to the value of checkout's attribute !! the attacker could easily change the value to something like 0, so the total_amount will change from $1000 to $0 !!

Now, it's Python :) let's check this example of python code that is vulnerable to Insecure Deserialization, we will use pickle module here, the process is called pickling in python.

Example 1 [RCE]:
================

```python
import pickle

with open('payload', 'r') as file:
     pickle.loads(file.read())
```

the issue here is that the code performs an insecure deserialization, which will load the file that's called payload without any validation or check, however an attacker could generate a serialized payload which will contain an OS command like whoami, when the code is executed, the attacker will receive the result of the whoami command, it's an RCE !!

Labs:
=====

Lab1 [Privilege Escalation]:
============================

let's solve this lab from Portswigger Academy, the required action here is to achieve Admin privileges and delete the account of a user called carlos, let's jump in :)

After the login process with a normal user privileges, this is the vulnerable app:

![](https://miro.medium.com/max/700/1*aQewMMZiGiW4JAvrm6msmg.png)

normal user's interface

now, let's reload the page and intercept the request with Burp:

![](https://miro.medium.com/max/700/1*GJskeOxKtuihtHgW3qeScA.png)

the session cookie contains a base64 encoded string, if we decode it using an online tool like [CyberChef](https://gchq.github.io/) we should get this object string: O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:0;}, the interesting part is the admin attribute's value which is a boolean 0, that means that it's false !! i think that is a condition, let's try to change it to 1. so the object now should be O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:1;}, we'll encode the object string to base64 format in the session cookie and sending the request using Burp's repeater tab.

let's see the response:

![](https://miro.medium.com/max/437/1*f1HMzWFaKFG2sBqdiSrwFA.png)

Boom !! i'm admin now ! let's try to request using GET method the /admin endpoint and search for carlos which is the user that we're going to delete his account in order to solve this lab:

![](https://miro.medium.com/max/437/1*vnjtq96hHim5y4lo_7fkcw.png)

we have here two users, me (wiener) and carlos, let's delete the account of carlos by requesting the /admin/delete?username=carlos endpoint using the GET method.

![](https://miro.medium.com/max/700/1*PVOyvVlTewtiEufMheYj2w.png)

Solved !!

Lab2 [Authentication Bypass]:
=============================

to understand the solution of this lab, we must understand how PHP handles the data types, PHP by origin is a loosely typed language in the == operator, which means that it looks just for the value not the data types of the two operands, let's understand this with the following code:

```php
<?php
   $value_1 = 10;
   $value_2 = "10";

   if ($value_1 == $value_2) {

       echo "Same !";
   }

?>
```

as you see, value_1 is an integer (whole number) but the value_2 is a string, even the two values are the same without considering the data types, the if condition using the == operator looks for the equality between the two values without looking for data types, so the condition will evaluate to true and therefore the echo statement will be executed to print Same !.

The second thing is that 0 with == operator creates an interesting issue to investigate. let's study the following code:

```php
<php?
      $string = "Welcome to my blog !";
      if (0 == $string) {
          echo "Same !";
      }
?>
```

string variable is a string (data type), the if condition is comparing 0 with our string variable, well, the if condition will evaluate to true and therefore the echo statement's going to execute, but why ?

PHP is a loosely typed language as i said before, so our string doesn't contain any integer like 9, 10 or 8 ... 0 integer is there, condition is true ! Same ! should be printed somewhere !

the purpose of this lab is to bypass the authentication to achieve an account with admin privileges, however let's look for a vulnerable code for the same situation and how we can achieve an authentication bypass from a source code and therefore solve the lab, a serialized object is transmitted in a session Cookie during an HTTP request. let's check this code:

```php
<php?
    $serial = unserialized($_COOKIE);

    // $password variable in the if condition is a pre-defined
    // password for admin

    if ($serial['password'] == $password) {
        // admin login  success!
    }
?>
```

the code above demonstrates a small authentication mechanism implemented in PHP, well it's vulnerable to Insecure Deserialization which is a good bug to bypass authentication, the user-controllable data which is the serialized object contains a password attribute, the value is the user's supplied password, the condition is comparing the password's attribute value with a predefined admin password, do you remember the 0 and PHP Loosely typed notation ! i bet that you remember it ! the attacker would change the serialized-object in the password attribute's value from some password to 0 ! now if the admin password doesn't start with a number, the login will be successful and therefore the authentication mechanism is bypassed !

now, we understand what's going on with PHP, let's solve the lab !

considering a serialized-session based mechanism, the required action is to bypass authentication in order to delete the account of carlos, let's jump in !

after login as a normal user, a default normal user interface is introduced, let's reload the page and intercept the request with Burp, the session cookie contains a base64 encoded string, let's decode it and see what's going on, the received result is this object O:4:"User":2:{s:8:"username";s:6:"wiener";s:12:"access_token";s:32:"sfzfvdy6lk5y3k5wd24tipbrdgsj8ggf";} with a user_name that's set to wiener and an access token, the important thing to note here is that there is an s in the object, which is the data type label, s for string, i for integer and so on ... there is also after the s: some number, this number is the length of the corresponding attribute/value ! so we must change things here very carefully !

i tried first to change the username attribute's value to admin but i get a 500 Internal Server Error in the response, so let's try to change it to administrator but remember that we must change the length in the object from 6 to 13, but we get again a Server Error, so the issue here is the access_token, let's write some PHP code to just create an imagination of the situation:

```php
<php?
    $serial = unserialized($_COOKIE);

    // $admin_access_token is a pre-defined variable that contains
    // the access token of the admin !
    if($serial['username'] == 'administrator' &&
       $serial['access_token'] == $admin_access_token) {

           // admin logic code here !
       }
?>
```

let's try to see, yes i see that you understand :) see here the == operator, the first operand will get the access_token's value, comparing it with a predefined admin_access_token, if the admin_access_token string doesn't start with a number, an attacker could change the value of access_token's value from sfzfvdy6lk5y3k5wd24tipbrdgsj8ggf for example to 0 as an integer value in order to evaluate the condition to true and therefore executing the admin logic code !! Please return to 0 and == notation to understand more !

we have already this object O:4:"User":2:{s:8:"username";s:6:"wiener";s:12:"access_token";s:32:"sfzfvdy6lk5y3k5wd24tipbrdgsj8ggf";}, let's change the username attribute's value to administrator with a length of 13 and also the access_token attribute's value to 0 with a data type label of integer [i], so the new object now is:

O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}

we're going now to encode this new object with the base64 encoding format, sending it in the session cookie in the HTTP POST request and see what's the server response.

![](https://miro.medium.com/max/439/1*Bp6FxX5w0XfQlK2jaCqxdw.png)

Boom, we're admin now !! after navigating to admin endpoint, let's try to request /admin/delete?username=carlos:

![](https://miro.medium.com/max/700/1*8mmL4RHxIjd-sxjiOmb_eg.png)

Awesome, solved !

NOTE: in the deserializing process of objects, it reserves the data types which means that integer is integer and string is string !! in normal requests with objects, data types are converted to be compatible with the situation !

Another Note: my English isn't that good, so please expect some grammar errors, technical errors are also expected !

for carlos, i'm sorry for deleting your account 2 times, please forget about that and create a new account :(

Thanks for reading, i hope you understand what Insecure Deserialization is and i hope that code examples are supporting materials to understand it more !! if you have any questions, edits, technical/language error fixes, you're welcome to contact me at akhrazmoad14@gmail.com.

![](https://miro.medium.com/max/220/1*IXviPWr1jkTX4PtIWVgVvQ.gif)

Cheers, @mdakh404
