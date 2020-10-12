## Introduction
Script tags in html file are perhaps larger than the html or css element in the document. Thus, it occupies the most of the time the browser would spend on loading the page.
Moreover, it prevents other low-size content to be loaded until it finishes downloading or loading.
For providing a better user experience, we need to tell broswer the order and priority in our html file, because only we know the workflow.

Besides of many other methods, we will see three primary methods to optimize the rendering, script defer, script async and dynamic script. The first two are attributes for script tag, which means we can easily handle it without any outside help.
### Defer
Browser downloads defered script in the background. It can parse HTML during its downloading. And the run of the script is 'defered' until DOM is ready.

`<script defer src="..."></script>`

Defered script runs **after** DOM is ready and **before DOMContentLoaded** event.

If you load multiple scripts with defer attribute, the small size content may be downloaded first. However, it runs in the order they specified in the HTML file.

### Async
Async scripts are downloaded in the background as well. So HTML parses asynchronously.

You cannot sure which of DOMContentLoaded event and async script execution occurs first. Async script runs immediately when its ready.
Neither you sure about which script runs first, which means async script runs regardless of the order in the HTML document. We call this 'load-first order'.

### Dynamic
You can write dynamic script in the document using JavaScript. It works exactly as the way async script works.
```javascript
let script = document.createElement('script');
script.src = "https://example.com/externalCND/long.js";
document.body.append(script); // (*)
// You can assure the order script runs by specifying `script.async = false`
```
It starts download at *.
