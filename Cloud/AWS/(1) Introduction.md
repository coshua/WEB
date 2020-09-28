AWS 는 가상 서버를 제공한다.

물리적인 서버 저장소가 필요하다. 전세계에 약 8개 정도가 있다. 이를 region 이라 하는데 각각의 region 은 여러 개의 availabiltiy zone 으로 구성되어 있다. 
어느 곳의 시스템이 무너져도 다른 az 가 region 을 지탱한다. 

Edge location 은 AWS 의 CDN 을 위한 캐시 서버이다. CDN 은 미디어와 같은 컨텐츠를 캐시 서버에 복제해놓고 필요한 사용자에게 빠르게 전달하는 서비스이다. CDN 이 사용자와 만나는 지점이 edge 이다.
