Tree shaking is a form of dead code elimination. The term 'tree shaking' comes from the mental model of your application and its dependencies as a tree-like structure.
Each node in the tree represents a dependency. In modern apps, these dependencies are brought in via static import statement.

`import arrayUtils from "array-utils"; // Import all the array utilities!`

When your app gets bigger and bigger, some old dependencies fall out of use but may not get pruned from your code. Tree shaking addresses this by taking advantage of how we use static import statements to pull in specific parts of ES6 modules.
`import { unique } from "array-utils"; // Import only some of the utilities! Get only 'unique' export from the utils module.`

This code imports only specific parts of the module. In dev builds, nothing changes. In production build, however, we can configure webpack to "shake" off exports from ES6 modules 
that weren't explicityle imported, making the production build smaller.

Reference: https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/
