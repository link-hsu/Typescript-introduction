## Webpack & Typescript setup
[Course Link](https://www.youtube.com/playlist?list=PL4cUxeGkcC9hOkGbwzgYFmaxB0WiduYJC "Link here")  
[Github Code](https://github.com/iamshaunjp/webpack-and-typescript)  
[reference - PJ](https://pjchender.dev/typescript/ts-basic-types/)  
[webpack 5 - full course](https://www.youtube.com/watch?v=TOb1c39m64A)
### Basics
- **Goal**
  1. How to use webpack to compile Typescript into Javascript
  2. How to bundle source code into a single javsscript file
  3. How to use webpack dev server
  4. How to use ES6 modules & source maps(debugging)
- installation
  - ```tsc --init```  
    *tsconfig.json*
    ~~~ typescript
    {
      "compilerOptions": {
        "target": "es6",
        "module": "es2015",
      }
    }
    ~~~
  - ```npm init -y```  
    ```npm install webpack webpack-cli ts-loader -D```  
    ```// ts-loader teaches webpack how to compile typescript```  
    ```npm install typescript -D // still need to install locally, even already install globally```  
  - create *./src/* & *./public/* *folders* and *./public/index.html* & *./src/index.ts* files
  - *webpack.config.js*
    ~~~ javascript
    const path = require('path');
    module.exports = {
      entry: './src/index.ts',
      module: {
        rule: [
          {
            test: /\.ts$/,
            include: [path.resolve(__dirname, 'src')],
            use: 'ts-loader',
          }
        ]
      }
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'public'), // absolute path
      },
    }
    ~~~
  - *package.json*
    ~~~ javascript
    "scripts": {
      "build": "webpack",
    },
    ~~~
    ```npm run build```
  - *Webpack Dev Server*
    - install     
    ```npm install webpack-dev-server -D```
    - *package.json*
      ~~~ javascript
      "scripts": {
        "serve": "webpack-dev-server",
      },
      ~~~  
      ```npm run serve```  
      - webpack-dev-server recompile file, but wepack don't rebuild file -> wepack.config.js setting
      - *webpack.config.js*
      ~~~ javascript
      const path = require('path');
      module.exports = {
        ...
        output: {
          publicPath: 'public', //  realtive path - tell webpack-dev-server where to server new code which has in memory from. (build is still webpack's job, not webpack-dev-server)
          filename: 'bundle.js',
          path: path.resolve(__dirname, 'public'), // absolute path
        },
      }
      ~~~
- Using ES6 Modules
  - *webpack.config.js*
    ~~~ javascript
    const path = require('path');
    module.exports = {
      ...
      resolve: {
        extensions: ['.ts', '.js'],
      },
      ...
    }
    ~~~
  - resolve 是什麼:在 webpack 中，resolve 是一個用於解析模組路徑的函式。  
  resolve 函式會從當前工作目錄開始，逐層向上搜索，直到找到指定的模組。  
  如果 resolve 函式無法找到指定的模組，則會拋出 module not found 錯誤。  
  **module: { rule: } take care content in file**  
  **resolve: { extensions: [] } take care which path(type)**
- Debug in Typescript - using **Source Map**
  - *source map* create links between source files and compiled output files
  - How to use:  
    *tsconfig.json*
    ~~~ javsscript
    {
      "compilerOptions": {
        "sourceMap": true,
      }
    }
    ~~~  
    *webpack.config.js*
    ~~~ javascript
    const path = require('path');
    module.exports = {
      devtool: 'eval-source-map',
      ...
    }    
    ~~~
- mode(*[webpack-docs](https://webpack.js.org/configuration/mode/)*) for webpack.config.js
  *webpack.config.js*
  ~~~ javascript
  const path = require('path');
  module.exports = {
    mode: 'development' // production,
    ...
  }    
  ~~~

    
