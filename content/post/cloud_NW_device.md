---
author: "LaMelD"
title: "[CLOUD] Network Device"
date: 2020-01-06T09:34:37+09:00
tags : [
	study_network
]
categories : [
	study_network
]
linktitle: Network Device
---

# 네트워크 장비
### 200106 Monday ~ 200110 Friday

berryz web share ip :: http://192.168.0.100 (사설 IP)  
berryz web share ip :: http://121.140.73.126 (공인 IP)  
복습 :: http://www.ddarahakit.kro.kr

-----

## 1. 계층별 장비와 케이블
- 계층 별 장비
    - Physical Layer --> Repeater, Hub
    - Data link Layer --> Switch, Bridge
    - Network Layer --> Router, L3 Switch  

- Physical Layer :: Repeater
    - 전기 신호 증폭
    - cable 전송으로 약화된 신호를 초기화, 증폭, 재전송의 기능을 수행
    - 상위 계층에서 사용하는 MAC 주소나 IP주소를 이해하지 못하고 단지 전기 신호만을 증폭시키는 역할을 한다.
- Physical Layer :: Hub
    - 무조건 모두에게 전달
    - 전기적 신호를 증폭
    - LAN 전송거리를 연장시키고 여러 대의 장비를 LAN에 접속할 수 있도록 한다.(멀티 포트 리피터)
    - 충돌 문제가 발생할 수 있다.  

- Data link Layer :: Bridge
    - 브릿지, 스위치도 허브와 마찬가지로 Ethernet 장비를 물리적으로 연결하고 Frame의 전송거리를 연장
    - 단순히 전기적 신호만을 증폭시키는 것이 아니라 Frame을 다시 만들어서 전송
    - 허브와 달리 Layer 2 주소인 MAC 주소를 보고 Frame 전송 포트를 결정
- Data link Layer :: Switch
    - 여러 기능이 추가됨
    - 브릿지와 스위치는 MAC 주소와 해당 장비의 포트번호가 기록된 MAC 주소 table을 보고 목적지에게만 Frame을 전송
    - 스위치는 한 포트에서 전송되는 Frame이 MAC 주소 table에 있는 특정 포트로만 전송하기 때문에 다른 포트가 전송하는 Frame과 충돌이 발생하지 않는다.
    - 즉, 스위치는 각각의 포트가 하나의 Collision domain에 있다고 표현한다.  

- Networ Layer :: Router
    - 다른 네트워크를 연결하는
    - 라우터와 L3 스위치는 IP주소 등 Layer 3 header에 있는 주소를 참조하여 목적지와 연결되는 포트로 packet을 전송
    - 따라서 라우터와 L3 스위치를 3계층 장비라고 한다.
    - 다른 네트워크(LAN) 구간의 장비와 통신을 하려면 반드시 3계층 장비를 거쳐야 한다.
    - 라우터는 특정 인터페이스를 통하여 수신한 packet의 목적지 IP 주소를 보고 목적지와 연결된 인터페이스를 통하여 전송할 것을 결정
    - 이를 라우팅(Routing)이라고 한다.
    - 라우터의 기본 기능은 경로 결정, 경로에 따른 packet 전송이다.
    - 스위치는 멀티캐스트, 브로드캐스트, 목적지를 모르는 유니캐스트를 수신할 경우 수신 포트를 제외한 모든 포트로 flooding.
    - L3 장비들은 이런 Frame을 모두 차단(즉, 브로드캐스트 전송을 막는다.)

- 통신 케이블
    - UTP, STP, Coaxial(동축), Fiber-Optic(광)
    - straight-through cable : 2계층과 3계층 연결할 때
    - crossover cable : 같은 계층 연결
        
        ![IMAGE](/images/net_device_1/UTP.PNG)

## 2. 3계층 장비 라우터 :: PDF를 다시 봐볼 필요가 있다.....ㅜㅜ
- 라우터란?
    - 서로 다른 Network를 연결하고 Broadcast Domain을 나눈다
    - 경로결정 : packet이 목적지로 갈 수 있는 경로를 확인하고 어느 경로가 가장 최적 경로인지 결정
    - Routing protocol에 따라 Routing table을 작성한다
- 라우터의 구성
    - Power supply, Flash SIMM, Boot ROM, RAM DIMMs, CPU --> PC와 비슷함
- 라우터의 부팅 과정
    - Power on self test (POST)
    - Load and run bootstrap code
    - Find the IOS software
    - Load the IOS software
    - Find the configuration
    - Load the configuration
    - Run
- 라우터의 설정은 PDF를 참고한다.
- 라우터의 여러가지 모드(CISCO 라우터)
    - ROMMON Mode
    - Setup Mode
    - User Mode
    - Privileged Mode
    - Global Configuration Mode

- ROMMON 모드
    - 복구 모드라고 생각하면 됨
- Setup 모드
    - Router 설정 파일이 없을 때 초기 설정을 도와주는 모드
- User 모드
    - 부팅에 성공했을 때 실행되는 모드
    - Router>
- Privileged 모드(GNS에서는 바로 진입)
    - 설정 확인 모드
    - 관리자 모드
    - Router#
- Global Configuration 모드
    - 설정하는 모드
    - configuration 모드
    - Router(config)#

## 3. 라우팅 프로토콜

- 라우터의 역할
    - show ip route : privileged 모드에서 확인
    - 목적지 네트워크와 해당 네트워크로 가기 위해서 어느 경로로 나가야 하는지의 정보를 가지고 있다.
    - Router가 Packet을 목적지로 보내기 위해서는 이럲게 Routing table을 참조한다
    - Best path만을 Routing table에 올린다
    - 즉, Routing table이란 어떤 목적지로 가기 위해서 어떤 경로로 가야 하는지 알 수 있는 네트워크 지도
- 라우팅 프로토콜
    - 목적지 네트워크로 가는 경로를 알아내기 위해 사용하는 Protocol
- 라우터는 기본적으로 자신과 연결된 네트워크 정보만을 라우팅 테이블에 가지고 있다
- 때문에 라우팅 프로토콜을 사용해서 직접 연결되지 않은 네트워크의 정보를 라우팅 테이블에 추가시킨다
    - 즉, 라우팅 프로토콜이 설정되지 않으면 자신과 직접 연결된 주소만 라우팅 테이블에 보인다.
- 각 라우터는 서로의 주소를 알아야 통신이 가능


- 정적 라우팅 프로토콜
    - 기본 라우팅 설정
- 동적 라우팅 프로토콜
    - RIP
    - ...
    - ...

## 4. 동적 라우팅 프로토콜 - RIP

- RIP : 라우터의 개수가 적은 경로를 최적의 경로로 설정한다. Distance Vector Routing Protocol
- Routing table의 교환 : 각 라우터는 30sec 마다 공유한다.
- V1 과 V2
    - V1 : Classful만 지원한다.
    - V2 : Classless도 지원한다.
- UDP 포트 520번을 사용한다.
- AD 값(가중치?낮은 값일 수록 좋다....우선순위) : 120
    - 직접 연결은 AD값이 0으로 설정됨
    - static으로 설정한다면 ad값이 낮아지며 우선순위가 높아진다.(1로 설정됨)
- 장점
    - 설정이 간단하며, 표준 Routing Protocol이므로 모든 회사의 Router에 사용 가능
    - 작은 규모의 네트워크나 대형 네트워크의 말단 지점에서 사용하기 유리하다.
- 단점
    - Hop-count로 경로를 판단하기에 느린 경로를 선택할 수 있다.
    - 최대 Hop-count가 15이기 때문에 대형 네트워크에 사용이 불가능하다.
    - 아무 조건 없이 30sec마다 패킷을 교환하기 때문에 비효율적이다.
    - Convergence Time(수렴 시간)이 30sec로 길다.
        - 수렴 시간이란?
            - 네트워크에 변화가 생길 경우 모든 라우터가 네트워크 변화 상태에 대해 정확하고 일관된 정보를 유지하는 것
            - 네트워크에 변화가 생겼을 경우 그 변화된 정보를 서로 인식하고 수정하는 시간
            - 짧을 수록 좋다.
- 문제점
    - 잘못된 정보를 공유할 수 있다.
    - 연결이 끊어졌다는 사실을 알기위해 약 7분이 걸린다. -> 15 Hop-count 까지 도달한 뒤 올바른 정보를 공유할 수 있다.
- 해결책
    - A로부터 받은 정보는 A에게 전달하지 않는다.
    - 장애가 발생하면 메트릭 값을 16(infinity)로 설정
    - 일전시간 정보를 못 받으면 삭제(Hold-down Timer)
    - 네트워크에 변화가 생겼을 때만 광고(패킷)를 보낸다(Triggered Update)


>
```
라우터(CISCO)
a. interface에 연결된 부분 ip 설정
configure terminal
    interface fastEthernet [물리적 포트 번호: 0/0]
        ip address [설정 ip] [서브넷 마스크]
        no shutdown
        exit
    exit

b. Router 설정(static 설정)
configure terminal
    ip route [target 네트워크 대역] [target 서브넷 마스크] [목적지 :: 게이트웨이가 될 곳]
    exit

c. RIP 프로토콜 설정
configure terminal
    router rip
        version 2
        no auto-summary
        network [알고 있는 네트워크 대역]
```