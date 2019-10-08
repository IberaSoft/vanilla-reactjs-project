# Vanilla ReactJS
Create React Project without create-react-app


> Step by step guide to start a simple ReactJS project

[![License](https://github.com/IberaSoft/vanilla-reactjs-project/blob/master/LICENSE)](http://badges.mit-license.org)

## Quick Start

1- Open your terminal and clone the repository on your disk

```
git clone --depth=1 https://github.com/IberaSoft/vanilla-reactjs-project.git
```

2- Remove the .git folder

```
cd vanilla-reactjs-project
rm -rf .git
```

3- Install all of the node dependencies and packages required by the project.

```
npm i
```

## Step by Step Guide

Create a directory in your system

```
mkdir my-app
```

Go to the directory

```
cd my-app
```

Create package.json file
```
npm init -y
```
> npm init will create new package.json file (Flag -y will tell npm to use all default config option while creating package.json)

Install react and react-dom
```
npm install react react-dom
```
> it will add react and react-dom under dependencies in package.json file as well as it create node_modules directory with all other dependent libraries in it.

Create gitIgnore to avoid pushing unnecessary code to github
```
vim .gitignore
```
Possible items you need in your gitignore file are:
node_modules
.DS_Store/     # If you're on mac machine
.vscode/       # If you IDE is vscode
node_modules   # Folder with all dependencies
dist           # Distribution folder

Create app folder
```
mkdir app
```

Create 3 files within it
```
cd app && touch index.html index.js index.css
```

Open index.html and copy paste the following code:
```
<!DOCTYPE html>
<html>
    <head><title>my-app</title></head>
    <body>
        <div id="app"></div>
    </body>
</html>
```

Open index.js and start writing your first component:
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';

const App = () => <div>Hello World!</div>

ReactDOM.render( < App / > , document.getElementById('app'))
```

> At this point, if you try to run the code above, it will give an error as that code is written in JSX and the browser does not understand it. To solve that, we will need install some dependencies...

On your Terminal
```
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli webpack-dev-server babel-loader css-loader style-loader html-webpack-plugin
```

> Flag --save-dev : we use this flag to differentiate out build dependencies than our app dependencies (check your package.json file in order to see how this flag differentiate in that)

## Webpack configurations

Webpack is module bundler. So currently we only have on module. However, as our app expands we will have more modules. So webpack intelligently bind all those modules together and creates one single file which serves all these.

```
cd .. && touch webpack.config.js
```

And copy the following code:

```
var path = require('path');
var HtmlWebpackPlugin =  require('html-webpack-plugin');

module.exports = {
    entry : './app/index.js',
    output : {
        path : path.resolve(__dirname , 'dist'),
        filename: 'index_bundle.js'
    },
    module : {
        rules : [
            {test : /\.(js)$/, use:'babel-loader'},
            {test : /\.css$/, use:['style-loader', 'css-loader']}
        ]
    },
    mode:'development',
    plugins : [
        new HtmlWebpackPlugin ({
            template : 'app/index.html'
        })
    ]

}
```

In conjuction with out babel-loader works we have to add babel preset config to our ***package.json*** file

```
"main": "index.js",
"babel":{
    "presets" : [
      "@babel/preset-env",
      "@babel/preset-react"
    ]
  }
```

To run the build we have to add webpack to our script tag in our ***package.json***

```
"main": "index.js",
  "babel":{
    "presets" : [
      "@babel/preset-env",
      "@babel/preset-react"
    ]
  },
  "scripts": {
    "create": "webpack"
  },
```

So when you run ***npm run create*** from terminal it will run the webpack which will create the dist folder and our bundle file with index.html file.

It's hassle to run webpack every time. So you can start a webpack dev server. so it will start build your code as soon as you run it.
Modify your script in package.json with following:

```
"scripts": {
    "create": "webpack",
    "start": "webpack-dev-server --open"
  }
```

Now when you run ***npm run start*** it will start the dev server and open your app in the browser.

## Final directory structure will look like this

```
app
|_ index.css
|_ index.html
|_ index.js

dist
|_ index_bundle.js
|_ index.html

node_modules
|_ .gitignore
|_ package-lock.json
|_ package.json
|_ webpack.config.js
```

## License

- [MIT license](https://github.com/IberaSoft/vanilla-reactjs-project/blob/master/LICENSE)
- Copyright 2019 © <a href="http://iberasoft.com" target="_blank">IberaSoft</a>.