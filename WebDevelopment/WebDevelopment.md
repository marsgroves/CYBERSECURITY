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

## 