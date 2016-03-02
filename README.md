# NodeJS and Rapid Development

## Using NodeJS you can build a rapid development enviroment

### package.json
```bash
{
  "name": "NodeJS-Rapid-Development",
  "version": "1.0.0",
  "description": "NodeJS-Rapid-Development: Using NodeJS for rapid devlopement",
  "dependencies": {
    "connect": "^3.4.0",
    "connect-inject": "^0.4.0",
    "serve-static": "^1.10.0"
  },
  "cordovaPlugins": [
    "cordova-plugin-device",
    "cordova-plugin-console",
    "cordova-plugin-inappbrowser",
    "cordova-plugin-whitelist",
    "cordova-plugin-splashscreen",
    "com.ionic.keyboard",
    "phonegap-plugin-push"
  ],
  "cordovaPlatforms": []
}
```

### dev.js
```bash
var connect = require('connect');
var serveStatic = require('serve-static');
var fs = require('fs');
var port = 8080;
var base = "/www"

console.log('Serving directory ' + __dirname +base);
console.log('Running server on port ' + port);
connect()
	.use(require('connect-inject')({
		ignore: ['.js', '.css', '.svg', '.ico', '.woff', '.png', '.jpg', '.jpeg','scss'],
		runAll: true,
		rules: [
			{
				match: /<!doctype html>/ig,
				snippet: '',
				fn: function(w, s) {
					return '';
				}
			},
			{
				match: /<head>/ig,
				snippet: '',
				fn: function(w, s) {
					return w + s;
				}
			}
		]
	}))
	.use(serveStatic(__dirname+base))
	.listen(port);
```

