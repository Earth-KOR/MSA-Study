MSA   sad
- 스프링 클라우드
- 컨테이너 오케스트라

MSA
-> 회사 리소스를 많이 투자하긴 해야함
-> 기존에 잘 돌아가는걸 하나씩 뽑아서 분리해야하기때문
-> 분리하기 떄문에 네트워크 비용이 발생
-> 분리하기 떄문에 배포와 모니터링에 많은 리소스가 듦

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

결론:
지금 모놀리틱에도 서비스를 충족한다면 굳이 바꿀 필요가 없다
즉, 현재 구조가 모놀리틱이 버티지 못하는 순간이 올 때 MSA가 필요함 

예시 )
코드 베이스가 너무 커서 신규 개발자가 파악하기 어려움
A도메인이 수정됐는데 C도메인에 영향을 주는 경우가 발생할때

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

모놀리틱의 불편함.
-> 한 피쳐가 개발이 끝났는데 배포일정을 맞추기 위해서 늦게
배포되는 문제가 있음.
-> 배포직후 예상하지 못한 부분에서 버그가 발생함

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

비즈니스 도메인 단위로 시스템을 작게 분리하기 위한 전략은 많음
-> 스트랭글러 패턴, 점진적인 배포 등등..

스트랭글러 패턴
 -> 기존 시스템과 신규 시스템에 유입되는 트래픽을 조절하면서 점진적으로 신규 시스템 쪽으로 트래픽을 늘려가는 과정
-> 트래픽을 조절할 장치가 필요 앞단의 proxy가 될수가있고 서비스 내부의 라우팅 조직이 될수도있다.

DB분리 기존과 신규 데이터
-> 기존, 신규 dual write 하는 방법
-> 하나의 데이터베이스를 바라보게 하는방법

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

MSA를 쪼갤때 기준
-> 비즈니스 도메인을 중심으로 모델링된 각각의 서비스
-> 레이어드 아키텍쳐에서 도메인을 중심으로 다른 레이어가
의존관계가 있듯이 비즈니스와 도메인사이에도 의존관계가 있음

즉, 도메인간의 의존관계를 먼저 파악하고 쪼개는게 좋다고 생각!
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

어떤 도메인으로 쪼개는게 좋을까??

너무 세세하게 쪼개지말고 덩어리로 쪼개고 점진적으로 나아가는
것도 좋은방법이라고 생각함.

-> 프론트쪽은 여러 API를 적절히 어그리게이션한 프론트 도메인 도 있으면 좋음!

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

비즈니스 도메인 중에서 가장 임팩트가 큰 것부터 전환
-> 큰 도메인을 분리해야 MSA의 효과를 볼 수 있다
-> 임팩트가 작고 분리 안해도 되는 도메인을 굳이 전환?
이거는 모놀리틱으로 모아놔도 괜찮다고 생각함

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

여러가지 도메인이 복잡하게 섞인 기능 및 시급성을 따졌을 때 굳이 MSA로 분리하지않고 모놀리틱으로 유지하고 운영하는거도 좋은 방법이라고 생각함.
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

API 체계 정하기

하나의 서버로 하는게 아니라 여러 서버로 API를 쏘기 때문에
중구난방으로 response를 받을수가 있다. 또는 메세지 브로커
를 통해서 비동기로도 돌아갈수도 있음.
즉, API 응답을 통일하는게 좋다고 생각함!

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

처음부터 데이터베이스를 분리하지 않아도 된다.
-> shared database
-> 온전한 msa전환에서는 각 서비스마다 각자의 데이터베이스를 가지는 것이 맞다
-> 하지만 점진적인 방식의 전환을 진행할떄의 장점을 생각하면 코드를 먼저 분리 후 데이터베이스를 분리하는 방식이 좋다고 생각
-> 코드를 분리하게 되면 해당 코드가 사용하는 데이터가 무엇인지 확인할 수 있기 때문에
-> 이를 기반으로 추후 데이터베이스 분리 작업도 수월하게 진행가능

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

데이터베이스 분리과정

1. 새로운 DB를 만들어서 원래 DB 데이터를 일괄복제를함
2. batch 서비스를 만들어서 원래 DB 데이터를 읽고 바뀐 데이터를 그대로 복제한 DB데이터에 적용하는 로직을 만듦
3. 두가지 데이터베이스의 정합성이 일치하는 순간이 온다
4. 두 데이터에 dual write를 한다 + batch를 내린다
5. read부하를 새로운 DB로 돌린다
6. dual write를 내리고 트랙픽을 새로운 DB로 돌린다.

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

MSA에서 필요한것

1. 고도화된 배포
2. 모니터링
3. 로깅
4. 보안
5. 네트워크
6. 개발 환경

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

서버간 통신 매커니즘 정의

네크워크로 연결된 서비스 간의 통신을 기반으로 운영되는 분산 아키텍쳐

- 동기식 (클라에서 서버세에 요청을 보내고 응답을 기다림) HTTP, gRPC
- 비동기식 (이벤트 브로커를 통해 메세지를 비동기적으로 전달)메세지 브로커


<gRPC식>

바이너리 기반의 메세지 포맥 -> HTTP에 비해 빠름, 프로토콜 버퍼를 통한 통신 과정에서의 데이터 타입을 명확하게 정의 할 수 있음 하지만 외부 클라이언트에서의 gRPC 사용은 충분히 지원되지 않고 있고 학습비용이 있음


시스템 내부에서는 gRPC를 사용하는걸 권장
 - 동기식
 - 바이너리 방식
 - 스키마에 제약
 - 웹, 앱 기반에는 사용하기 애매함


<비동기 메세징 처리>
어떠한 비즈니즈 로직이 바로 적용될 필요가 없는 경우에 비동기로 처리가능 !

-> SQS, Kakfa 등등…


ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

프론트에 표현할때 request 어떻게?? 비동기 동기?? 여러서버 돌려서?? 머징??

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

기존에는 프론트에서 api하나만 호출하면 모든게 가능했는데
msa로 넘어가면 여러 도메인에 대해서 api를 쏴야한다.

<CQRS 모델 도입>

모든 도메인은 kafka를 가운데에 두고 퍼플리싱 하고 있고
front에서 컨슘을 진행한다.

Front에서 별도의 db를 둔다 -> 몽고DB 

몽고 DB는 컨슈밍 한걸 따라서 DB데이터를 업데이트 한다.

즉, 조회를 할 때 여러 api를 쏘는게 아니라 한번의 api를 쏴서 화면을 그리기 가능함 (redis 를 둬도 좋음)

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

카프카의 특징

멀티 컨슈밍 -> 컨슈머 그룹 여러개 -> 자신의 기준에 맞는 오프셋만큼 가져감

카프카 이슈 

1. 리밸런싱

클러스터내 토픽을 가지고 N개의 파티션을 만들수있음
이벤트가 쌓일때 여러 파티션에 랜덤으로 쌓임
특정 토픽을 읽음  -> 컨슈머 그룹 선언
컨슈머 그룹 내에서 파티션 소유권을 가지고있는 인스턴스를 가짐
인스턴스가 죽으면 소유권을 해지시킴 -> 다른쪽으로 양도함

이슈 : 특정 순간에 리밸런싱이 일어나면 특정 시간동안 처리가 0으로 떨어지고 정상화 되면 다시 작동함

Msa -> 파트별로 배포하면 죽었다가 살아나기 때문에 계속해서 리밸런싱이 일어남

Kafka 2.3 버젼 이상으로는 이 이슈가 해결댐
-> 하나가 죽었을떄 소유권을 다 회수하고 살아난걸 판별하고 분배하는게 아니라 이미 가지고 있는 소유권은 냅두고 죽은애꺼만 가지고 뿌리는걸로 함

1. 순서보장

이슈 : 이벤트는 토픽에서 순서를 보장하는게 아니라 파티션 내에서만 순서보장이 된다.
즉, 파티션에 흩어져서 이벤트를 등록한것이라면 메세지의 순서가 보장이 되지 않는다.

Send (message)
Send (key, message)

key값을 같이 보내주면 key값을 인식하여 파티셔너가 이걸 인식한다. 그리고 해싱을 돌려서 순서를 보장하도록 한 파티션으로 넣어준다


1. 중복메세지 수신

이슈 :
카프카와 서버 사이에 통신 이슈가 생길수있음.
-> 서버에서 잘 읽었는지 카프카가 모름
-> Kafka에서 offset 기록을 안함
-> 서버가 정상화 됨 -> Kafka 재호출 
-> kafka는  reture을 못받아서 다시한번 데이터를 넘겨줌

해결:
주문 ID -> 결제완료
주문 ID -> 결제완료 중복 수신

i) Exception 을 던짐
ii) status 200 던짐
iii) 컨슈머 로직에서 @TranX로 묶음
메세지를 읽으면 id : 123 insert 함 (프로세스 메세지 DB)
결제처리

동일한 결제완료가 들어왔다!
프로세스 메세지를 insert 한다 -> Exception 발생 -> 롤백된다


ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

Graceful shutdown 설정

특정 api 호출후에 서버가 죽었을 때 강제로 종료가 된다면 중간에 프로세스가 끊기게 된다.
-> 이러한 상황을 막아야함!

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

Timeout 설정 -> 동기식 HTTP 할때 필수!

커넥션 타임아웃
리드 타임아웃

타임아웃을 잡을 때 시간을 얼마나 잡을지가 중요함!


ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

프로메테우스와 그라파나

프로메테우스 -> 타겟이 되는 서버로 부터 메트릭 수집 및 규칙 확인 -> 알람 매니저에게 알려줌

그라파나 -> fromQL을 통해서 프로메테우스에 쿼리를 날리고 받은 결과값을 토대로 시각화 한다

알람 매니저 -> 매트릭 정보를 받아서 메일이나 슬랙으로 알려줌

익스포터 -> 메트릭 수집 및 포트 오픈 (가운데 중재자 역할)

푸쉬게이트웨이 -> 익스포터 push 방식

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

보통은 프로메테우스가 pull 방식으로 서버에서 정보를 받지만. 불가피하게 push 방식으로 받아야 할 떄에는 server에서 pushgateway로 push를 하고 프로메테우스가 푸쉬게이트웨이를 pull 해서 작동할수도 있다.

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

프로메테우스의 특징

메트릭 이름과 키 값 쌍으로 이뤄진 다차원 데이터 모델 (라벨)
다차원 데이터 모델 활용을 위한 쿼리 언어 -> PromQL
HTTP 기반의 pull 방식 메트릭 수집
 - 브라우저를 통한 확인 가능
 - 다수의 모니터링 용이
 - 모니터링 서버 변경 용이
 - 새로운 호스트 발생 시 추가 필요
 - 모니터링 서버 부하


ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

대용량 서비스

1. 서비스 트래픽이 많은 서비스는 다음과 같은 능력이필요
    1. 탄력성
    2. 장애회복성
    3. 자동화
    4. 모니터링

SPOF -> 하나의 서버만 관리한다면 전체가 같이 실패하기 때문에 N대의 서버를 돌려야함! (서버나 DB 전부다!)

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

테스트

성능 테스트

부하 테스트

스트레스 테스트



- DB 
-> NoSql

-> redis (MemoryCache)
인메모리 DB -> 가득차면?
하드디스크는 커서 잘 없는데 메모리는 가득찰수있음
스왑을 통해서 하드디스크에다가 일부 넣고 사용이 가능
=> 괜찮은 방법이 아님 -> 메모리 캐시를 쓰는거 자체가 빠르기 떄문에 쓰는건데 하드디스크에 넣는순간 페이지네이션 때문에 성능이 엄청 죽어버림
=> 오래된것들을 지워버린다 or 돈을 쓰는거다

-> RDBMS (PostgreSql?)
오라클 mysql 보다 기능이 다양
PostgreQL이 오라클을 카피한 것
성능적으로 PostgreQL이 좋기도함

-> INDEX
인덱스는 효율적인 검색을 하기위한 자료구조입니다.
대표적으로 사전의 색인을 예시를 많이드는데.
만약 “바”라는 단어를 찾는다면 앞의 가~나~는 다 스킵하고 찾을 수 있기 때문에 검색 효율이 증가합니다.

단점으로는 CUD를 수행할 때 인덱스에 관한 추가적인 작업이 필요하기 때문에 변경이 잦으면 오히려 성능 저하가 올 수가 있음

- 블로킹/논블로킹
함수의 제어권에 따라 달라짐

- Msa 모니터링 방식? (동기/비동기)
에러 핸들링 -> 보상 트랙잭션으로 가능
서킷 브레이크 작동 -> 모니터링 툴 -> 히스트릭스, 프로메테우스

-> 트러블 슈팅 ? -> ELK ???

- 보상 트랙잭션 (비동기)
이벤트로 발행 -> a b c d -> 에서 -> d에서 실패하면 -> 실패 이벤트를 발행하면 -> 실패 이벤트 -> 앞에서 했던 애들이 감지를해서 -> 작동했던것들을 전부 롤백 시키는 보상 트랜잭션을 작동

- DDD
도메인만 봐도 얘가 어떻게 동작하는지를 파악가능하게 설계
로직을 도메인에 넣어서 설계
유지보수 , 인지부하가 줄어드는게 장점
객체지향적 설계
도메인을 분리해서 제작하기때문에 뜯어내기 좋다

- RESTful API



- 대규모 서비스 대응
-> 수평적으로 서버 증설 가능?
-> 반복적으로 호출되는걸 캐시로 처리하기


- MSA 분리기준?

A b 같은 서비스단 같은 로직에서 움직일 수 있으면 같이 묶어서
도메인 로직에 따라서 분리하는게 좋음
도메인 간의 의존성을 봐야함
이걸 위해서 DDD나 클린아키텍쳐가 필요


- 필터, 인터셉터
필터는 서블릿 기반
인터셉턴 스프링 기반


- 리퀘스트의 흐름 
필터 -> 디스패처 서블릿 -> 리퀘스트 맵핑 (핸들러 맵핑 이라는 DB에다가 키벨류로 저장) -> 인터셉트 -> 핸들러 -> 비즈니스 로직 

- Bean scope & lifeCycle

스프링 컨테이너 -> 빈 생성 (오토 스캔) -> 의존관계 주입 -> 초기화 -> 사용 -> 종료직전 다 죽고 -> 컨테이너 죽음

싱글톤 스코프 -> 이 객체가 무조건 하나만 생성되도록
처음 호출들어오면 생성됨 -> 서버가 꺼지기 전까지는 계속 살아있음 

쓰레드기반으로 요청을 받는다!


- JPA 성능

1. 부수적인 쿼리들이 나가는게 있음 (1차캐시랑 실제 DB데이터를 맞추기 위해)
2. 프록시를 많이 생성해서
3. n+1 문제 (패치조인, LAZY 처리)

- JPA OSIV
