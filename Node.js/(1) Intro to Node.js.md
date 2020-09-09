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
