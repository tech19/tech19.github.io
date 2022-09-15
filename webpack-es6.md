# webpack-es6

Webpack:

* static module bundler
* compact and mimizie(uglify) css, js
* copy & move
* import css,js inside JS

> entry\
> one entry point per HTML page. \
> SPA: one entry point, \
> MPA: multiple entry points.

After entering the entry point, webpack will figure out which other modules and libraries that entry point depends on

## Phpstorm Webpack

[https://www.jetbrains.com/help/phpstorm/2017.3/webpack.html?utm\_medium=help\_link\&utm\_source=from\_product\&utm\_campaign=PS\&utm\_content=2017.3](https://www.jetbrains.com/help/phpstorm/2017.3/webpack.html?utm\_medium=help\_link\&utm\_source=from\_product\&utm\_campaign=PS\&utm\_content=2017.3)

* es5를 쓸려면 webpack으로 module하고 shim을 쓸려면 쓰고. (shim은 html5, jquery, es5,6,7,...)
* pollyfill로 대신?
* 크롬과 파이어폭스에서는 쉽게 ES6 을 사용할 수 있지만 다른 브라우저는 babel, traceur, es6-shim등을 이용
*   es6 = es2015

    그래서 es5는 대부분 최신 브라우저에서 됨. 그러나 shim을 add 하면 good.
*   es5 vs es6(es2015)

    \[[https://www.zerocho.com/category/EcmaScript/post/5757feea4bd934472a2ee52c](https://www.zerocho.com/category/EcmaScript/post/5757feea4bd934472a2ee52c)

    [https://www.zerocho.com/\](https://www.zerocho.com/category/EcmaScript/post/5757feea4bd934472a2ee52c](https://www.zerocho.com/]\(https://www.zerocho.com/category/EcmaScript/post/5757feea4bd934472a2ee52c)

    [https://www.zerocho.com/](https://www.zerocho.com/))

[https://firejune.com/1798/%EC%B4%88%EB%B3%B4%EC%9E%90%EC%9A%A9+Webpack+%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC+%ED%8C%8C%ED%8A%B81+-+Webpack+%EC%9E%85%EB%AC%B8](https://firejune.com/1798/%EC%B4%88%EB%B3%B4%EC%9E%90%EC%9A%A9+Webpack+%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC+%ED%8C%8C%ED%8A%B81+-+Webpack+%EC%9E%85%EB%AC%B8)

[https://medium.com/@soeunlee/webpack%EC%9D%84-%EC%84%9C%EB%B9%84%EC%8A%A4%EC%97%90-%EC%A0%81%EC%9A%A9%ED%95%B4-%EB%B3%B4%EA%B8%B0-a5ccfec070f3](https://medium.com/@soeunlee/webpack%EC%9D%84-%EC%84%9C%EB%B9%84%EC%8A%A4%EC%97%90-%EC%A0%81%EC%9A%A9%ED%95%B4-%EB%B3%B4%EA%B8%B0-a5ccfec070f3)

## phpstorm 에서 npm

\[hrm]

* node.js: install c:\Program Files\nodejs\node.exe seting: enable
* npm: terminal: npm init -> create package.json ? "main": "index.js" -> default
*   package.json -> (npm) \
    devDependencies \
    "babel-loader"\
    "babel-preset-es2015" -> es6를 es5로 \
    "babel-polyfill" \
    "webpack", \
    "webpack-dev-server",\
    "copy-webpack-plugin"\
    "babel-core", "css-loader", "react", "react-dom", "react-hot-loader", "style-loader", "bable-preset-react",\
    "react-table"&#x20;

    scripts \
    &#x20; "build": "webpack", \
    &#x20; "watch": "webpack --watch",\
    \-> Webpack에서 파일의 상태가 변경되면 자동으로 빌드 \
    &#x20; "start": "webpack-dev-server --hot --inline" \
    &#x20; babel: { \
    &#x20;   "presents": \[ "es2015", "react" ] \
    &#x20; },
* webpack.config.js (to use other name file use --config) \
  var dir\_js = ... \
  var dir\_build = \
  module.exports = { \
  &#x20; entry: ..., \
  &#x20; output: { \
  &#x20;   path: \_\_dirname + '/js/', \
  &#x20;   filename: 'bundle.js' \
  &#x20; }, \
  &#x20; module: { \
  &#x20;   loaders: \[ \
  &#x20;       { \
  &#x20;         loader: 'babel-loader', \
  &#x20;         test: dir\_js, -> what transfile, .css, .jsx \
  &#x20;         test: /.jsx?$/, \
  &#x20;         exclude: /(node\_modules)/, \
  &#x20;       } \
  &#x20;   ] \
  }, \
  pulgins: \[ \
  &#x20; .... \
  ], \
  devtool: 'source-map', \
  devServer: { \
  &#x20;   ... \
  }, \
  };

## Es6 문법

[http://alexband.tistory.com/37](http://alexband.tistory.com/37) [http://beomy.tistory.com/category/JavaScript?page=1](http://beomy.tistory.com/category/JavaScript?page=1) [http://yubylab.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%BD%9C%EB%B0%B1%ED%95%A8%EC%88%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0](http://yubylab.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%BD%9C%EB%B0%B1%ED%95%A8%EC%88%98-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
