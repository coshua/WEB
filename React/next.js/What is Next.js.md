
In Nextjs, a page is a React component exported from a file in the 'pages' directory.

### Link
You use the 'Link' component from 'next/link' to wrap the '<a>' tag.
  
The Link component enables client-side navigation between two pages in the same app. It means the page transition happens using JavaScript.

Next.js does code splitting automatically, so each page only loads what's necessary for that page.

In a production build of Next.js, whenever 'Links' appear in the browser's viewpoint, it prefetches the code for the linked page in the background.
So when you click the link, the code for that page is already loaded, and the page transition is very fast.
