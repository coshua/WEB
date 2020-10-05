### CORS?
Cross-Origin Resource Sharing is a mechanism that allows a web application to access to selected resources from a different origin. 
We say two URLs have the same origin if the protocol, port, and host are the same for both.

For security reasons, broswers restrct cross-origin HTTP requests. XMLHttpRequest and the Fetch API follow this policy. 

However, web applications using those APIs can request resources from the different origin the application was loaded if the response includes the right CORS headers.


Resources: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
