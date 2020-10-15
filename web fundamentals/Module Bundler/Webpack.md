## Background
import/export 구문이 없던 모듈 이전 상황에서 개별 JavaScript objects 들을 하나의 html 파일에서 쓰는 것은 여러모로 불편했다.
Objects 들이 공유된 namespace 를 갖게 되고, html 파일의 복잡도가 증가한다.

ES2015 에서 모듈이라는 문법이 등장했다. CommonJS 는 exports 키워드와 require() 함수를 통해 서로 다른 object 를 연결짓는다.

`exports function sum(a, b) { return a + b; } //example.js`

```
const helper = require("./example.js"); //app.js
helper.sum(1, 2) // 3
```

ES2015 가 제안한 표준 모듈 시스템은 export/import 구문으로 모듈을 전달하고 바벨과 웹펙으로 관리하는 것으로 현재까지 주류 패러다임이다.

```
export function sum(a, b) {return a + b; } //example.js

import * as example from './example.js' //app.js
example.sum(2, 3);
```

열심히 JS 를 개발해놨자 브라우저가 이를 지원하지 않으면 소용이 없다. 크롬은 아래와 같은 구문으로 module 을 지원한다.

`<script type="module" src="app.js"></script>`

모든 브라우저에서 일관되게 모듈을 쓸 수 있게 해주는 bundler 의 개념이 필요하게 되었다.

## Webpack
웹팩은 대표적인 bundler 중 하나이다. 번들러의 기본적인 작동 방식은 다음과 같다.

Entry point 를 입력받아 거기에서부터 의존하는 모듈을 모두 그러모아 하나의 파일(Output)로 합친다. 이야기해보자면 결국 import/export 가 필요 없이 output 파일에 모든 구성 요소가 들어가는 것이다.
이로 인한 장점은 브라우저에서 import/export 구문을 지원하지 않더라도 하나의 파일을 읽고 script 들을 실행함으로써 개발자가 구현되길 바라는 결과를 만들어내는 것이다.
모듈 없이 하나의 파일을 읽는다면 앞서 말한 문제점이 있지 않은가? 그렇지 않다. css module 에서 element 들의 class name 이나 id 등이 compiler 끼리 문제없이 소통 가능하지만 겹치지 않도록 자동으로 이름을 부여하는 것처럼,
하나의 파일 안에 namespace 가 겹칠 일은 없다.

기본적인 작동 방식은 webpack.config.js 에 설정을 정해두고 webpack 을 실행하면 컴파일이 되어 아웃풋 파일이 생기는 원리이다.

### Loader
웹팩은 자바스크립트밖에 모른다. 하지만 웹팩은 이미지와 스타일시트도 모듈로 관리한다. 비 자바스크립트 파일을 자바스크립트 형식으로 바꾸어 주는 것이 로더의 역할이다.

로더는 test, use 키를 갖고 있는 객체이다.
* test : 로딩할 파일을 지정한다.
* use : 해당 파일에 맞는 로더를 설정한다.

로더는 따로 설치해줘야 하며, 로더를 이용하여 만든 configuration file 은 다음과 같다.
```javascript
//webpack.config.js
const path = require("path");
module.exports = {
  entry: {
    main: "./src/main.js",
  },
  output: {
    filename: "bundle.js",
    path: path.resolve("./dist"),
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["css-loader"], //css 파일을 js 구문으로 바꾸어놓는다.
      },
    ],
  },
};
```


