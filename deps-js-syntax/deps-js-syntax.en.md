# The Syntax for `deps.js`

## The complete implimentation of the deps object:

```js
    {
        block : 'bBlock',
        elem  : 'elem',
        mod   : 'modName',
        val   : 'modValue',
        tech  : 'techName',    // file extention for this dependency (e.g. if javaScript `tech : '.js'`)
        mustDeps   : [  ],     // Array of blocks connected to this dependency
        shouldDeps : [  ],     // The order of connected blocks is not important (important that they connect)
        noDeps : [  ],         // It's possible to exclude some blocks, for example: `[ 'i-bem__dom_init_auto' ]`
    }
```
