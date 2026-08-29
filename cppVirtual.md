# 8/21 — virtual

### virtual이란 무엇인가?

가상함수를 선언하기 위해 필요한 거

### virtual 함수가 필요한 이유는?

부모클래스로 자식 클래스 객체를 다룰 때 자식의 함수를 호출하기 위해

### virtual이 없는 함수 호출과 있는 함수 호출은 어떻게 다른가?

부모 클래스 포인터로 자식클래스를 지정했을 때, virtual이 없는 함수 호출은 부모클래스의 멤버함수가, 있는 함수 호출은 자식클래스의 멤버
함수가 실행된다.

### virtual 함수 호출은 실행 시 어떻게 동작하는가?

vptr이 가상 함수 테이블에서 적절한 함수를 찾아 실행시킨다 

### vtable과 vptr은 무엇인가?

vtable - (보통은) read only data영역에 있는 가상함수들의 주소들이 담긴 테이블

vptr - vtable을 가르키는 포인터

### virtual 함수가 객체의 메모리 구조에 어떤 영향을 주는가?

객체에 vptr의 메모리가 할당되어 8바이트 정도 더 소모할 수 있다. 함수자체는 code 영역에 선언되어 있어 가상함수가 여러개여도 객체의
메모리 사용량은 늘어나지 않는다.

---

### 게임 서버에서 virtual이 필요한 상황은 무엇인가?
(제미니햄 도와줘요)
게임 서버 개발(주로 C++ 또는 C# 환경)에서 virtual(가상 함수)은 객체 지향 프로그래밍의 핵심인
'다형성(Polymorphism)'을 구현하기 위해 필수적입니다.

게임 서버는 수만 개의 다양한 객체(유저, 몬스터, 아이템, 스킬 등)를 실시간으로 동시에 처리해야 하므로, 이들을 하나의 공통된 방식으로
관리할 때 virtual이 빛을 발합니다.

게임 서버에서 virtual이 반드시 필요하거나 유용하게 쓰이는 대표적인 상황 5가지를 정리해 드립니다.

**1. 게임 내 오브젝트(Entity)의 통합 관리 및 업데이트**

서버의 맵(Map)이나 섹터(Sector)에는 플레이어, 몬스터, NPC, 드랍된 아이템 등 다양한 객체가 존재합니다. 서버는 매
프레임(Tick)마다 이 객체들의 상태를 갱신해야 합니다.

  - 상황: 모든 객체를 하나의 리스트(std::vector<GameObject*>)에 담아 루프를 돌며 업데이트하고 싶을 때.
  - 적용: 최상위 부모 클래스에 virtual void Update()를 선언합니다.

```cpp
class GameObject {
public:
    virtual void Update() = 0; // 순수 가상 함수
    virtual void OnDeath() = 0; 
};

class Player : public GameObject {
public:
    void Update() override { /* 스태미나 회복, 버프 시간 감소 등 플레이어 전용 로직 */ }
    void OnDeath() override { /* DB에 사망 기록, 경험치 하락 로직 */ }
};

class Monster : public GameObject {
public:
    void Update() override { /* AI 어그로 판단, 순찰 로직 */ }
    void OnDeath() override { /* 아이템 드랍, 리스폰 타이머 시작 */ }
};

// 서버의 틱(Tick) 처리 부분
for(GameObject* obj : mapObjects) {
    obj->Update(); // 플레이어인지 몬스터인지 몰라도 각자 맞는 로직이 실행됨
}
```

**2. 패킷 처리 (Packet Handling) 및 커맨드 패턴**

클라이언트로부터 초당 수백~수천 개의 다양한 네트워크 패킷(이동, 공격, 채팅, 거래 등)이 서버로 들어옵니다. 이를 if-else나
switch문으로만 처리하면 코드가 수만 줄이 되어 유지보수가 불가능해집니다.

  - 상황: 수많은 종류의 패킷을 각각의 핸들러(Handler) 클래스로 분리하여 처리할 때.
  - 적용:

```cpp
class PacketHandler {
public:
    virtual void Execute(Player* player, Stream& packetData) = 0;
};

class MoveHandler : public PacketHandler {
public:
    void Execute(Player* player, Stream& packetData) override {
        // 이동 패킷 파싱 및 서버 내 플레이어 좌표 이동 로직, 시야(AOI) 브로드캐스팅
    }
};

class AttackHandler : public PacketHandler {
public:
    void Execute(Player* player, Stream& packetData) override {
        // 타겟 데미지 계산 및 사망 처리 로직
    }
};

// 패킷이 도착하면 ID에 맞는 핸들러를 찾아 실행 (Map 등에 미리 등록해둠)
PacketHandler* handler = handlerMap[packetId];
handler->Execute(player, packetData);
```

**3. 아이템 및 스킬 시스템 구현**

RPG 게임 서버에는 수백 가지의 아이템과 스킬이 존재합니다. '포션'을 사용할 때와 '귀환 주문서'를 사용할 때 서버가 처리해야 할 로직은
완전히 다릅니다.

  - 상황: 유저가 인벤토리에서 '사용(Use)' 버튼을 눌렀을 때, 아이템의 종류에 따라 다른 효과를 서버에 적용해야 할 때.
  - 적용:

```cpp
class Item {
public:
    virtual bool Use(Player* user) = 0;
};

class HpPotion : public Item {
public:
    bool Use(Player* user) override {
        user->AddHp(100);
        return true; // 소비됨
    }
};

class TownScroll : public Item {
public:
    bool Use(Player* user) override {
        if (user->IsInCombat()) return false; // 전투 중 사용 불가
        user->Teleport(TOWN_X, TOWN_Y);
        return true;
    }
};
```

**4. FSM (유한 상태 기계) 기반의 몬스터 AI**

서버에서 몬스터의 AI를 구현할 때 주로 상태(State) 패턴을 사용합니다. 대기, 이동, 추적, 공격, 도망 등의 상태를 클래스로 나눕니다.

  - 상황: 몬스터가 현재 어떤 상태인지에 따라 행동 로직이 달라져야 할 때.
  - 적용:

```cpp
class AIState {
public:
    virtual void Enter(Monster* mob) {}
    virtual void Update(Monster* mob) = 0;
    virtual void Exit(Monster* mob) {}
};

class ChaseState : public AIState {
    void Update(Monster* mob) override {
        // 타겟과의 거리 계산, 일정 거리 이상 멀어지면 ReturnState로 전환 등
    }
};
```

**5. 데이터베이스(DB) 또는 로깅 시스템의 추상화**

게임 서버는 MySQL, Redis, MongoDB 등 다양한 저장소와 통신합니다. 개발 환경(로컬)과 라이브 환경의 DB가 다를 수도
있습니다.

  - 상황: 비즈니스 로직(게임 로직)을 수정하지 않고, 하위 DB 접근 기술만 교체하고 싶을 때.
  - 적용: 인터페이스(순수 가상 클래스)를 활용한 의존성 주입(DI).

```cpp
class IDatabase {
public:
    virtual bool SavePlayerInfo(const PlayerData& data) = 0;
};

class MySQLDatabase : public IDatabase { ... };
class RedisDatabase : public IDatabase { ... }; // 캐싱용
class DummyDatabase : public IDatabase { ... }; // 단위 테스트용
```

**⚠️ 주의할 점 (서버 성능과 virtual)**

게임 서버에서 virtual은 코드의 가독성과 확장성을 극대화하지만, **성능적 비용(Overhead)**이 존재합니다.

1.  가상 함수 테이블(vtable) 참조 비용: 함수를 호출할 때마다 객체의 메모리를 참조해 vtable을 찾고, 실제 함수 주소를 찾는
    과정이 추가됩니다.
2.  캐시 미스(Cache Miss) 및 분기 예측 실패: 여러 종류의 객체가 섞인 배열을 루프 돌며 virtual 함수를 호출하면, CPU의
    명령어 캐시 적중률이 떨어져 심각한 성능 저하(Cache Thrashing)를 유발할 수 있습니다.

해결/대안(최신 트렌드): 이러한 성능 문제 때문에 최근의 고성능 게임 서버(특히 대규모 MMO)에서는 깊은 상속 구조와 virtual 함수
남용을 피하고, 데이터 중심 설계인 ECS(Entity-Component-System) 아키텍처를 도입하여 다형성을 대체하고 캐시 효율을
극대화하는 방식을 많이 사용합니다.

단, 패킷 핸들링, 최상위 상태 제어 등 CPU 병목이 크게 발생하지 않는 아키텍처 구조 단원에서는 여전히 virtual이 가장 직관적이고
훌륭한 선택입니다. (C++11 이상의 final 키워드를 함께 사용하여 컴파일러 최적화를 돕는 것이 좋습니다).
