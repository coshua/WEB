### IP 와 Host
각각의 컴퓨터는 고유한 ip를 가지고 있고 인터넷에 연결된 컴퓨터를 host라 지칭한다.

ip로 컴퓨터들을 찾아다니는 것을 힘들다. 컴퓨터는 hosts 파일을 이용해 ip에 이름을 부여해서 접속 가능하다.

hosts 파일을 변조해서 특정 주소로 원하는 사이트를 못 찾을 수도 있다. https protocol은 사이트가 변조되었는지 아닌지 확인해준다.

### DNS
Domain Name System Server 는 도메인 이름과 ip를 기억한다. 
우리가 인터넷에 연결되어 있는 컴퓨터를 쓴다면 자동으로 DNS 서버에 액세스하여 원하는 host로 접근이 가능하다 (로컬 hosts 파일에 해당 도메인 이름이 없는 경우에).

DNS에 접근하려면 DNS server에 대한 ip와 같은 정보가 필요하다. 여러 도메인 서버가 있으며 컴퓨터마다 개별적으로 사용하고자 하는 DNS 서버를 설정할 수 있다.

무료로 이용가능한 public DNS 서버가 다양하게 제공되고 있다.

### Record
DNS 서버에서 특정 도메인에 대한 기록이 record 이다. Record type 은 nameserver, address 등이 있다.

record 는 다음과 같은 구조이다. 

name - type - target

a record 는 최종적인 ip 주소를 가져온다. example.com 이란 domain name 목적 ip 에 다다른다면 이는 a 타입 record 이다.

CNAME record 는 ip 주소를 기억하지 않고 또 다른 domain name 을 기억한다. 그래서 연쇄적으로 연결되어 최종적으로 목적지에 도달할 수 있게 한다.

결국 주소는 ip로 찾아가지만 그 과정에서 사용자의 편의를 돕는 것이 cname 이라 할 수 있다.
