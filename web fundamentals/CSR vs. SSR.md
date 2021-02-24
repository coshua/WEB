To determine whether the application is rendered client-side or server-side, you should consider this question: 'Where do you want the work to happen?'

## Routing
### SSR
The adjustment of URL requests a whole new page from the server. The GET request is sent to the server which responds with a new document, completely discarding the old page altogether.
### CSR
A client-side route happens when the route is handled internally by the JavaScript that is loaded on the page. When a user clicks on a link, the URL changes but the request is prevented.
The adjustment to the URL results in a changed state of the application. The changed state results in a different view of the webpage. 
This could be the rendering of a new component, or even a request to a server for some data that the application will turn into some HTML elements.
It is important to note that the whole page won't refresh when using client-side routing. There are some elements inside the applciation that changes
