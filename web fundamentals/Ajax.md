With AJAX, you can update the page without reloading the page. You can request and receive data from a server after the page has loaded. In the meantime, the page send data to a server.

It is abbreviated of Asynchronus Javascript And XML. It is not a programming language. It is just a combination of a browser built-in XMLHttpRequest object and Javascript, HTML DOM.

The procedure is
1. An event occurs in the page
2. An XMLHttpRequest object is created by Javascript.
3. The object sends a request to a web server.
4. The server processes the request.
5. The server sends a response back to the web page.
6. The response is read by Javascript.
7. User defined action is performed by Javascript using response.

A simple example is following

```Javascript
function reqListener () {
  console.log(this.responseText);
}

var oReq = new XMLHttpRequest();
oReq.addEventListener("load", reqListener);
oReq.open("GET", "http://www.example.org/example.txt");
oReq.send();
```

