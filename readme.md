# Webpack + TypeScript Setup

## Steps

1. start with an empty project `npm init`
2. install minimal dipendencies `npm i webpack webpack-cli typescript ts-loader -D`
3. Crate this file structure
   > src/index.ts
   > package.json
   > tsconfig.json
   > webpack.config.js
4. Add this content to `tsconfig.json`

```json
{
  "compilerOptions": {
    "outDir": "./dist/",
    "noImplicitAny": true,
    "module": "es6",
    "target": "es5",
    "allowJs": false,
    "sourceMap": true
  }
}
```

5. Add this content to `webpack.config.js`

```javascript
const path = require("path");

module.exports = {
  mode: "production",
  entry: path.resolve(__dirname, "./src/index.ts"),
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: "ts-loader",
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: [".tsx", ".ts", ".js"],
  },
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
};
```

6. Add an npm script to the `package.json`

```json
"scripts": {
  "build": "webpack"
},
```

7. Write some code to `/src/index.ts`

```javscript
window.addEventListener("load", () => {
  const header = document.createElement("h1");
  header.innerText = "Webpack❤️TS"

  const body = document.querySelector("body");
  body.appendChild(header);
})
```

8. Build the project with `npm run build`

## HTML templates

1. Install `npm i webpack-html-plugin html-webpack-plugin clean-webpack-plugin -D`
2. Add a new file `src/index.html`
3. Add this content to `src/index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"
    />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Webpack❤️TS</title>
  </head>
  <body></body>
</html>
```

4. In the `webpack.config.js` we will use newly instaleld plugins

   > **webpack-html-plugin** takes care of including your bundle to the html template
   > **clean-webpack-plugin** is a simple plugin which cleans up output folder on every build.

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require("clean-webpack-plugin");

module.exports = {
  ...
  output: {
    filename: 'bundle.[fullhash].js', // <- fullhash to ensure unique bundle name
    path: path.resolve(__dirname, 'dist'),
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "./src/index.html")
    })
  ]
};
```

5. Let's build again
