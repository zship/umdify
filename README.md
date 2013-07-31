umdify
======

umdify is a small JavaScript library for converting modules authored in AMD
format to [UMD format](https://github.com/umdjs/umd). It's useful for
distributing libraries with wide compatibility in mind. Output UMD is
compatible with AMD loaders, CommonJS loaders (like node.js), and (optionally)
browser globals.

Based on and shares the same "modify as little as possible" philosophy with
[nodefy](https://github.com/millermedeiros/nodefy).


Installation
------------

Using npm:

```
npm install umdify
```


Usage
-----

### *String* umdify( *String* contents, *String* [moduleName] )

Converts `contents` (a valid AMD JavaScript module) to UMD format. `moduleName`
is only required if you want to support browser globals, and will be the name
of the exported `window` property.

Example (node.js):

```js
var fs = require('fs');
var umdify = require('umdify');

var contents = fs.readFileSync('src/myModule.js', 'utf8');
contents = umdify(contents);
fs.writeFileSync('dist/myModule.js', contents);
```

Want to do a bulk convert? I won't stand in your way. How about
[node-glob](https://github.com/isaacs/node-glob)?

```js
var fs = require('fs');
var path = require('path');
var glob = require('glob');
var umdify = require('umdify');

var files = glob.sync('src/**/*.js');
files.forEach(function(file) {
	var contents = fs.readFileSync(file, 'utf8');
	contents = umdify(contents);
	var dest = path.join('dist', file.replace(/^src\//, ''));
	fs.writeFileSync(dest, contents);
});
```


License
-------

Released under the [MIT
License](http://www.opensource.org/licenses/mit-license.php).
