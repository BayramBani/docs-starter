# Webpack
---

## basic

- project

```text
app
|- src/index.js
|- index.html
|- package.json
```

- install

```bash
npm install webpack webpack-cli --save-dev
# or
yarn add webpack webpack-cli --dev
```

- ' package.json '

```json
{
  "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
  }
}
```

- ' ./src/index.js'

```javascript
console.log('hello webpack !');
```

- ' ./index.html '

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo</title>
</head>
<body>
<script src="dist/main.js"></script>
</body>
</html>
```

- for development
 
```bash
npm run dev
```

- for production

```bash
npm run build
```

## css loader

- install

```bash
npm install css-loder style-loader --save-dev
```

- ' webpack.config.js '

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader','css-loader']
      }
    ]
  }
};
```

## bootstrap

- install

````bash
npm install bootstrap jquery popper.js
````

- './src/index.js'

````javascript
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.css'

document.getElementById('root').innerHTML = '<h1 class="display-1 text-center">Hello webpack !</h1>';
console.log('done !');
````

## babel

- install 

````bash
yarn add @babel/core babel-loader @babel/preset-env --dev
````

- './.babelrc'

````json
{
  "presets": [
    "@babel/preset-env"
  ]
}

````

- './webpack.config.js'

````javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
````

## react

- install

````bash
yarn add react react-dom

yarn add @babel/preset-react --dev

````

- './.babelrc'

````json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
````

## webpack dev server

- install

````bash
npm install webpack-dev-server --save-dev
````

- ' package.json '

````json
{
  "scripts": {
    "start": "webpack-dev-server --mode development --open"
  }
}
````

- run the server

````bash
npm start
````

- run dev server in dist 

````javascript
var path = require('path');

module.exports = {
    //...
    devServer: {
        contentBase: path.join(__dirname, 'dist'),
        compress: true,
        port: 9000
    }
};
````

- dev server hot reloading module

````bash
yarn add webpack-hot-middleware --dev
````

- './webpack.config.js'

````javascript
const webpack = require('webpack');

module.exports = {

    devtool: 'inline-source-map',
    devServer: {
        contentBase: './dist',
        hot: true
    },
    plugins: [
        new webpack.HotModuleReplacementPlugin()
    ]
};
````
