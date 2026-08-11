좋아. 이제 조건이 꽤 명확해졌어.

2026년 8월 11일(화) → 2027년 2월 3일(수) 전역을 기준으로 하고,

9/28 ~ 10/2 휴가
11/6 ~ 11/8 휴가
2027/1/10 ~ 전역일까지 휴가
평소 하루 2~3시간
싸지방이라 직접적인 장시간 개발은 불가능
현재 서버 개발 경험은 사실상 없음

을 전부 반영해서 짜보자.

이번에는 단순히 "1개월차 뭐 공부"가 아니라 실제 날짜별로 무엇을 할지 정리하겠다.

전체 전략

네가 전역하는 2월 3일에 도달했을 때 목표는 이거야.

C++ / Linux / OS / Network에 대한 기초를 다시 살리고, 게임 서버의 구성요소와 동작 원리를 이해해서 전역 후 바로 서버 프로그래밍 실습에 들어갈 수 있는 상태.

따라서 6개월을 이렇게 배분하자.

8월       C++ 재활
9월       C++ + Linux
10월      Linux + Network
11월      Network
12월      OS + Concurrency
1월       Game Server
2월       Game Server 복습

그런데 휴가가 많기 때문에 실제로는 8~12월을 핵심 공부기간, 1월을 복습/정리 기간으로 보는 게 좋다.

먼저 전체 일정표
기간	주제	핵심 목표
8/11~8/31	C++ 복구 ①	C++ 기본기
9/1~9/27	C++ 복구 ②	Modern C++ + STL
9/28~10/2	🏖 휴가	공부 최소화
10/3~10/19	Linux ①	Linux 기본
10/20~11/5	Linux ②	Process / FD / GDB / Git
11/6~11/8	🏖 휴가	휴식
11/9~11/30	Network ①	TCP/IP
12/1~12/20	Network ②	Socket / Server
12/21~12/31	OS/Concurrency ①	Process / Thread
1/1~1/9	OS/Concurrency ②	Mutex / Race / Deadlock
1/10~2/3	🏖 휴가	복습/정리/전역 준비

이렇게 보면 실제로 집중해서 공부하는 기간은 약 4개월 반 정도다.

그리고 이 정도면 충분하다.

0. 공부 규칙부터 정하자

너는 지금까지 "1회독"을 많이 했기 때문에 이번에는 방법을 바꿔야 한다.

매일:

① 메인 공부 60~80분

그날의 주제.

② 알고리즘 30~40분
③ 복습 30~40분

이렇게 한다.

최대 3시간이면:

메인 공부       80분
알고리즘        40분
복습/정리       40분
----------------
총             160분

약 2시간 40분.

2시간밖에 못 하는 날은:

메인 공부       60분
알고리즘        30분
복습            30분

으로 줄인다.

공부시간이 부족하면 알고리즘부터 줄이고 메인 공부는 유지한다.

1단계 — 8월 11일 ~ 8월 31일
C++ 기억 복구

약 3주.

여기서는 열혈 C++을 처음부터 다시 1회독하지 않는다.

이미 한 번 봤기 때문에 "내가 이걸 설명할 수 있는가?"를 확인하는 방식으로 간다.

8/11 ~ 8/16
C++ 기본

공부:

포인터
참조
const
배열
struct
class
함수
함수 오버로딩
namespace

목표:

포인터와 참조를 설명할 수 있다.

stack과 heap을 설명할 수 있다.

8/17 ~ 8/23
객체지향
생성자
소멸자
상속
다형성
virtual
virtual destructor
abstract class

특히 이 질문에 답할 수 있도록.

왜 서버 코드에서 virtual이 필요한가?

8/24 ~ 8/31
메모리 + Modern C++
RAII
unique_ptr
shared_ptr
weak_ptr
move semantics
rvalue reference
lambda
auto

여기까지.

2단계 — 9월 1일 ~ 9월 27일
C++ 2차 + STL

약 4주.

9/1 ~ 9/7
STL ①
vector
deque
list
iterator
9/8 ~ 9/14
STL ②
map
unordered_map
set
unordered_set
queue
stack
priority_queue
9/15 ~ 9/21
STL 알고리즘
sort
find
lower_bound
upper_bound
binary_search
accumulate
lambda + algorithm
9/22 ~ 9/27
C++ 총복습

이때는 책을 보는 것보다 질문에 답하는 것을 한다.

예:

vector와 list의 차이는?

map과 unordered_map의 차이는?

unique_ptr와 shared_ptr의 차이는?

move semantics가 필요한 이유는?

virtual destructor가 필요한 이유는?

RAII란?

이 질문에 막힘없이 답할 수 있으면 성공.

9/28 ~ 10/2
🏖 휴가

공부 계획에서 제외한다.

이 기간에는 공부를 억지로 넣지 않는 게 좋다.

정말 공부하고 싶으면 책 읽기 정도만.

3단계 — 10월 3일 ~ 10월 19일
Linux ①

이제부터 네 약점을 제대로 보완한다.

10/3 ~ 10/9
Linux 기본 명령어

다음에 익숙해진다.

pwd
ls
cd
cp
mv
rm
mkdir
cat
less
head
tail
grep
find

그리고

man
which
history
10/10 ~ 10/16
Process

OSTEP과 연결해서 공부.

Process란?
PID
Parent / Child
fork
exec
wait
exit
signal

그리고 Linux 명령어:

ps
top
kill
10/17 ~ 10/19
복습

여기서 한번 정리.

특히:

프로그램을 실행하면 Linux에서 무슨 일이 일어나는가?

를 자기 말로 설명해본다.

4단계 — 10월 20일 ~ 11월 5일
Linux ②
10/20 ~ 10/26
File / File Descriptor

이건 정말 중요하다.

공부:

file
open
read
write
close
file descriptor
stdin
stdout
stderr

그리고 반드시

socket과 file descriptor의 관계

까지 연결한다.

10/27 ~ 11/2
Linux 개발환경
gcc/g++
make
CMake
Git
GDB

GDB:

break
run
next
step
continue
print
bt

이 정도.

11/3 ~ 11/5
Linux 전체 복습

이 질문들을 답할 수 있으면 된다.

Process란?

PID란?

fork란?

exec란?

File Descriptor란?

signal이란?

GDB는 왜 필요한가?

11/6 ~ 11/8
🏖 휴가

완전히 제외.

5단계 — 11월 9일 ~ 11월 30일
Network ①

여기부터 네가 이미 읽은 네트워크 하향식 접근을 다시 활용한다.

이번에는 "네트워크 공부"가 아니라

"서버 프로그램은 네트워크를 어떻게 사용하는가?"

관점으로 본다.

11/9 ~ 11/15
인터넷 구조 복습
Application layer
Transport layer
Network layer
Link layer
IP
Port

목표:

Application
     ↓
TCP/UDP
     ↓
IP
     ↓
Ethernet

구조를 설명할 수 있는 것.

11/16 ~ 11/22
TCP 집중

공부:

Connection
3-way handshake
Sequence number
ACK
Retransmission
Flow control
Congestion control

그리고 가장 중요한 질문:

TCP는 왜 신뢰성이 있는가?

11/23 ~ 11/30
TCP와 게임 서버

여기서부터 게임 서버와 연결.

생각할 것:

TCP는 message protocol인가?

TCP에서 send() 한 번 했다고 recv() 한 번에 그대로 받을 수 있는가?

Packet이란 정확히 무엇인가?

TCP에서 Packet framing이 왜 필요한가?

이걸 이해하면 상당히 좋다.

6단계 — 12월 1일 ~ 12월 20일
Network ② — Socket

여기가 게임 서버 공부의 입구다.

12/1 ~ 12/7
Socket 기본

다음 API를 공부한다.

socket()
bind()
listen()
accept()
connect()

서버 흐름:

socket
 ↓
bind
 ↓
listen
 ↓
accept

클라이언트:

socket
 ↓
connect
12/8 ~ 12/14
데이터 송수신
send()
recv()

그리고

Send buffer
Receive buffer
Partial send
Partial recv

를 공부한다.

12/15 ~ 12/20
Blocking / Non-blocking

공부:

Blocking
Non-blocking
select
poll
epoll
IOCP

단, epoll/IOCP는 여기서 깊게 공부하지 않는다.

지금 목표는:

"왜 이런 기술이 등장했는가?"

까지만.

7단계 — 12월 21일 ~ 12월 31일
OS + Concurrency ①

이제 OSTEP을 다시 꺼낸다.

12/21 ~ 12/25
Process / Thread
Process
Thread
Context switching
Scheduling
12/26 ~ 12/31
Concurrency
Race Condition
Critical Section
Mutex
Lock

여기서부터 C++과 연결한다.

std::thread
std::mutex
std::lock_guard
8단계 — 2027년 1월 1일 ~ 1월 9일
OS + Concurrency ②

짧지만 중요하다.

1/1 ~ 1/4
Synchronization
Mutex
Condition Variable
Semaphore
Atomic
1/5 ~ 1/7
Deadlock
Deadlock 조건
발생 원인
해결 방법
1/8 ~ 1/9
Thread Pool

코드를 직접 만들 필요는 없다.

구조를 이해한다.

              ┌─ Worker
Task Queue ───┼─ Worker
              ├─ Worker
              └─ Worker

그리고:

왜 Thread Pool을 사용하는가?

를 설명할 수 있도록 한다.

1월 10일 ~ 2월 3일
🏖 사실상 휴가

여기는 새로운 공부를 하지 않는다.

이게 중요하다.

약 3주 반 정도 남는데, 여기서 새로운 책을 시작하면 오히려 머릿속이 엉킨다.

대신 휴가 중 공부가 가능한 날에는 복습만 한다.

9. 1월 10일 이후 복습 순서

이 순서로 돌린다.

Day 1

C++ 메모리

Day 2

C++ OOP

Day 3

STL

Day 4

Linux Process

Day 5

Linux File Descriptor

Day 6

TCP

Day 7

Socket

Day 8

Thread

Day 9

Mutex / Race Condition

Day 10

Game Server 구조

그리고 반복.

10. 그런데 게임 서버 공부는 어디 갔냐?

이 부분이 중요해.

게임 서버를 1월에 처음 공부하는 게 아니다.

12월 Network 공부부터 조금씩 섞는다.

예를 들어 TCP를 공부하면서:

TCP
 ↓
Socket
 ↓
Session
 ↓
Packet
 ↓
Game Server

이렇게 연결한다.

그리고 12월부터 네가 가진

NewbieGameServerProgrammerLearningMaterials

자료를 주 1~2회 정도 읽는다.

단, 전체를 정독하지 않는다.

11. 게임 서버 공부의 정확한 범위

군대에서는 여기까지만.

반드시 이해
Client / Server
Client
  ↕
Server
Session
Session
 ├─ Socket
 ├─ Receive Buffer
 ├─ Send Buffer
 └─ Client State
Packet
Header
+
Body
Room
Server
 ├─ Room 1
 ├─ Room 2
 └─ Room 3
Game Loop
Network
 ↓
Game Logic
 ↓
State Update
 ↓
Broadcast
Thread
Network Thread
      ↓
Game Thread
      ↓
Worker

정도의 개념.

12. 반대로 6개월 동안 하지 말 것

이건 꽤 중요하다.

❌ Unreal Engine

지금 필요 없음.

❌ Unity

지금 필요 없음.

❌ Redis 심화

아직 필요 없음.

❌ Kafka

필요 없음.

❌ Kubernetes

필요 없음.

❌ AWS

지금은 필요 없음.

❌ Docker 심화

필요 없음.

❌ 분산 시스템

나중.

❌ MMO 서버 아키텍처

나중.

❌ IOCP 심화

전역 후.

❌ epoll 심화

전역 후.

❌ 서버 프로젝트

지금은 못 하니까 억지로 하지 않음.

13. 대신 알고리즘은 6개월 내내

이건 별도 트랙이다.

주 5일 정도:

30~40분.

8월

배열 / 문자열

9월

스택 / 큐 / 덱

10월

BFS / DFS

11월

이분탐색 / 그리디

12월

DP 기초

1월

그래프 / 최단거리

다만 문제를 많이 풀려고 하지 마.

주 5~10문제 정도면 충분하다.

지금은 체력 만들기다.

14. 전체 공부시간을 계산해보자

평균 하루 2.5시간이라고 하면:

메인 공부      1시간 20분
알고리즘       40분
복습           30분

정도.

그런데 휴가를 제외하고 약 4개월 반 정도 집중한다고 하면 꽤 많은 시간이 나온다.

대략적으로:

하루 2.5시간 × 약 130일 = 325시간

정도다.

325시간이면 충분하다.

문제는 시간이 아니라 분산되는 것이다.

그래서 이번 6개월에는 책을 추가하지 않는 게 좋다.

15. 네가 매주 반드시 남겨야 할 결과물

싸지방이라 코드를 못 만들더라도 결과물을 남겨야 한다.

매주 하나의 문서를 만든다.

예:

2026-08-16 C++ Pointer.md
2026-08-23 C++ OOP.md
2026-08-30 Modern C++.md
2026-10-09 Linux Process.md
2026-10-19 Linux FD.md
2026-11-22 TCP.md
2026-12-14 Socket.md
2026-12-31 Thread.md
2027-01-09 Concurrency.md

그리고 문서마다:

1. 한 줄 정의

2. 왜 필요한가

3. 어떻게 동작하는가

4. 관련 개념

5. 게임 서버에서는 어떻게 쓰이는가

6. 내가 이해하지 못한 부분

6개만 작성한다.

16. 특히 매주 "백지 테스트"를 해

이게 너한테 상당히 중요하다.

예를 들어 TCP를 공부했다면 책을 덮고:

TCP란?

TCP의 특징은?

TCP connection은 어떻게 만들어지는가?

TCP는 데이터를 어떻게 전달하는가?

TCP에서 recv()는 어떤 문제를 가질 수 있는가?

게임 서버에서 TCP를 사용할 때 어떤 문제가 있는가?

를 적는다.

못 쓰면 다시 공부한다.

이걸 하면 "1회독했는데 기억 안 남음" 문제가 상당히 줄어든다.

17. 전역 직전 최종 시험

2월 초에는 아래 질문에 답해봐.

C++
RAII란?
unique_ptr와 shared_ptr 차이는?
move semantics란?
virtual이 필요한 이유는?
vector와 list 차이는?
map과 unordered_map 차이는?
Linux
Process란?
Thread란?
File Descriptor란?
fork와 exec 차이는?
GDB는 왜 쓰는가?
Network
IP와 Port 차이는?
TCP와 UDP 차이는?
TCP 3-way handshake란?
TCP가 byte stream이라는 것은 무슨 뜻인가?
socket이란?
listen/accept는 무엇을 하는가?
OS
Race Condition이란?
Mutex가 필요한 이유는?
Deadlock이란?
Atomic이란?
Thread Pool이란?
Game Server
Session이란?
Packet이란?
Room이란?
Game Loop란?
서버가 클라이언트를 믿으면 안 되는 이유는?
게임 서버에서 TCP를 사용할 때 Packet 구조가 왜 필요한가?

20개 이상을 자기 말로 설명할 수 있으면 군생활 공부는 성공했다고 봐도 된다.

18. 그리고 전역 첫날부터 이렇게 시작하면 된다

2월 3일 전역.

그때부터는 완전히 공부 방식이 바뀐다.

1개월차
Linux 환경 구축
CMake
Git
GDB
Socket
2개월차
TCP Echo Server
Multi Client
3개월차
Session
Packet
Thread
Thread Pool
4개월차
Room
Game Loop
5개월차
DB
6개월차
epoll / IOCP

그 이후:

게임 서버 프로젝트

로 들어간다.

즉, 군대 6개월을 끝내고 전역하자마자 "뭐부터 하지?"가 아니라 바로 Socket Programming부터 시작할 수 있는 상태를 만드는 것이다.

19. 네 상황에서 가장 현실적인 최종 그림
             현재
              │
              ▼
       C++ 기초는 있음
       CS 1회독 경험 있음
       Linux 매우 약함
       Server 경험 없음
              │
              │
        2026.08 ~ 10
              │
              ▼
         C++ + Linux
              │
              │
        2026.11 ~ 12
              │
              ▼
        Network + Socket
              │
              │
        2026.12 ~ 27.01
              │
              ▼
       OS + Concurrency
              │
              │
        2027.01 ~ 02
              ▼
       Game Server 구조
              │
              ▼
          2027.02.03
             전역
              │
              ▼
       "이제 직접 만든다"
              │
              ▼
       Socket Server
              │
              ▼
       Multi Client
              │
              ▼
       Game Server
              │
              ▼
       DB / IOCP / epoll
              │
              ▼
          포트폴리오

이 흐름이 네 상황에는 가장 맞아.

그리고 딱 하나 더 강조하고 싶어.

지금 네 목표를 "게임 서버 개발자가 되기"로 잡지 마.

너무 멀어.

2월 3일의 목표는 훨씬 작게:

"게임 서버 개발을 시작할 준비가 끝난 사람"

이면 된다.

지금까지 네 공부가 열혈 C++ 1회독 → 네트워크 1회독 → OSTEP 1회독 → 바킹독 1회독 식으로 흘러갔다면, 이번 6개월은 그걸 한 줄의 지식 체계로 연결하는 기간으로 쓰는 게 가장 가치 있다.

그리고 전역 후부터 실제 코딩을 시작하면 된다.

특히 네 상황에서는 8~12월의 공부 순서를 절대 뒤섞지 않는 걸 추천한다.
C++ → Linux → Network → Socket → OS/Concurrency → Game Server 순서를 타면, 12월쯤부터 네가 전에 읽었던 게임 서버 자료가 갑자기 훨씬 잘 이해되기 시작할 가능성이 높다.
