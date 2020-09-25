Node 는 정말 많은 module 을 이용하여 개발자 경험을 개선한다.

node 에서 쓰는 `var a = require('something');` 이나 리액트에서 `import a from 'something';` 와 같은 어법들은 모두 모듈을 불러오는 것이다.

module 은 결국 어떤 기능을 수행하기 위해 모인 도구들의 모음이다. 하나의 큰 객체이며, OOP 개념이다.

모듈은 아래와 같이 쉽게 만들 수 있다.
```javascript
//someModule.js
var M = {
  v:'v',
  f:function(){
    console.log(this.v);
  }
}
 
module.exports = M;

//app.js
var part = require('./someModule.js');
part.f();
```

결국 모듈은 향상된 품질의 코드를 짜기 위해 코드의 재활용, 최소 단위로의 splitting 등을 활용한 수단이다.
