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
