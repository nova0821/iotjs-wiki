IoT.js follows the practice of node.js npm to provide module development community but with separate registry.

* To see what it actually is, please visit [www.npmjs.com](https://www.npmjs.com/), and also [docs.npmjs.com](https://docs.npmjs.com/).
* To avoid confusion with the original server, we'll call it "ipm", for IoT.js Package Management
* Current status of "ipm" is for developers. it has no separate web page. we will provide some neat user interface web pages when we are ready.
* "npm" program is used for publish and download modules

### Installing "npm"
```
sudo apt-get install npm"
```

### Setting registry

As ipm uses different server you need to change registry information
```
npm config set registry="http://ipm.iotjs.net:5984/registry/_design/app/_rewrite"
```

### Adding your account

You may have to register your account if you plan to publish some packages
```
npm set init.author.name "Your Name"
npm set init.author.email "you@example.com"
npm set init.author.url "http://yourblog.com"
npm adduser
```


### Publish a package

cd to your package folder and init
```
npm init
```

It'll ask information for your package, for an example;
```
Press ^C at any time to quit.
name: (t) echotest
version: (1.0.0) 0.0.1
description: simple echo server
entry point: (index.js)
test command:
git repository:
keywords:
license: (ISC)
About to write to /(your working folder)/package.json:
{
  "name": "echotest",
  "version": "0.0.1",
  "description": "simple echo server",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "(your name) <your email address> (your blog page)",
  "license": "ISC"
}
 
Is this ok? (yes) yes
```

and all things are good to go, publish.
```
npm publish ./
```


Please visit [npmjs.org](https://docs.npmjs.com/getting-started/publishing-npm-packages) for detailed explanation.
