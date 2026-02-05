# **Earn Your Legacy: 사회 실험형 정치 MMORPG를 위한 시스템 설계 및 기술적 타당성 분석 보고서**

## **1\. 서론: 가상 세계의 가치 재정립과 'Earn Your Legacy'의 비전**

### **1.1 연구 배경 및 목적**

현대 MMORPG(Massively Multiplayer Online Role-Playing Game) 시장은 '테마파크(Theme Park)' 형 구조의 고착화로 인한 정체기를 겪고 있다. 플레이어는 불멸의 아바타를 통해 수직적 성장(Level, Gear Score)만을 추구하며, 이는 콘텐츠 소모 속도의 가속화와 엔드 콘텐츠(Endgame)의 고갈이라는 만성적인 문제를 야기한다.1 이에 대한 대안으로 제시된 샌드박스(Sandbox) 장르 역시 초기 진입 장벽과 후반부의 고인물화(Power Creep), 그리고 사회적 상호작용의 부재라는 한계에 직면해 있다.2

본 보고서는 이러한 문제의식에서 출발하여, 사용자(Client)가 제시한 "Earn Your Legacy"라는 핵심 아이디어를 구체화하고, 이를 실현하기 위한 게임 디자인, 경제 모델, 그리고 기술적 아키텍처를 심층 분석한다. 이 프로젝트의 핵심은 \*\*영구적 죽음(Permadeath)\*\*을 통한 경제의 순환, **유산(Legacy)** 시스템을 통한 메타 프로그레션(Meta-Progression), 그리고 \*\*유저 정의 법률(User-Defined Laws)\*\*에 기반한 사회 실험적 정치 체제의 결합이다.

### **1.2 핵심 철학: 아바타에서 가문(Lineage)으로의 가치 이동**

'Earn Your Legacy'의 가장 급진적인 제안은 플레이어의 정체성을 단일 캐릭터(Avatar)가 아닌, 시대를 관통하는 가문(Lineage) 또는 영혼(Soul)에 두는 것이다.

* **삶의 유한성:** 모든 캐릭터는 수명, 전투, 사고 등으로 반드시 죽는다. 이 죽음은 실패가 아니라 유산을 남기는 과정이다.3  
* **아이템의 고유성:** 제작된 아이템은 단순한 데이터베이스의 복사본이 아니라, 제작자의 이름과 역사가 기록된 유일무이한 아티팩트(Artifact)다.  
* **사회적 결과:** 이 모든 과정은 무정부 상태에서 시작하여 문명을 건설하고, 필연적으로 부패하여 혁명으로 이어지는 정치적 시뮬레이션 안에서 이루어진다.

## ---

**2\. 제1장: 인생의 설계와 고유 제작 시스템 (The Life Cycle)**

이 장에서는 사용자의 첫 번째 아이디어인 "자신만의 제작 아이템이 있는 세상"과 "인생을 살아가는 유저"의 개념을 구체화한다.

### **2.1 절차적 생성에 기반한 인생의 다양성**

전통적인 MMORPG에서 모든 전사는 동일한 스킬 트리를 가진다. 그러나 'Earn Your Legacy'에서는 각 캐릭터의 탄생이 유전적, 환경적 요인에 의해 결정되어야 한다.

#### **2.1.1 유전적 특성과 재능 (Genetic Traits)**

캐릭터 생성 시, 플레이어는 선대 캐릭터(Legacy)로부터 특정 형질을 물려받거나, 무작위로 생성된 재능을 부여받는다.4

* **신체적 특성:** 근력 한계치, 이동 속도, 질병 저항력 등은 수직적 성장이 아닌 수평적 다양성을 제공한다. 예를 들어, 어떤 캐릭터는 '광산 노동'에 특화된 근지구력을 타고날 수 있으며, 이는 해당 생애의 직업 선택에 영향을 미친다.  
* **환경적 요인:** 태어난 지역(Biome)에 따라 초기 기술 습득 속도가 달라진다. 사막에서 태어난 캐릭터는 물 관리 기술에 보너스를 받고, 숲에서 태어난 캐릭터는 목공 기술에 이점을 가진다. 이는 *One Hour One Life*에서 증명된 바와 같이, 플레이어 간의 상호 의존성을 높이는 장치로 작용한다.5

#### **2.1.2 시간 제한적 성장과 노화 메커니즘**

캐릭터는 현실 시간 또는 게임 내 틱(Tick)에 따라 노화한다. 노화는 단순한 디버프가 아니라, 플레이어에게 "마감 기한"을 부여하여 행동의 우선순위를 정하게 하는 전략적 요소다.7

* **청년기:** 신체 능력의 정점. 전투와 탐험에 적합하다.  
* **중년기:** 제작 기술과 정치적 영향력의 정점.  
* **노년기:** 신체 능력 저하, 지혜(멘토링 보너스) 증가. 이 시기에 플레이어는 자신의 죽음을 대비하여 유산을 정리하고 후계자를 양성해야 한다.

### **2.2 영혼이 깃든 아이템: 제작과 프로비넌스(Provenance)**

"자신만의 제작 아이템"이라는 아이디어를 실현하기 위해서는 기존의 아이템 테이블 구조를 탈피해야 한다. 모든 아이템은 고유한 ID(UUID)와 변경 불가능한 역사 기록(Log)을 가져야 한다.

#### **2.2.1 동적 레시피 시스템 (Dynamic Recipe System)**

*EVE Online*의 제작 시스템이 청사진(Blueprint)에 의존한다면, 본 게임은 재료의 조합과 제작자의 '인생 경험'을 반영한다.8

* **재료의 DNA:** 철광석이라도 채굴된 위치(던전 깊이, 지역)에 따라 미세한 속성 차이(불순물, 마력 함유량)를 가진다.  
* **제작자의 서명:** 아이템 제작 시, 제작자의 현재 상태(나이, 기분, 스킬 숙련도)가 아이템의 '숨겨진 속성'으로 각인된다.  
  * *예시:* "분노에 찬 대장장이"가 만든 검은 치명타 확률이 높지만 내구도가 낮을 수 있다.

#### **2.2.2 아이템 이력 추적 (Item Genealogy)**

이 시스템의 핵심은 **프로비넌스(Provenance)**, 즉 아이템의 소유 및 사용 이력을 추적하는 것이다.10 데이터베이스 차원에서 아이템은 단순한 객체가 아니라 하나의 그래프 노드(Graph Node)로 취급된다.

| 항목 | 설명 | 데이터 예시 |
| :---- | :---- | :---- |
| **Creator\_ID** | 제작자 | User\_Alpha (Year 105\) |
| **Material\_Source** | 재료 출처 | Deep\_Mine\_Sector\_7 (Star-Metal) |
| **Kill\_Count** | 처치 기록 | Boss\_Red\_Dragon (1회), Player\_X (3회) |
| **Owners\_Log** | 소유자 역사 | User\_Alpha \-\> User\_Beta (상속) \-\> User\_Gamma (약탈) |

이러한 이력은 아이템의 가치를 '성능(Stats)'에서 '역사(History)'로 전환시킨다. 유저는 성능이 떨어지더라도 "초대 왕이 사용했던 검"이라는 이유만으로 해당 아이템을 소유하려 할 것이며, 이는 정치적 정통성을 부여하는 도구가 된다.12

## ---

**3\. 제2장: 죽음과 상속 시스템 (The Death & Legacy)**

사용자의 두 번째 아이디어인 "죽으면 유산을 남기고, 던전에서 사망하기도 하며 사람들이 그것을 획득하는" 과정을 설계한다. 이는 게임 경제의 인플레이션을 억제하고(Entropy), 플레이 동기를 부여하는(Motivation) 핵심 루프다.

### **3.1 영구적 죽음(Permadeath)의 유형과 결과**

죽음은 그 원인과 장소에 따라 다른 결과를 초래해야 한다. 이는 플레이어에게 리스크 관리(Risk Management)를 강요한다.13

#### **3.1.1 야전/던전 사망 (The Tragic Death)**

위험 지역(PvP 존, 던전)에서의 사망은 가장 가혹한 페널티를 가진다.

* **소지품(Inventory):** 100% 드랍된다(Full Loot). 이는 던전을 탐험하는 다른 유저나 몬스터(NPC)에게 획득될 수 있다.  
* **시체(Corpse):** 일정 시간 동안 물리적 객체로 남는다. 동료들이 시체를 회수하여 장례를 치르거나 아이템을 회수할 수 있다. 만약 회수되지 못하면 아이템은 던전의 전리품 테이블(Loot Table)로 흡수되어, 훗날 보스 몬스터가 그 장비를 착용하고 나타날 수 있다. 이는 "내 아이템이 세상의 일부가 되는" 경험을 제공한다.15

#### **3.1.2 자연사 및 은퇴 (The Planned Death)**

노화로 인한 죽음이나 자발적 은퇴는 플레이어가 통제할 수 있는 죽음이다.

* **유산 정리:** 플레이어는 죽기 전에 자신의 자산을 '상속 가능한 상태'로 전환할 수 있다.  
* **멘토링:** 후계자(다음 캐릭터 또는 다른 유저)에게 기술 일부를 전수하여 스킬 숙련도 감소를 최소화한다.

### **3.2 유언장(Will)과 상속 메커니즘**

죽음 이후 자산이 이동하는 방식은 **유언장 시스템**에 의해 제어된다. 이는 단순한 자동 전송이 아니라, 게임 내 법률과 상호작용하는 복잡한 계약이다.16

#### **3.2.1 유언장의 작성과 집행**

플레이어는 생전에 공증인 NPC 또는 변호사 직업을 가진 유저를 통해 유언장을 작성한다.

* **수혜자 지정:** 특정 유저, 길드, 또는 자신의 다음 캐릭터(Next of Kin).  
* **조건부 상속:** "나의 복수를 해주는 자에게 이 검을 준다"와 같은 퀘스트 형태의 상속도 가능하다(스마트 컨트랙트 기반).

#### **3.2.2 상속세와 엔트로피 (The Death Tax)**

경제적 정체(고인물화)를 막기 위해, 상속 과정에는 반드시 손실이 발생해야 한다.18

* **엔트로피 법칙:** 모든 자산 이전 시 기본적으로 10\~30%의 자산이 소멸하거나 내구도가 손상된다.  
* **정치적 상속세:** 플레이어 정부(Government)는 상속세율을 책정할 수 있다. 높은 상속세는 부의 재분배를 유도하지만, 부유한 유저들의 반발이나 탈세(자산을 땅에 묻는 행위 등)를 유발한다.

### **3.3 레거시 포인트와 어센션(Ascension)**

캐릭터는 사라지지만, 계정(Account) 차원의 진척도는 유지되어야 박탈감을 완화할 수 있다.19

* **레거시 점수(Legacy Score):** 한 생애 동안의 업적(탐험, 제작, 전투, 정치 등)을 합산하여 점수화한다.  
* **어센션 특전:** 레거시 점수를 소모하여 다음 생애에 적용될 메타 특전(Perks)을 해금한다.  
  * *수직적 강화 지양:* "공격력 \+10%" 같은 수직적 강화보다는, "동방의 언어 이해 가능", "희귀 광물 탐지 가능" 등 **새로운 가능성을 여는 수평적 보상**에 집중하여 파워 인플레이션을 방지한다.21

## ---

**4\. 제3장: 사회 실험형 정치 시스템 (The Political Sandbox)**

세 번째 아이디어인 "사회 실험형 정치 MMO"는 게임의 초기, 중기, 말기 단계에 따라 사회 구조가 진화하는 과정을 통해 구현된다. 유저 정의 법률(User-Defined Laws)은 이 진화의 핵심 동력이다.

### **4.1 초기 단계 (Early Game): 무정부 상태와 자연 상태 (State of Nature)**

서버 초기 또는 변방 지역은 홉스(Hobbes)적 자연 상태다. 법은 없으며, 생존이 유일한 목표다.22

* **사회적 장치:** **신뢰(Trust)와 부족(Tribe).**  
  * 시스템적인 보호 장치가 없으므로, 플레이어는 생존을 위해 자연스럽게 소규모 그룹을 형성한다.  
  * *One Hour One Life*와 같이, 신규 유저(아기/신입)는 기존 유저의 보호 없이는 생존이 불가능하도록 설계하여 강제적인 사회적 유대를 형성한다.5  
* **갈등 요소:** 자원 쟁탈전. 희소한 자원을 두고 부족 간의 약탈과 전쟁이 발생한다.  
* **경제:** 물물교환 및 약탈 경제. 화폐는 아직 신뢰를 얻지 못한다.

### **4.2 중기 단계 (Mid Game): 사회 계약과 국가의 탄생**

생존이 안정되면 유저들은 자산을 보호하고 싶어 한다. 이 욕구는 '사회 계약'을 이끌어내며, 도시와 국가의 건설로 이어진다.

* **사회적 장치:** **헌장석(Charter Stone)과 법률 편집기(Law Editor).**  
  * 플레이어들은 자원을 모아 '헌장석'을 세우고 영토를 선포한다.  
  * *Eco* 게임의 법률 시스템을 차용하여, 프로그래밍 로직(If-Then)으로 법을 제정한다.24  
    * *예시:* "IF \[Citizen\] KILLS \[Citizen\] IN \[Zone: City\] THEN \[Action: Jail 10 mins\] AND \[Fine: 1000 Gold\]"  
* **집행 메커니즘:**  
  * **자동 집행(Code is Law):** 마법적 결계나 AI 경비병을 통해 시스템적으로 범죄를 차단하거나 즉결 심판한다. 비용이 많이 든다.  
  * **수동 집행(Sheriff System):** 보안관(Sheriff) 권한을 가진 유저에게 체포 권한을 부여한다. 부패할 가능성이 있어 정치적 견제가 필요하다.26  
* **경제:** 화폐의 발행과 조세 제도. 국가는 도로를 건설하고 치안을 제공하는 대가로 세금을 걷는다.

### **4.3 말기 단계 (Late Game): 쇠퇴, 독재, 그리고 혁명**

장기적으로 운영되는 MMO는 필연적으로 부의 집중과 계층 고착화(Inheritocracy) 문제를 겪는다. 'Earn Your Legacy'는 이를 게임의 엔드 콘텐츠로 승화시킨다.18

* **사회적 장치:** **불평등 지수(Inequality Index)와 혁명(Revolution).**  
  * 서버는 실시간으로 지니 계수(부의 불평등 정도)를 모니터링한다.  
  * 불평등이 임계치를 넘으면 '혁명' 메커니즘이 활성화된다.  
* **혁명 메커니즘:**  
  * 하위 계층 유저들에게 "혁명가" 버프가 부여된다(제작 비용 감소, 귀족 대상 데미지 증가).  
  * "단두대(Guillotine)" 아이템 제작이 해금된다. 이는 고레벨 유저(귀족)를 \*\*영구 처형(강제 상속세 100% 적용 및 유산 소멸)\*\*할 수 있는 유일한 무기다.12  
* **순환:** 혁명이 성공하면 기존의 법률과 소유권이 초기화되고, 사회는 다시 혼란기(초기 단계)로 돌아가 새로운 질서를 모색한다. 이 순환 구조는 서버 초기화(Wipe) 없이도 게임의 역동성을 유지한다.27

## ---

**5\. 기술적 아키텍처 및 구현 방안 (Technical Architecture)**

이 복잡한 상호작용(유산 상속, 법률 연산, 아이템 이력)을 실시간으로 처리하기 위해서는 기존의 웹 서버 구조를 넘어선 데이터베이스 중심의 아키텍처가 필요하다.

### **5.1 SpacetimeDB와 인메모리 로직 (Logic-in-Database)**

전통적인 "Application Server \+ SQL DB" 구조는 매 행동마다 DB를 조회해야 하므로 법률 시스템(이동할 때마다 법률 체크) 구현 시 레이턴시(Lag) 문제가 발생한다. 이에 대한 해결책으로 **SpacetimeDB**와 같은 차세대 데이터베이스 기술을 제안한다.28

* **개념:** 게임 로직(Rust/Wasm)이 데이터베이스 내부에서 직접 실행된다. 즉, 데이터 조회와 로직 처리가 메모리 상에서 원자적(Atomic)으로 이루어진다.  
* **적용:**  
  * **법률 연산:** 유저가 "A 지역에서 나무를 벤다"는 요청을 보내면, DB 내의 리듀서(Reducer)가 즉시 해당 지역의 법률 테이블을 조회하여 0ms에 가까운 속도로 허용 여부를 결정한다.30  
  * **트랜잭션 안전성:** 유언장 집행과 같은 민감한 자산 이동이 ACID 트랜잭션으로 보장되어, 서버 다운이나 복사 버그(Duplication Glitch)를 원천 차단한다.

### **5.2 그래프 데이터베이스를 활용한 족보(Lineage) 추적**

아이템과 가문의 방대한 역사를 저장하기 위해 관계형 데이터베이스(RDBMS)와 그래프 데이터베이스의 하이브리드 모델이 필요하다.11

* **노드(Node):** 플레이어, 아이템, 사건(Event).  
* **엣지(Edge):** CREATED, KILLED, INHERITED, STOLEN\_FROM.  
* 이 구조를 통해 "이 검은 누구의 손을 거쳐왔는가?"라는 복잡한 쿼리를 효율적으로 처리하고, 유저에게 시각화된 '역사 그래프'를 제공할 수 있다.

### **5.3 RLS(Row Level Security)를 활용한 정보전(Information Warfare)**

정치 게임에서 정보는 힘이다. SpacetimeDB의 **Row Level Security** 기능을 게임 메커니즘으로 활용한다.33

* 기본적으로 유저는 자신의 데이터만 볼 수 있다(SELECT \* FROM Items WHERE Owner \= Me).  
* **첩보 스킬:** "스파이" 직업을 가진 유저는 일시적으로 RLS 규칙을 우회하여 타인의 인벤토리나 유언장을 엿볼 수 있는 권한을 얻는다. 이는 기술적 보안 기능을 게임플레이 요소로 승화시킨 혁신적인 접근이다.

## ---

**6\. 게임 단계별 상세 장치 (Game Phase Devices Matrix)**

사용자가 요청한 "초기, 중기, 말기를 고려한 장치"를 구체적으로 정리한다.

| 단계 | 핵심 테마 | 주요 게임플레이 장치 (Devices) | 경제 및 상속 장치 | 정치 및 사회 장치 |
| :---- | :---- | :---- | :---- | :---- |
| **초기** (Early) | **생존 & 신뢰** (Survival) | **모닥불 (Campfire)** \- 소규모 안전지대 \- 접속 종료 시 생명 유지 \- 연료 필요 (활동 강제) | **비밀 은닉처 (Stash)** \- 맵 어딘가에 숨겨진 상자 \- 죽어도 유지되나 도난 위험 \- '보물지도'가 유일한 열쇠 | **근거리 음성 채팅** \- "손을 흔드는" 행위로 우호 표현 \- 배신과 협력의 딜레마 \- 자연적 리더 발생 |
| **중기** (Mid) | **질서 & 번영** (Order) | **헌장석 (Charter Stone)** \- 도시 선포 및 영역 설정 \- 건물 건설 권한 제어 | **공증인 & 은행 (Notary)** \- 안전한 자산 보관 \- 유언장 작성 및 상속세 납부 \- 계약 시스템 (청부, 거래) | **법률 테이블 (Law Table)** \- 코딩 방식의 법 제정 \- 보안관(Sheriff) 임명 \- 투표 및 의회 시스템 |
| **말기** (Late) | **부패 & 혁명** (Conflict) | **기념비 (Monument)** \- 가문의 위상을 높이는 거대 건축물 \- 유지비 과다 (자원 독점 유발) | **가문 금고 (Dynasty Vault)** \- 영구적 자산 축적 (Power Creep) \- 해킹/공성전의 주요 목표물 | **단두대 (Guillotine)** \- 불평등 지수 상승 시 해금 \- 지배층 영구 처형 기능 \- 혁명 성공 시 법률 초기화 |

## ---

**7\. 잠재적 문제점 및 해결 방안 (Risk Analysis)**

### **7.1 그리핑(Griefing)과 사회 공학적 공격**

퍼마데스 게임에서 가장 큰 위협은 시스템을 악용해 타인의 노력을 파괴하는 '그리퍼'들이다.35

* **문제:** 신규 유저를 안전지대 밖으로 유인해 살해하거나, 스파이 행위로 길드 창고를 터는 행위.  
* **해결책:**  
  * **사회적 신용 시스템(Karma):** *EVE Online*의 Security Status와 유사하게, 범죄 행위 시 '현상수배' 상태가 되며 도시 진입이 차단된다.37  
  * **멘토링 계약:** 신규 유저를 돕는 행위에 대해 시스템적 보상(버프, 명성)을 제공하여, 고레벨 유저가 뉴비를 보호할 동기를 부여한다.35

### **7.2 데이터베이스 마이그레이션과 지속성**

게임 업데이트나 시즌 초기화 시 데이터 유지가 기술적 난관이다.38

* **Incremental Migration:** *SpacetimeDB*의 특성을 활용하여, 구버전 테이블과 신버전 테이블을 공존시키며 점진적으로 데이터를 이관한다. 이를 통해 서버 중단(Downtime) 없이 게임을 업데이트하고 역사를 보존한다.

### **7.3 경제 인플레이션과 정체**

* **문제:** 상속을 통해 부가 계속 축적되면 화폐 가치가 하락한다.40  
* **해결책:** 아이템 내구도의 영구적 손상(수리 시 최대 내구도 감소)과 상속세(Entropy)를 통해 자원을 지속적으로 소각(Sink)한다.

## ---

**8\. 결론**

"Earn Your Legacy"는 단순한 게임을 넘어선 디지털 사회 실험이다. 플레이어는 자신의 \*\*생존(Survival)\*\*을 위해 투쟁하고, \*\*번영(Prosperity)\*\*을 위해 법을 만들며, \*\*역사(History)\*\*를 남기기 위해 죽음을 맞이한다.

이 프로젝트의 성공은 다음 세 가지 요소의 조화에 달려 있다.

1. **철학적 동의:** 플레이어가 "죽음은 끝이 아니라 새로운 시작"이라는 개념을 받아들이게 하는 내러티브 디자인.  
2. **기술적 혁신:** SpacetimeDB와 같은 최신 기술을 활용하여 유저가 직접 코딩하는 법률 시스템과 복잡한 상속 로직을 렉 없이 구현하는 것.  
3. **정치적 역동성:** 고인물화를 방지하고 끊임없이 새로운 지배층과 혁명 세력이 등장하도록 유도하는 경제적 밸런싱.

이 게임은 유저들에게 "당신은 무엇을 남길 것인가?"라는 질문을 끊임없이 던지며, 그 대답이 곧 게임의 역사가 되는 진정한 의미의 샌드박스 경험을 제공할 것이다.

# ---

**\[부록\] 상세 기획 및 분석 보고서**

## **9.1 시스템 심층 분석: 법률 시스템의 구현 (Deep Dive: Law Mechanics)**

### **9.1.1 법률 에디터의 UX/UI**

*Eco* 게임에서 영감을 받은 블록형 코딩 인터페이스를 제공한다. 프로그래밍 지식이 없는 유저도 "조건(Trigger) \- 대상(Target) \- 효과(Effect)"의 구조로 법을 만들 수 있다.

* **트리거:** 지역 진입, 아이템 채집, 공격, 거래, 채팅 등.  
* **필터:** 길드, 레벨, 재산, 평판, 소지 아이템.  
* **효과:** 이동 차단, 아이템 압수, 벌금 부과, 감옥 이송, 현상금 걸기.

### **9.1.2 법률의 계층 구조 (Hierarchy of Laws)**

법률 충돌을 방지하기 위해 헌법적 위계 질서를 둔다.

1. **자연법 (Server Config):** 개발자가 설정한 절대 규칙 (예: 중력, 버그 악용 금지).  
2. **헌법 (Constitution):** 국가의 기본 이념. 변경하기 매우 어렵다 (전체 투표 75% 이상 찬성 필요).  
3. **법률 (Statute):** 의회에서 제정하는 일반 법.  
4. **조례 (Ordinance):** 특정 지역(마을) 소유주가 설정하는 로컬 규칙. 상위 법에 위배될 수 없다.

## **9.2 경제 심층 분석: '피의 경제학' (Blood Economy)**

### **9.2.1 에센스(Essence) 시스템**

최상위 티어 아이템 제작에는 일반 자원 외에 '에센스'가 필요하다.

* **획득처:** 에센스는 오직 **플레이어의 죽음**을 통해서만 생성된다. 고레벨 캐릭터가 죽을수록 더 순도 높은 에센스가 드랍된다.  
* **경제적 함의:** 이는 "최고의 검을 만들기 위해 영웅의 희생이 필요하다"는 서사를 부여하며, PvP와 PK를 경제 활동의 일부로 편입시킨다. 평화로운 시대에는 에센스 가격이 폭등하여 전쟁을 부추기는 경제적 압력이 발생한다.12

### **9.2.2 다중 서명 금고 (Multi-sig Vaults)**

길드 자산의 횡령을 막기 위해 블록체인의 다중 서명(Multi-sig) 개념을 도입한다.41

* 길드 금고에서 아이템을 꺼내려면 간부 3명 이상의 동의(접속 및 승인)가 필요하다.  
* 이는 신뢰 비용을 시스템화한 것으로, 거대 길드의 운영 난이도를 높이고 내부 정치(파벌 싸움)를 유도한다.

## **9.3 기술 심층 분석: 서버 아키텍처 (Server Architecture)**

### **9.3.1 Rust & WebAssembly (Wasm) 기반 모듈**

게임 로직은 Rust로 작성되어 Wasm으로 컴파일된 후 SpacetimeDB에 업로드된다.43

* **안전성:** Rust의 메모리 안전성은 복잡한 상속 연산 중 발생할 수 있는 서버 크래시를 방지한다.  
* **확장성:** 샌드박스형 게임은 유저가 만든 오브젝트가 무한히 늘어날 수 있다. SpacetimeDB의 관계형 데이터 구조는 이를 효율적으로 인덱싱하고 쿼리할 수 있게 해준다.

### **9.3.2 데이터 마이그레이션 전략**

게임 규칙(법률 로직 등)이 변경될 때, 기존 데이터를 보존하기 위한 전략이다.

* **버전 관리:** 모든 아이템과 캐릭터는 Schema\_Version 태그를 가진다.  
* **Lazy Migration:** 데이터는 접근되는 순간 최신 버전으로 변환된다. 이를 통해 전체 서버를 멈추고 DB를 패치하는 시간을 없앤다.39

이 보고서는 "Earn Your Legacy"가 단순한 아이디어를 넘어, 기술적, 경제적, 사회적으로 실현 가능한 차세대 MMORPG 모델임을 입증한다.

#### **참고 자료**

1. Endgame slop killed mmos : r/MMORPG \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/MMORPG/comments/1qa722r/endgame\_slop\_killed\_mmos/](https://www.reddit.com/r/MMORPG/comments/1qa722r/endgame_slop_killed_mmos/)  
2. \[Discussion\]The Fundamental Problem of Sandbox MMOs(and themeparks) is Progression : r/MMORPG \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/MMORPG/comments/c6hhdk/discussionthe\_fundamental\_problem\_of\_sandbox/](https://www.reddit.com/r/MMORPG/comments/c6hhdk/discussionthe_fundamental_problem_of_sandbox/)  
3. Perfect Ten: MMOs that flirted with permadeath | Massively Overpowered, 2월 4, 2026에 액세스, [https://massivelyop.com/2019/08/21/perfect-ten-mmos-that-flirted-with-permadeath/](https://massivelyop.com/2019/08/21/perfect-ten-mmos-that-flirted-with-permadeath/)  
4. Family genetics and fatherhood / Main Forum / One Hour One Life Forums, 2월 4, 2026에 액세스, [https://onehouronelife.com/forums/viewtopic.php?id=8603](https://onehouronelife.com/forums/viewtopic.php?id=8603)  
5. Creating a FAMILY LEGACY in One Hour One Life \- YouTube, 2월 4, 2026에 액세스, [https://www.youtube.com/watch?v=VeaXQy5y2LA](https://www.youtube.com/watch?v=VeaXQy5y2LA)  
6. Starting Guide \- Official One Hour One Life Wiki, 2월 4, 2026에 액세스, [https://onehouronelife.fandom.com/wiki/Starting\_Guide](https://onehouronelife.fandom.com/wiki/Starting_Guide)  
7. Does perma death mechanics have the potential to aid in preventing problematic power creep within an MMORPG? : r/gamedesign \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/gamedesign/comments/1gvqozl/does\_perma\_death\_mechanics\_have\_the\_potential\_to/](https://www.reddit.com/r/gamedesign/comments/1gvqozl/does_perma_death_mechanics_have_the_potential_to/)  
8. Games with realistic economy, diplomacy/politics, a world that evolves without the player : r/gamingsuggestions \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/gamingsuggestions/comments/1bhs9g4/games\_with\_realistic\_economy\_diplomacypolitics\_a/](https://www.reddit.com/r/gamingsuggestions/comments/1bhs9g4/games_with_realistic_economy_diplomacypolitics_a/)  
9. Building an MMORPG Crafting System WITHOUT MINIGAMES \- YouTube, 2월 4, 2026에 액세스, [https://www.youtube.com/watch?v=7OJPNhZIcRY](https://www.youtube.com/watch?v=7OJPNhZIcRY)  
10. Provenance and Lineage \- MarkLogic, 2월 4, 2026에 액세스, [https://docs.marklogic.com/datahub/5.2/logs/about-provenance-lineage.html](https://docs.marklogic.com/datahub/5.2/logs/about-provenance-lineage.html)  
11. What Is Data Lineage? Tracking Data Through Enterprise Systems \- Neo4j, 2월 4, 2026에 액세스, [https://neo4j.com/blog/graph-database/what-is-data-lineage/](https://neo4j.com/blog/graph-database/what-is-data-lineage/)  
12. Designing an MMORPG system that replaces destructive habits with healthy equivalents, 2월 4, 2026에 액세스, [https://www.reddit.com/r/gamedesign/comments/1q99ttu/designing\_an\_mmorpg\_system\_that\_replaces/](https://www.reddit.com/r/gamedesign/comments/1q99ttu/designing_an_mmorpg_system_that_replaces/)  
13. How can I make permanent death in a MUD seem acceptable and fair to players?, 2월 4, 2026에 액세스, [https://gamedev.stackexchange.com/questions/77425/how-can-i-make-permanent-death-in-a-mud-seem-acceptable-and-fair-to-players](https://gamedev.stackexchange.com/questions/77425/how-can-i-make-permanent-death-in-a-mud-seem-acceptable-and-fair-to-players)  
14. Why Permadeath Matters. \- YouTube, 2월 4, 2026에 액세스, [https://www.youtube.com/watch?v=f9LSeW28Hsg](https://www.youtube.com/watch?v=f9LSeW28Hsg)  
15. Our True Lord and Savior is Permadeath : r/MMORPG \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/MMORPG/comments/magoqs/our\_true\_lord\_and\_savior\_is\_permadeath/](https://www.reddit.com/r/MMORPG/comments/magoqs/our_true_lord_and_savior_is_permadeath/)  
16. Planning for Your Gaming Accounts and Virtual Assets in a Will \- Cipherwill, 2월 4, 2026에 액세스, [https://www.cipherwill.com/blog/planning-for-your-gaming-accounts-and-virtual-assets-in-a-will-2856d63626188140abe1e97f1c9eb895](https://www.cipherwill.com/blog/planning-for-your-gaming-accounts-and-virtual-assets-in-a-will-2856d63626188140abe1e97f1c9eb895)  
17. Why Managing Digital Assets is Critical In Estate Planning \- Kitces.com, 2월 4, 2026에 액세스, [https://www.kitces.com/blog/estate-planning-digital-assets-documentation-financial-holdings-inventory-cryptocurrency-investment-online/](https://www.kitces.com/blog/estate-planning-digital-assets-documentation-financial-holdings-inventory-cryptocurrency-investment-online/)  
18. Turning Wealth Into Innovation: The Surprising Power of Inheritance Taxes \- ADB Blog, 2월 4, 2026에 액세스, [https://blogs.adb.org/blog/turning-wealth-innovation-surprising-power-inheritance-taxes](https://blogs.adb.org/blog/turning-wealth-innovation-surprising-power-inheritance-taxes)  
19. Endgame | Project Ascension Wiki | Fandom, 2월 4, 2026에 액세스, [https://project-ascension.fandom.com/wiki/Endgame](https://project-ascension.fandom.com/wiki/Endgame)  
20. Redefining Foundations | Ascension, 2월 4, 2026에 액세스, [https://ascension.gg/cz/news/redefining-foundations/141](https://ascension.gg/cz/news/redefining-foundations/141)  
21. Can Power Creep be overcome by requiring players to experience earlier content to reach later content? \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/gamedesign/comments/6k3h4u/can\_power\_creep\_be\_overcome\_by\_requiring\_players/](https://www.reddit.com/r/gamedesign/comments/6k3h4u/can_power_creep_be_overcome_by_requiring_players/)  
22. Massive, living, generational RPG idea — rigid class system \+ restarts, legacy, professions and permadeath (long) : r/MMORPG \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/MMORPG/comments/1numppn/massive\_living\_generational\_rpg\_idea\_rigid\_class/](https://www.reddit.com/r/MMORPG/comments/1numppn/massive_living_generational_rpg_idea_rigid_class/)  
23. How to structure early game sandbox? : r/DMAcademy \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/DMAcademy/comments/1poh06f/how\_to\_structure\_early\_game\_sandbox/](https://www.reddit.com/r/DMAcademy/comments/1poh06f/how_to_structure_early_game_sandbox/)  
24. Laws \- Eco \- English Wiki, 2월 4, 2026에 액세스, [https://wiki.play.eco/en/Laws](https://wiki.play.eco/en/Laws)  
25. Eco :: Developer Blog: Laws Part I \- Using the System \- Steam Community, 2월 4, 2026에 액세스, [https://steamcommunity.com/games/382310/announcements/detail/2384040944547213858?l=indonesian](https://steamcommunity.com/games/382310/announcements/detail/2384040944547213858?l=indonesian)  
26. Eco :: Developer Blog: Laws Part I \- Using the System \- Steam Community, 2월 4, 2026에 액세스, [https://steamcommunity.com/games/382310/announcements/detail/2384040944547213858](https://steamcommunity.com/games/382310/announcements/detail/2384040944547213858)  
27. Apocalyptic endgames & server resets in strategy MMOs : r/truegaming \- Reddit, 2월 4, 2026에 액세스, [https://www.reddit.com/r/truegaming/comments/2m815e/apocalyptic\_endgames\_server\_resets\_in\_strategy/](https://www.reddit.com/r/truegaming/comments/2m815e/apocalyptic_endgames_server_resets_in_strategy/)  
28. SpacetimeDB and BitCraft \- Clockwork Labs, 2월 4, 2026에 액세스, [https://clockwork-labs.medium.com/spacetimedb-and-bitcraft-bc957a7faf40](https://clockwork-labs.medium.com/spacetimedb-and-bitcraft-bc957a7faf40)  
29. My Childhood MMORPG Dream? SpacetimeDB Might Just Make It a Reality | by Martin Erlic, 2월 4, 2026에 액세스, [https://medium.com/@SeloSlav/my-childhood-mmorpg-dream-spacetimedb-might-just-make-it-a-reality-1e3f61d574d4](https://medium.com/@SeloSlav/my-childhood-mmorpg-dream-spacetimedb-might-just-make-it-a-reality-1e3f61d574d4)  
30. reducer in spacetimedb \- Rust \- Docs.rs, 2월 4, 2026에 액세스, [https://docs.rs/spacetimedb/latest/spacetimedb/attr.reducer.html](https://docs.rs/spacetimedb/latest/spacetimedb/attr.reducer.html)  
31. 3 \- Gameplay | SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/tutorials/unreal/part-3/](https://spacetimedb.com/docs/tutorials/unreal/part-3/)  
32. Understanding Recursive SQL for Hierarchical Data Structures | by Igor Plotnikov \- Medium, 2월 4, 2026에 액세스, [https://medium.com/learning-sql/understanding-recursive-sql-for-hierarchical-data-structures-76e3ac29c693](https://medium.com/learning-sql/understanding-recursive-sql-for-hierarchical-data-structures-76e3ac29c693)  
33. Row Level Security | SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/rls](https://spacetimedb.com/docs/rls)  
34. Row Level Security (RLS) \- SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/rls/](https://spacetimedb.com/docs/rls/)  
35. Griefing and social engineering policies \- Starbase Forum, 2월 4, 2026에 액세스, [https://forum.starbasegame.com/threads/griefing-and-social-engineering-policies.1520/](https://forum.starbasegame.com/threads/griefing-and-social-engineering-policies.1520/)  
36. Tutorials/Griefing prevention \- Minecraft Wiki \- Fandom, 2월 4, 2026에 액세스, [https://minecraft.fandom.com/wiki/Tutorials/Griefing\_prevention](https://minecraft.fandom.com/wiki/Tutorials/Griefing_prevention)  
37. Security status \- EVE University Wiki, 2월 4, 2026에 액세스, [https://wiki.eveuniversity.org/Security\_status](https://wiki.eveuniversity.org/Security_status)  
38. The Database Module | SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/databases](https://spacetimedb.com/docs/databases)  
39. Incremental Migrations | SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/how-to/incremental-migrations/](https://spacetimedb.com/docs/how-to/incremental-migrations/)  
40. Inflation: The long death of MMOs \- Skycandy, 2월 4, 2026에 액세스, [http://skycandy.org/2011/04/04/inflation-the-long-death-of-mmos/](http://skycandy.org/2011/04/04/inflation-the-long-death-of-mmos/)  
41. What is Multi-signature? Multi-sig Wallets in Crypto Explained \- OSL, 2월 4, 2026에 액세스, [https://www.osl.com/hk-en/academy/article/what-is-multi-signature-multi-sig-wallets-in-crypto-explained](https://www.osl.com/hk-en/academy/article/what-is-multi-signature-multi-sig-wallets-in-crypto-explained)  
42. Multisig Wallets: Complete Guide 2024 \- Krayon Digital, 2월 4, 2026에 액세스, [https://www.krayondigital.com/blog/multisig-wallets-complete-guide-2024](https://www.krayondigital.com/blog/multisig-wallets-complete-guide-2024)  
43. Rust Quickstart | SpacetimeDB docs, 2월 4, 2026에 액세스, [https://spacetimedb.com/docs/quickstarts/rust/](https://spacetimedb.com/docs/quickstarts/rust/)  
44. Fast, Secure, Language-Agnostic Policy Engine Using WASM \- Hacker News, 2월 4, 2026에 액세스, [https://news.ycombinator.com/item?id=45436843](https://news.ycombinator.com/item?id=45436843)