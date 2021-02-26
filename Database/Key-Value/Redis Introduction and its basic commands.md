# Redis
Remote Dictionary Server 는 메모리 기반의 key-value 구조 데이터 관리 시스템이다. 모든 데이터가 memory에 저장되기에 빠른 읽기 쓰기 속도를 보장한다.
메모리는 휘발되기 때문에 저장된 데이터를 중간중간 snapshot 으로 디스크에 기록한다. 따라서 snapshot이 언제나 가장 최신의 데이터베이스를 보장할 수 없다.
저장가능한 자료형은 String, Bitmap, Hash, List, Set, Sorted Set 등이 있다.

## Commands
SET key "value"
GET key
SET int 1
INCR int #2
GETSET int 0 #2
GET int #0
EXISTS int #1

### List
Redis의 list 타입은 head와 tail reference가 있는 linked list와 같다.
LPUSH mylist A
RPUSH mylist B

### Hash
hash는 field-value 쌍을 사용한 일반적인 해시이다. key 에 대한 field 의 갯수에는 제한이 없다.
hash key 를 PK, field 는 column, value 를 value 로 대응하면 RDB의 table 의 한 row 와 비슷하다.

### Set
교집합, 차집합, 합집합 연산에 유용하다.

SADD myset 1 2 3 4 5

### Sorted Set
오름차순으로 정렬한다. 인덱스로 조회하는데 유용하다.

ZADD sortedset 100 dongju 80 judy
ZRANGE sortedset 0 1 #judy dongju

## Sessioning
EXPIRE 커맨드는 value 값 후에 key 를 멸소시킨다. 이 특징으로 세션을 간편하게 만들 수 있다. 동일한 키가 다시 들어오면 timeout 이 재설정된다. 따라서 계속 이용하는 데이터는 남아있고, 쓰지 않는 데이터는 말소된다.

https://try.redis.io/
컴퓨터에 설치하지 않고도 쉽게 커맨드들을 테스트할 수 있다.
