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

## Notes to consider while constructing your deps.js for your project:

### 1. Root blocks and elements start from naming a file, therefore it's optional to create the following file with the following data:

For the file named: `b1.deps.js` write according to this pattern:

```js
    ({
      block : 'b1',
      mustDeps : { block : 'b2' }
    })

    ({
      mustDeps : { block : 'b2' }
    })
```
