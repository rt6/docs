# Javascript / NodeJS / MEAN Stack 

## 1) NVM
```sh
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
$ nvm install node
$ nvm ls
```

## 2) Express Restful API Backend

```sh
$ npm install express-generator -g
$ expres my-new-app
$ cd my-new-app
$ npm i
```

The above will create the below structure:
```
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.jade
    ├── index.jade
    └── layout.jade
```

## 3) User Authentication and Login using Passport

Install these packages
```
$ npm i --save passport-local passport passport-local-mongoose
```


### Setup Babel and Nodemon
So you use ES6 in express source code, and watch file changes which restarts express automatically

install packages using devDepndencies flag (-D)
```sh

npm i -D babel babel-cli babel-core babel-preset-es2015 nodemon
```
create `.babelrc`:
```js
{
    "presets": ["es2015"]
}
```

add npm commands to scripts section of `package.json` :
```js
"scripts": {
  "build": "node_modules/babel-cli/bin/babel.js ./ --source-maps --out-dir dist",
  "start": "node_modules/nodemon/bin/nodemon.js -- node_modules/babel-cli/bin/babel-node.js server.js"
}
```
Note: You may want to call it "dev" instead "start".


Now you can start the server in bash with: 
```
$ npm start
```

## 4a) React Web Frontend

- coming soon

# 4b) React Web Frontend with Semantic UI

- coming soon

# 5) React Native Mobile App

- coming soon
