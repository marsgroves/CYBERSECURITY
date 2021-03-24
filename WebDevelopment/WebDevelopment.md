# Web Development

## HTTP Requests and Responses

1. What type of architecture does the HTTP request and response process occur in?

HTTP uses client-server architecture where the client makes a request from the server and the server responds back. It's sort of like talking to each other in a way or ordering something that gets delivered back.

2. What are the different parts of an HTTP request? 

Request line, request headers, and a request body.

3. Which part of an HTTP request is optional?

The request body is optional.

4. What are the three parts of an HTTP response?

The status line, the response headers, and response body.

5. Which number class of status codes represent errors?

400 status codes represent client errors. 500 status codes represent server errors. They both represent errors.

6. What are the two most common request methods that a security professional will encounter?

POST and GET requests.

7. Which type of HTTP request method is used for sending data?

POST requests.

8. Which part of an HTTP request contains the data being sent to the server?

Request body.

9. In which part of an HTTP response does the browser receive the web code to generate and style a web page?

Response body.

## Using curl

10. What are the advantages of using 'curl' over the browser?

It lets you see the response status lines and can be repeated or edited while in use.

11. Which 'curl' option is used to change the request method?

The curl option -X followed by a POST request method lets you change the request method.

12. Which 'curl' option is used to set request headers?

The curl option -H lets you add a header to a request e.g., curl google.com -H "Cookie: Session ID=John".  

13. Which 'curl' option is used to view the response header?

The curl option -I lets you view the response header.

14. Which request method might an attacker use to figure out which HTTP requests an HTTP server will accept?

The OPTIONS request method so they can figure out usable request methods from what they see.

## Sessions and Cookies

15. Which response header sends a cookie to the client?

The "Set-Cookie" response header sends a cookie to the client.

HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: cart=Bob

16. Which request header will continue the client's session?


The "Cookie" request header will send the "cart=Bob" cookie with the GET request. 

GET /cart HTTP/1.1
Host: www.example.org
Cookie: cart=Bob

## Example HTTP Requests and Responses

HTTP Request:

```HTTP
POST /login.php HTTP/1.1
Host: example.com
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 34
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.132 Mobile Safari/537.36

username=Barbara&password=password
```

17. What is the request method?

The request method is POST.


18. Which header expresses the client's preference for an encrypted response?

The Upgrade-Insecure-Requests: 1 header is the browser requesting an encrypted response.


19. Does the request have a user session associated with it?

No, because the request does not have a Cookie header set.


20. What kind of data is being sent from this request body? 

It appears that this request is an attempt to authenticate into the site's login.php page.

HTTP Response:

```HTTP
HTTP/1.1 200 OK
Date: Mon, 16 Mar 2020 17:05:43 GMT
Last-Modified: Sat, 01 Feb 2020 00:00:00 GMT
Content-Encoding: gzip
Expires: Fri, 01 May 2020 00:00:00 GMT
Server: Apache
Set-Cookie: SessionID=5
Content-Type: text/html; charset=UTF-8
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type: NoSniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block

[page content]
```

21. What is the response status code?

The response status code is 200 OK.


22. What web server is handling this HTTP response?

The web server handling this HTTP response is Apache.


23. Does this response have a user session associated to it?

Yes, which you can see from the Set-Cookie header.


24.  What kind of content is likely to be in the [page content] response body?

The site’s web code based on the content-type: text/html header.


25. If your class covered security headers, what security request headers have been included?

There are many security headers in this example, but the one covered in class would have been `Strict-Transport-Security`, which tells the client that it should only be accessed over HTTPS and not HTTP.

## Monoliths and Microservices

26. What are the individual components of microservices called?

Services.


27. What is a service that writes to a database and communicates to other services?

An Application Programming Interface or API that allows people to interact directly with back-end-like services.

28. What type of underlying technology allows for microservices to become scalable and have redundancy?

Containers which allow microservices to be both scalable and redundant.

## Deploying and Testing a Container Set

29. What tool can be used to deploy multiple containers at once?

Docker-Compose can deploy multiple containers at once using a `docker-compose.yml` file.


30. What kind of file format is required for us to deploy a container set?

A YAML file, specifically a `docker-compose.yml` configuration file that contains all of the base containers, networking, and other configurations for our container set.

## Databases

31. Which type of SQL query would we use to see all of the information within a table called 'customers'?

## SELECT * FROM customers;

32. Which type of SQL query would we use to enter new data into a table? (You don't need a full query, just the first part of the statement.)

## INSERT INTO

33. Why would we never run `DELETE FROM <table-name>;` by itself?

We would never run it because it would delete the entire table.

## Bonus Challenge Solution: The Cookie Jar

The goal for this bonus challenge was to quickly get familiar with using `curl` to save and manage cookies. Security roles that deal with testing websites will need to know how to use command-line cookies for scripting and automation.

The solution below skips Step 1: Set Up. 

## Step 2: Baselining

The goal of the baselining portion of this activity was to get you familiar with the contents of the Dashboard and what 'users.php' look like for both Administrator and Editor users. 

The later parts of the activity checked to see if curl returned these same pages.

## Step 3: Using Forms and a Cookie Jar

1.  Construct a `curl` request that enters two forms: `"log={username}"` and `"pwd={password}"` and goes to `http://localhost:8080/wp-login.php`. Enter Ryan's credentials where there are placeholders:

curl --form "log=Ryan" --form "pwd=123456" http://localhost:8080/wp-login.php

Q: Did you see any obvious confirmation of a login? (Y/N)
A: No.

2. Construct the same `curl` request, but this time add the option and path to save your cookie: `--cookie-jar ./ryancookies.txt`. This option tells `curl` to save the cookies to the `ryancookies.txt` text file:

curl --cookie-jar ./ryancookies.txt --form "log=Ryan" --form "pwd=123456" http://localhost:8080/wp-login.php

3.  Read the contents of the `ryancookies.txt` file. 