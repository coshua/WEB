기본적으로 http 에서 클라이언트는 url 에 요청하고자 하는 데이터를 보낸다.

http://hostname:port/?id=100

위와 같은 url을 해석한다면 http 라는 프로토콜(약속) 하에, hostname 이라는 컴퓨터(서버)의 몇번 port 로 id=100 이라는 쿼리 스트링을 보내는 것이다.

서버에서는 들어오는 쿼리를 다음과 같이 처리한다.

```javacript
var http = require('http');
var url = require('url');
 
var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    console.log(queryData) // {id: 100}
}
```

### handle POST
클라이언트에서 서버측으로 post method 를 이용해 데이터를 보낼 수 있다.
위 사항에서 다음 내용을 추가한다.
```javascript
var qs = require('querystring');

var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    var pathname = url.parse(_url, true).pathname;
    if(pathname === 'submit') {
      var body = '';
      request.on('data', (data) => {
        body += data;
      } //.on 은 일종의 event listener 이다. 여러번의 데이터를 나누어 받는다.
      request.on('end', () => {
        var post = qs.parse(body); //body 를 객체화해서 post에 담는다.
        var title = post.title;
        var content = post.content;
      } // 전송이 끝나면 발생하는 이벤트에 대한 리스너이다.
      response.writeHead(200);
      response.end('success');
    }
}
```
