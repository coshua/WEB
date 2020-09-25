### socket.io 란?

socket.IO 는 실시간 웹 어플리케이션을 위한 jS 라이브러리이다.

```javascript
const app = require(‘express’)();
const http = require(‘http’).createServer(app);
const io = require(‘socket.io’)(http);
app.get(‘/’, (req, res) => {
  res.sendFile(__dirname + ‘/index.html’);
});

io.on("connection", (socket) => {
  console.log("Client is connected " + socket.id);

  //Broadcast
  socket.on("userMessage", (data) => {
    io.emit("userMessage", data);
  });
  socket.on("userTyping", (data) => {
    io.emit("userTyping", data);
  });

  socket.on("disconnect", () => {
    io.emit("userDisconnect", socket.id);
  });
});
```javascript
server 측 구현은 이렇다. 
클라이언트에서 `const socket = io();` 로 소켓과 연결한다. 이때 서버에서 `io.on('connection') 이벤트가 발생한다.
이후에 서버와 클라이언트는 이벤트를 주고 받으며 매개변수로 데이터를 관리한다.

`emit(eventName)` 으로 발생하는 이벤트를 `on(eventName)` 으로 듣는다.
```javascript
document.getElementById('sendButton').addEventListener("click", (e) => {
  e.preventDefault();
  socket.emit("userMessage", {
    message: message.value
  });

  message.value = "";
});
```
이런 식으로 클라이언트에서 이벤트를 발생시킬수 있다. 

'userMessage' 와 같은 임의의 이벤트 말고도 socket 에서 'connection'과 같이 기본으로 내장하고 있는 이벤트가 몇 가지 있다.
클라이언트가 접속을 끊으면 `on('disconnect`)` 이벤트가 발생한다.

### Namespace & Room
Namespace 개념으로 socket 들을 분류하고 구분이 가능하다. 특정 namespace 에 있는 socket 들끼리 분류가 되는 것이다.
더 나아가 Room 은 같은 Namespace 의 같은 Room 에 있는 socket 에게 통신이 가능하게 한다.
*Namespace -> Room -> Socket* 으로 전체 모양이 구성된다.

`const socket = io();` 로 연결 되는 것은 루트 디렉토리의 Namespace 이다.
다른 Namespace 로 입장하려면 `const socket = io('/namespace')` 와 같이 선언하면 된다.

서버에서 Namespace 설정은 다음과 같이 한다.
```javascript
const namespace = io.of('/namespace');
namespace.on('connection', socket => {
 namespace.emit('hi', 'everyone');
});
```

Room 은 namespace 내부에서 나눠지는 또 하나의 집합이다.

`socket.join()` 으로 접속하고 `socket.leave()`로 나간다.
```javascript
io.on('connection', socket => {
  socket.join('first room');
});
```
특정 room 에게 `io.to()`를 통해 이벤트를 보낸다 (`io.in()` 도 같은 기능을 수행한다).
```io.to('first room').emit('event');```
**Room 은 서버에서만 join 과 leave 가 가능하다**

Reference to grab the background information to understand why it emerges: https://github.com/coshua/WEB/blob/master/Protocol/From%20HTTP%20to%20WEBSOCKET.md
