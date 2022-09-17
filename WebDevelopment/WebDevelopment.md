# Web Development

## HTTP Requests and Responses


HTTP uses client-server architecture where the client makes a request from the server and the server responds back. It's sort of like talking to each other in a way or ordering something that gets delivered back.

Different parts of an HTTP request include the **request line, request headers, and a request body**.

The **request body** is optional.

The three parts of an HTTP response are: **status line, the response headers, and response body.**

The number class of status codes that represent errors are:
`400` status codes represent client errors. `500` status codes represent server errors. They both represent errors.

Two of the most common request methods that a security professional will encounter are `POST` and `GET` requests.

`POST` requests are used for *sending data*.

The **request body** *contains the data* being sent to the server.

A browser receives web code to generate and style a web page in the **response body** of an HTTP response.

## Using curl

Using **curl** lets you see the response status lines and can be repeated or edited while in use.

The *curl option* `-X`followed by a POST request method lets you change the request method.

The *curl option* `-H` lets you add a header to a request e.g., curl google.com -H "Cookie: Session ID=John".  

The *curl option* `-I` lets you view the response header.

The `OPTIONS` request method can be accepted by an HTTP server and used by an attacker to can figure out what request methods they can use from what they can see.


## Sessions and Cookies

The `Set-Cookie` response header sends a cookie to the client. See example below.

`HTTP/1.1 200 OK
Content-type: text/html
**Set-Cookie**: cart=Bob`

The `Cookie` request header will continue the client's session by sending the `cart=Bob` cookie with the GET request. 

`GET /cart HTTP/1.1
Host: www.example.org
Cookie: cart=Bob`

## Example HTTP Requests and Responses

Example of an HTTP Request:

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

The request method is `POST`.

The `Upgrade-Insecure-Requests*: 1` header is the browser requesting an encrypted response.

The request shown in the example above does **NOT** have a session associated with it because the request DOES NOT have a `Cookie` header set. 

It appears that data being sent from the request body is an attempt to *authenticate into the site's login.php page* (see username and password details).


# HTTP Response

Here is an example of an HTTP response.

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

The *response status code* is `200 OK`.

The web server handling this HTTP response is **Apache**.

This response has a user session associated with it because it has a **Set-Cookie** header and **SessionID=5**.

The site's web code is the content most likely to be in the *[page content]* part because in the **Content-Type** part of the HTTP response, you can see it contains **text/html** 

There are many security headers in this example, such as `Strict-Transport-Security`, `X-Content-Type`, `X-Frame-Options`, and `X-XSS-Protection` that have various purposes. For exanple, `Strict-Transport-Security` tells the client that it should only be accessed over HTTPS and not HTTP.


## Monoliths and Microservices

The individual components of microservices are called **services**.

An **Application Programming Interface (API)** is a service that writes to a database and communicates to other services. It allows clients to interact directly with back-end-like services.

**Containers** are an underlying technology that allows microservices to become scalable and redundant. Thus, containerization is a great choice for scalability and redundancy.


## Deploying and Testing a Container Set

`Docker-Compose` can deploy multiple containers simultaneously via a `docker-compose.yml` file.

A YAML file, specifically a `docker-compose.yml` configuration file is required for the deployment of a container set. It contains all of the base containers, networking, and other configurations for our container set.

## Databases (e.g., SQL queries)

An SQL query can request information from a table. For example, to see all of the information within a table called 'customers' we need to make an SQL query that looks like this:
`SELECT * FROM customers;`

32. Which type of SQL query would we use to enter new data into a table? (You don't need a full query, just the first part of the statement.)

This is the SQL query we would use to enter new data into a table:
`INSERT INTO`

We would never run `DELETE FROM <table-name>;` by itself because it would delete the entire table.

## Bonus Challenge: The Cookie Jar

The goal for this bonus challenge was to quickly get familiar with using `curl` to save and manage cookies. Security roles that deal with testing websites will need to know how to use command-line cookies for scripting and automation. So I created command-line cookies using forms in the demonstration below with the Editor Ryan's credentials.

After completing steps one and two, that is, setting up and completing baselining where I got familiar with the contents of the dashboard and saw the Administrator and Editor users in the *users.php* file, I decided to construct a curl request. I found a user with Editor credentials named Ryan from the list. Let's skip to step 3 now.

## Step 3: Using Forms and a Cookie Jar

I constructed a **curl** request that enters two forms: `"log={username}"` and `"pwd={password}"` and goes to `http://localhost:8080/wp-login.php`. In this example, I entered Ryan's credentials where there are placeholders, and it looks like this.

`curl --form "log=Ryan" --form "pwd=123456" http://localhost:8080/wp-login.php`

After constructing my curl request using forms, I did not get an obvious confirmation of a login.

So what did I do?

I constructed the same **curl** request, but this time I added the option and path to save your cookie: 
`--cookie-jar ./ryancookies.txt` 

This option tells `curl` to save the cookies to the `ryancookies.txt` text file:

`curl --cookie-jar ./ryancookies.txt --form "log=Ryan" --form "pwd=123456" http://localhost:8080/wp-login.php`

Now I proceeded to read the `ryancookies.text` file.

After reading the contents of the **ryancookies.text** file, **I found 4 cookies** in the `ryancookies.txt` file.

## Step 4: Log in Using Cookies

Next, I crafted a new **curl** command that now uses the **--cookie** option, followed by the path to your cookies file. For the URL, use `http://localhost:8080/wp-admin/index.php` like this:

`curl --cookie ./ryancookies.txt http://localhost:8080/wp-admin/index.php`

It is not yet obvious that we can access the Dashboard with this new curl command using the **--cookie** option.

So I pressed the up arrow on my keyboard to run the same command, but this time, I would pipe `| grep Dashboard` to the end of my command to return all instances of the word **Dashboard** on the page which looks like this:

`curl --cookie ./ryancookies.txt http://localhost:8080/wp-admin/index.php | grep Dashboard`

A: Next, I looked through the output where **Dashboard** is highlighted. After adding the grep pipe, I can see all occurrences of the word ‘Dashboard’ within the returned response body, showing us a successfully returned ‘index.php‘ session which allows me to log into the Editor's dashboard.

## Step 5: Test the Users.php Page

Finally, write a **curl** command using the same `--cookie ryancookies.txt` option, but attempt to access `http://localhost:8080/wp-admin/users.php`:

`curl --cookie ./ryancookies.txt http://localhost:8080/wp-admin/users.php`

After doing this, I saw the warning ‘You need a higher level of permission. Sorry, you are not allowed to list users.’ Because these are not Admin credentials, we were unable to access it, but at least we gained access to the Editor's dashboard.
