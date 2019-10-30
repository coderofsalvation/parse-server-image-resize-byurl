Flexible Parse server middleware to resize images on demand:

* http://my.parse.server/api/files/myproject/72243e65cd8af516dbc8a67b344.PNG?w=200
* http://my.parse.server/api/files/myproject/72243e65cd8af516dbc8a67b344.PNG?w=700

> It resizes on demand, or serves a cached file after the first requests

Fast performance: it clamps imagesizes:

* ?w=200 => resizes to width of 200px 
* ?w=260 => resizes to width of 300px 
* ?w=320 => resizes to width of 400px 

## Installation

    $ npm install parse-server-image-resize-byurl

now add it as express middleware:

```
var cfg {

    ...

    filesAdapter: {
        module: 'parse-server-fs-store-adapter',
        options: { filesSubDirectory: 'data/files' }
    }
}

var parse = new ParseServer(cfg)

var app = express()
app.use( require('parse-server-image-resize-byurl')(cfg.filesAdapter.options.filesSubDirectory) )
```

Now you can just use Parse imagefiles as usual, and add the `?w=xxxx` resize-option to urls.