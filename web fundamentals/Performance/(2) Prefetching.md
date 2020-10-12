## Prefetching
Resource prefetching is a technique to tell the browser which assets the user might need in the future.
Think of the circumstance where you want to transite from existing image to the new one. It is critical to ensure that the browser do not spend a significant time loading the new one.
Here is the place for prefetching.

## Prebrowsing
This practice of guessing what users need before they need it is has been called prebrowsing. It consists of a number of techniques. Let's look through them.

### DNS prefetching
This notifies the client that thare are assets we will be use from a URL so the browser can resolve the DNS as quickly as possible.
This is accomplished by one line. 

`<link rel="dns-prefetch" href="//example.com">`

Chrome does something like this all the time, so it saves miliseconds off each request.

### Preconnect
By initiating early preconnects, the browswer can set up the necessary sokcets ahead of time and eliminate the DNS, TCP, and TLS roundtrips from the critical path of the request.

`<link rel="preconnect" href="https://css-tricks.com">`

### Prefetching
If we know we need a specific resource later, we can make browser to request that item and store it in the cache for reference later.

`<link rel="prefetch" href="image.png">`

This is commonly used for loading webfonts, which have to wait until the DOM and CSSOM is constructed before they even download.

### Subresources
If you want to specify the priority of the prefetched resource, you can do it with subresource link.
Subresources have highest priority to be loaded.

`<link rel="subresource" href="styles.css">` //It should be placed on the head of the document.

### Prerendering
As the name implies, it renders a whole page to be ready to be used.

`<link rel="prerender" href="https://example.com">`

If the user navigates to the specified href, then the pre-rendered page is swapped into view making it appear to load instantly.

Resources
---
See more on https://css-tricks.com/prefetching-preloading-prebrowsing/
