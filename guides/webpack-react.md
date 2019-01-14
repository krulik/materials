# Creating a Webpack-React Project template

Based on the tutorial
[Creating a React App… From Scratch.](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658)

## SASS

```bash
npm install sass-loader node-sass --save-dev
```

## PostCSS

```bash
npm install postcss-preset-env post-css-loader --save-dev
```

`./.browserslist`

```
> 5% in IL
```

## React

```bash
npm install react react-dom react-hot-loader
```

`./src/components/App/App.jsx`

```jsx
import React from 'react';
import {hot} from 'react-hot-loader';

class App extends React.Component {
  render(){
    return(
      <div className="App">
        <h1> Hello, World! </h1>
      </div>
    );
  }
}

export default hot(module)(App);
```

`./src/components/App/_App.scss`

```scss
.App {
  padding: space(1/2);
  font-family: sans-serif;
  background-color: cornsilk;
}
```

`./src/index.scss`

```scss
:root {
  --space: 1em;
}

@function space($portion) {
  @return calc(var(--space) * $portion);
}

@import './components/App/App';
```

`./src/index.js`

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import './index.scss';

import App from './components/App/App.jsx';

ReactDOM.render(<App />, document.querySelector('main'));
```

`./public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>React Template App</title>
</head>
<body>

  <main></main>

  <script src="bundle.js"></script>
</body>
</html>
```

## Babel

```bash
npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/preset-react
```

`./.babelrc`
```json
{
  "presets": ["@babel/env", "@babel/preset-react"]
}
```

## Webpack

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader
```

`./webpack.config.js`

```js
let path = require('path');
let webpack = require('webpack');
let postcssPresetEnv = require('postcss-preset-env');


module.exports = {
  entry: './src/index.js',
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules)/,
        loader: 'babel-loader',
        options: { presets: ['@babel/env'] }
      },
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', {
          loader: 'postcss-loader',
          options: {
            ident: 'postcss',
            plugins: () => [
              postcssPresetEnv(/* pluginOptions */)
            ]
          }
        }, 'sass-loader']
      }
    ]
  },
  resolve: { extensions: ['*', '.js', '.jsx'] },
  output: {
    path: path.resolve(__dirname, 'public/'),
    publicPath: '/',
    filename: 'bundle.js'
  },
  devtool: 'inline-source-map',
  devServer: {
    contentBase: path.join(__dirname, 'public/'),
    port: 3002,
    publicPath: 'http://localhost:3002/',
    hotOnly: true,
    disableHostCheck: true
  },
  plugins: [new webpack.HotModuleReplacementPlugin()]
};
```

`./package.json`

```json
{
  "name": "react-jsx-class",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "webpack-dev-server --mode development",
    "build": "webpack --mode production",
    "lint": "eslint src/**/*.js src/**/*.jsx"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@babel/cli": "^7.2.3",
    "@babel/core": "^7.2.2",
    "@babel/preset-env": "^7.2.3",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.5",
    "babel-eslint": "^10.0.1",
    "eslint": "^5.12.0",
    "eslint-plugin-react": "^7.12.3",
    "css-loader": "^2.1.0",
    "node-sass": "^4.11.0",
    "sass-loader": "^7.1.0",
    "style-loader": "^0.23.1",
    "webpack": "^4.28.4",
    "webpack-cli": "^3.2.1",
    "webpack-dev-server": "^3.1.14"
  },
  "dependencies": {
    "react": "^16.7.0",
    "react-dom": "^16.7.0",
    "react-hot-loader": "^4.6.3"
  }
}
```

## ESLint

```bash
npm install eslint babel-eslint --save-dev
```

```bash
./node_modules/.bin/eslint --init
```

`./.eslintrc.json`

```json
{
    "env": {
        "browser": true,
        "commonjs": true,
        "es6": true,
        "node": true
    },
    "extends": ["eslint:recommended", "plugin:react/recommended"],
    "parser": "babel-eslint",
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": 2018,
        "sourceType": "module"
    },
    "plugins": [
        "react"
    ],
    "rules": {
        "indent": [
            "error",
            2
        ],
        "linebreak-style": [
            "error",
            "unix"
        ],
        "quotes": [
            "error",
            "single"
        ],
        "semi": [
            "error",
            "always"
        ],
        "no-console": "warn"
    }
}
```