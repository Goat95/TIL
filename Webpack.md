# Bundler
## Webpack
### 1. 프로젝트 생성
```bash
npm init -y
npm i -D webpack webpack-cli webpack-dev-server@next
```
- package.json 파일
```json
{
  "name": "webpack-example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    // --mode를 통해 개발 모드인지 제품 모드인지 구별
    "dev": "webpack-dev-server --mode development",
    "build": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^5.72.0",
    "webpack-cli": "^4.9.2",
    "webpack-dev-server": "^4.0.0-rc.1"
  }
}
```
- webpack.config.js 파일 만들기.
### 2. entry, output
- webpack.config.js
```js
// import
const path = require('path');

// export 
module.exports = {
  // 파일을 읽어들이기 시작하는 진입점 설정
  entry: './js/main.js',

  // 결과물(번들)을 반환하는 설정
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.js',
    // 기존에 만들었던 파일 제거하고 다시 파일 만들기.
    clean: true
  }
}
```
### 3. plugins
```bash
npm i -D html-webpack-plugin
```
- webpack.config.js
```js
// import
const HTMLPlugin = require('html-webpack-plugin');

// export 
module.exports = {
  // 번들링 후 결과물의 처리 방식 등 다양한 플러그인들을 설정
  plugins: [
    new HTMLPlugin({
      template: './index.html'
    })
  ],

  devServer: {
    host: 'localhost'
  }
}
```
### 4. 정적 파일 연결
```bash
npm i -D copy-webpack-plugin
```
- webpack.config.js
```js
// import
const CopyPlugin = require('copy-webpack-plugin');

// export 
module.exports = {
  // 번들링 후 결과물의 처리 방식 등 다양한 플러그인들을 설정
  plugins: [
    new CopyPlugin({
      patterns: [
        { from: 'static' }
      ]
    })
  ],
```
### 5. module
```bash
npm i -D css-loader style-loader
```
- webpack-config.js
```js
// export 
module.exports = {
  module: {
    rules: [
      {
        // .css 로 끝나는 파일을 찾아라.
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      }
    ]
  },
}
```
- main.js
```js
import '../css/main.css';
```
### 6. SCSS
```bash
npm i -D sass-loader sass
```
- webpack.config.js
```js
// export 
module.exports = {
  module: {
    rules: [
      {
        // .scss 로 끝나는 파일을 찾아라.
        test: /\.s?css$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      }
    ]
  },
}
```
### 7. Autoprefixer(PostCSS)
```bash
npm i -D postcss autoprefixer postcss-loader
```
- webpack.config.js
```js
// export 
module.exports = {
  module: {
    rules: [
      {
        test: /\.s?css$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader',
          'sass-loader'
        ]
      }
    ]
  },
}
```
- package.json
```json
 "browserslist": [
    "> 1%",
    "last 2 versions"
  ]
```
- .postcssrc.js
```js
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```
### 8. babel
```bash
 npm i -D @babel/core @babel/preset-env @babel/plugin-transform-runtime
 npm i -D babel-loader
```
- .babelrc.js
```js
module.exports = {
  presets: ['@babel/preset-env'],
  plugins: [
    ['@babel/plugin-transform-runtime']
  ] 
}
```
- webpack.config.js
```js
// export 
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          'babel-loader'
        ]
      }
    ]
  },
}
```