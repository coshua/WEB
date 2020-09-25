### SQL
SQL 은 Structured Query Language 의 약자로 데이터베이스를 정리된 표로 나타내는 약속이다. MySQL은 opensource 로 가장 인기있는 데이터베이스 중 하나이다. 
표(table)는 행(row)과 열(column)로 이루어져 있다.  

직접 MySQL을 다루어보며 자세하게 알아보자.

MySQL 은 기본적으로 Database Server > Database > table 의 구조를 띈다.

권한을 가진 이용자로 서버에 접속하면 기본적으로 Database Server 에 접근한 상태이다. 여기서 사용할 Database 를 만들어준다.

`CREATE DATABASE tutorials;` 

해당 Database 를 이용하기 위한 명령어이다.

`USE toturials;`

테이블을 만들자.

```
CREATE TABLE table1(
  id INT(11) NOT NULL AUTO_INCREMENT, //id 라는 column은 int type이며 11자리까지 디스플레이한다. 비어있을 수 없으며 서버에서 자동으로 넘버링한다.
  title VARCHAR(100) NOT NULL, //100글자로 제한하는 string type이다.
  description TEXT NULL); //공백을 허용하는 긴 string type column이다.
```

### CRUD

#### Insert
`INSERT INTO topic (title,description,created,author,profile) VALUES('My','SQL',NOW(),"dongju","kim");`

#### Select
`SELECT * FROM topic;` //select all columns
`SELECT id,title FROM topic;` //select specific columns
`SELECT id,title FROM topic WHERE author='dongju' ORDER BY id DESC;`
`SELECT id,title FROM topic WHERE author='dongju' ORDER BY id DESC LIMIT 2;` //show only two results from top

#### Update
`UPDATE topic SET description='changed',title='new title' WHERE id=2;`

#### Delete
`DELETE FROM topic WHERE id=1;` // to remove table contents

`DROP TABLE topic` //to remove table container
