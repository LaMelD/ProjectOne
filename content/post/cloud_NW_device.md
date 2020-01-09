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

- RIP Protocol : 라우터의 개수가 적은 경로를 최적의 경로로 설정한다. Distance Vector Routing Protocol
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

## 5. 동적 라우팅 프로토콜 - EIGRP

- EIGRP Protocol
    - Cisco에서 만든 Cisco 전용 라우팅 프로토콜
    - Auto-summary 적용되어 있음
    - 라우팅 정보 전송을 위해 IP 프로토콜 88번 사용
    - IGRP가 발전된 라우팅 프로토콜
    - DUAL 알고리즘 사용하여 최적 경로와 후속 경로 산출
    - Convergen time이 빠르다
    - AD값은 내부가 90, 외부가 170
    - AS(Autonomous System) 단위로 구성
    - Classless Routing protocol
- 장점
    - 빠르다
    - 부하분산 지원(Unequal cost)
    - OSPF에 비해 설정이 간단하다
- 단점
    - Cisco 전용 Routing protocol이기에 Cisco router에서만 동작
    - 대규모 네트워크 구성은 힘들다(라우팅 테이블이 매우 커짐)

- EIGRP Packet : 이웃을 맺고 라우팅 정보를 교환한다.
    - Hello packet
    - Update packet
    - Query packet
    - Reply packet
    - ACK(Acknowledgement) packet

- 라우팅 경로 계산 절차
    - Hello packet을 인접 Router가 서로 교환 한 후 Neighbor 관계를 맺고 Neighbor table을 생성한다.
    - Update packet을 통해 라우팅 정보를 교환하고 Topology table을 생성한다.
    - Topology table 정보를 종합해서 라우팅 경로를 계산하고 Best path를 Routing table에 저장한다.

- 특정 네트워크로 가는 경로 또는 인접 Router가 다운되었을 때
    1. 
    2. 
    3. ㅁㅁ  
    ㅁ0000ㄻ

- EIGRP 메트릭
    - 
    - 
    - 

- DUAL 알고리즘
    - 메트릭을 구하고
    - FD값을 구하고 가장 낮은 경로가 최적경로로 선출
    - 남아있는 경로 중 AD 값이 FD값보다 작은 경우 후속 경로로 선출


## 6. 동적 라우팅 프로토콜 - OSPF // 정리가 필요하다.

- OSPF Protocol
    - Link-state 라우팅 프로토콜
    - Classless 라우팅 프로토콜
    - Metric(메트릭) cost 사용
    - Multicast를 사용하여 정보 전달
    - AD값 : 110
    - SPF(Shortest path First) 또는 Dijkstra 알고리즘 이용(경로 계산)

- 장점
    - area 단위로 구성 --> 대규모 네트워크를 안정적으로 운영 가능
        - 
    - Stub이라는 강력한 축양 기능이 있다.....
        - 
    - 표준 Routing Protocol
    - Convergence time이 전반적으로 빠른 편이다.

- 단점
    - 설정이 복잡하다
        - 네트워크 종류에 따라 동작하는 방식과 설정이 다르다.
    - 네트워크의 종류
        - Broadcast Multi Access
        - Point-to-point
        - Point-to-Multipoint
        - Non Broadcast Multi Access
    
    - Broadcast Multi Access

    - Non Broadcast Multi Access

    - Point-to-point

    - Point-to-Multipoint(찾아보자)

- Packet
    - Hello packet
        - 내용
    - DBD packet
        - 내용
    - LSR packet
        - 내용
    - LSR packet
        - 내용
    - LSU packet
        - 내용
    - LSAck packet
        - 내용

- 과정
    1. OSPF를 설정한 Router끼리 Hello packet을 교환해서 Neighbor 혹은 adjancent Neighbor를 맺는다
        - adjancent Neighbor --> 라우팅 정보(LSA:Link State Advertisement)를 교환하는 네이버
    2. adjancent 네이버인 Router간 라우팅 정보를 서로 교환. 전송 받은 LSA를 Link-State-DB에 저장
    3. LSA를 모두 교환하고 SPF 또는 다익스트라 알고리즘을 이용하여 각 목적지까지의 최적 경로를 계산 후 Routing table에 올린다.
    4. 네트워크의 상태가 변하면 다시 위의 과정을 반복해서 Routing table을 생성

>명령어
```
vmware 설명
1. bridged
	Host PC의 네트워크 대역이랑 같은 네트워크 대역을 사용하는 가상의 네트워크 장치

2. host-only
	host PC랑만 연결된 가상의 네트워크 장치
	host PC의 가상의 랜카드와 연결됨 --> guest(가상 머신)이 host와 연결은 되지만 인터넷에는 연결 안됨
	GNS3를 이용해서 외부랑 연결 가능
	
3. NAT
	host PC의 IP를 공인 IP로 사용하는 사설 네트워크 대역을 만드는 가상의 네트워크 장치
	
	
	
conf t
int fa 0/0
ip addr 10.10.10.2 255.255.255.0
no sh
end



0.0.0.0 알고 있는것 이외의 모든 IP --> 지정된 게이트웨이로 나간다(설정)
127.0.0.0 자기 자신


라우팅 default 설정

conf t
ip route 0.0.0.0 0.0.0.0 게이트웨이IP



----------------------------------------------------------------------------------------------
명령어

<R1>

Router>enable                               -> 유저 모드에서 프리빌리지 모드로 들어간다. (단축키 en)

Router#configure terminal                   -> 프리빌리지 모드에서 글로벌 컨피그 모드로 들어간다. (단축키 conf t)

Router(config)#hostname R1                  -> 라우터 이름 R1으로 변경


R1(config)#no ip domain-lookup              -> 명령어를 잘못 입력하면 라우터는 Domain name으로 인식하고 다른 라우터에게
                                                                  브로드캐스트를 뿌려서 찾기때문에 한동안 명령어 입력을 못한다.
                                                                 이를 방지하기 위한 명령어 

R1(config)#line con 0                                  -> 콘솔 라인 모드로 들어간다.
R1(config-line)#exec-timeout 0 0               -> 콘솔 라인은 일정시간이 지나면 끊어지는데 이를 방지한다. 
R1(config-line)#logging synchronous          -> 명령어 입력중 로그메시지가 뜰 경우 명령어와 겹쳐져 확인하기가 힘들다. 이를 방지한다. 
R1(config-line)#exit                                   -> 글로벌 컨피그 모드로 나온다. 
                 

R1(config)#enable password ccna             -> 유저 모드에서 프리빌리지 모드에 들어갈때 사용되는 암호 (인크립션 X)
                                                                 (no service password-encryption이 디폴트 설정이기 때문에 인크립션이 안된다.              
                                                                  service password-encryption 명령어를 치면 password도 인크립션 된다.
                                                                 다시 no service password-encryption을 쳐도 인크립션이 풀리지 않는다.)


R1(config)#enable secret cisco              -> 유저모드에서 프리빌리지 모드에 들어갈때 사용되는 암호 (인크립션 된다.)
                                                               (password와 동시에 있을 경우 secret이 password를 대신한다. 즉, 우선순위)

R1(config)#interface FastEthernet0/0                             -> 인터페이스 모드로 들어간다. 
R1(config-if)#ip address 192.10.5.254 255.255.255.0    -> 이더넷 구간 IP 할당
R1(config-if)#no shutdown                                                  -> 인터페이스는 항상 열어줘야 한다.
R1(config-if)#exit                                                   -> 다시 글로벌 컨피그 모드로 나온다.

R1(config)#interface Serial0/0                         -> 인터페이스 모드로 들어간다.
R1(config-if)#ip address 201.100.10.1 255.255.255.0    -> 시리얼 인터페이스 IP할당
R1(config-if)#no shutdown                                  -> 인터페이스는 항상 열어줘야 한다.
R1(config-if)#exit                                          -> 다시 글로벌 컨피그 모드로 나온다.

R1(config)#line vty 0 4                                -> virtual terminal 라인 모드로 들어간다. 
R1(config-line)#password ccna                          -> password 설정
R1(config-line)#login                                  -> 외부에서 telnet 접속시 password 확인한다. (디폴트 설정)
R1(config-line)#exit                                   -> 다시 글로벌 컨피그 모드로 나온다.


 => 지금까지의 설정한 내용은 RAM에 running-config로 올라가 있다. 
    전원이 꺼지거나 재부팅 될 경우 자동으로 삭제된다. (램은 휘발성 메모리이기 때문에)
    때문에 설정한 내용을 저장하기 위해서는 NVRAM에 있는 startup-config로 저장해야 한다.
    (NVRAM은 비휘발성 메모리이다. -> 전원이 꺼져도 내용이 저장돼 있다.)
    저장한 내용은 전원을 껐다가 다시킬 경우 혹은 재부팅을 할 경우 startup-config의 설정 내용이
    자동으로 RAM위로 내용을 올려서 설정한 내용이 유지가 된다.

R1#write (단축키 wr) 

혹은

R1#copy running-config startup-config (단축키 copy run start)

명령어로 설정한 내용을 NVRAM에 저장한다. (둘 다 같은 의미)

 * CCNA 시험 중 시뮬레이션 문제에서는 반드시 설정을 완료하고 저장해야 한다.
   저장 내용을 확인하는 명령어는 'R1#show startup-config' -> 즉, startup-config에 있는 내용을 확인한다. 



<R2>

Router>enable                                        -> 유저 모드에서 프리빌리지 모드로 들어간다. (단축키 en)

Router#configure terminal                            -> 프리빌리지 모드에서 글로벌 컨피그 모드로 들어간다. (단축키 conf t)

Router(config)#hostname R2                           -> 라우터 이름 R2으로 변경

R2(config)#no ip domain-lookup                       -> 명령어를 잘못 입력하면 라우터는 DNS로 인식하고 다른 라우터에게
                                                                           브로드캐스트를 뿌려서 찾기때문에 한동안 명령어 입력을 못한다.
                                                                          이를 방지하기 위한 명령어 

R2(config)#line con 0                                -> 콘솔 라인 모드로 들어간다.
R2(config-line)#exec-timeout 0 0                     -> 콘솔 라인은 일정시간이 지나면 끊어지는데 이를 방지한다. 
R2(config-line)#logging synchronous                  -> 명령어 입력중 로그메시지가 뜰 경우 명령어와 겹쳐져 확인하기가 힘들다. 이를 방지한다. 
R2(config-line)#exit                                 -> 글로벌 컨피그 모드로 나온다.
        
R2(config)#interface FastEthernet0/0                 -> 인터페이스 모드로 들어간다.
R2(config-if)#ip address 195.7.5.254 255.255.255.0   -> 이더넷 구간 IP 할당
R2(config-if)#no shutdown                                -> 인터페이스는 항상 열어줘야 한다.
R2(config-if)#exit                                   -> 다시 글로벌 컨피그 모드로 나온다.

R2(config)#interface Serial0/1
R2(config-if)#ip address 201.100.10.2 255.255.255.0
R2(config-if)#clock rate 64000                                -> 라우터끼리 연결되었을 경우 시리얼 케이블 중 DCE가 연결된 쪽은 반드시 
R2(config-if)#no shutdown                                           clock rate를 줘야한다. (clock rate ? 치면 입력가능한 값이 나온다.)
R2(config-if)#exit                                                        (디지털 데이터를 시그널로 정확히 인식하게 하기 위해서)
                                                                                   R2#show controllers s 0/1 -> DCE인지 DTE인지 확인 가능
                                                       
                                                          
R2(config)#line vty 0 4
R2(config-line)#password ccna
R2(config-line)#no login                             -> 외부에서 telnet 접속시 password를 확인하지 않고 바로 접속하게 한다.
R2(config-line)#exit













장치에 연결된 부분 ip 설정

configure terminal
	interface fa [물리적 포트 번호 : 0/0]
		ip address [설정ip] [서브넷 마스크]
		no shutdown
		exit
	exit



Route 설정(static 설정)

configure terminal
	ip route [target 네트워크 대역] [target 서브넷 마스크] [destination :: 현재의 게이트웨이가 될 곳]
	exit




RIP 프로토콜 설정

configure terminal
	router rip
		version 2
		no auto-summary
		network [알고 있는 네트워크 대역]


EIGRP 프로토콜 설정
	R1(config)#router eigrp <AS number> 		(1)  
	R1(config)#no auto-summary 			(2)
	
	R1(config)#eigrp router-id x.x.x.x 		(3) --------------> 일단 하지 않아도 됨...
	
	R1(config)#network x.x.x.x y.y.y.y		(4)

	(1) AS 번호를 지정한다.(1~65535), EIGRP로 동작하는 모든 라우터는 동일한 AS번호를 가져야 한다.

	(2) 자동 축약을 취소한다.

	(3) 라우터ID. 임의로 설정하지 않을 경우 루프백 인터페이스에서 가장 높은 IP주소가 설정  
		루프백 인터페이스가 없을 경우 물리적 인터페이스에서 가장 높은 IP주소가 설정 (관리용)  
		(설정을 안해도 EIGRP는 정상적으로 동작 (스스로 설정하니까))
		  
	(4) 인접한 네트워크 대역 광고
		y.y.y.y : 와일드카드 마스크 (서브넷 마스크의 not이라고 생각하면 된다)
		대역을 나누는게 아니다...?
		
		
		광고 할때 쓰인다 -> RIP와 비슷한 맥락.....
		여러개를 묶기 위해서.....
		
		
	메트릭 계산 시 필요한 값 -> router에서 show interface fastEthernet [인터페이스 번호] 입력 후 값 확인


라우터 secondary 설정
configure terminal
	interface loopbackc 0
		ip address [ip] [서브넷 마스크]
		ip address [ip] [서브넷 마스크] secondary
		ip address [ip] [서브넷 마스크] secondary
		ip address [ip] [서브넷 마스크] secondary
		no sh
		exit
	exit
		

확인 command
show running-config
show ip interface brief
show ip route
show ip eigrp neighbors
show ip eigrp topology


축약 -> 서브네팅의 역방향
162.10.0.1/22	->	162.10.0.0/22
162.10.1.1/22
162.10.2.1/22
162.10.3.1/22

162.10.4.1/22	->	162.10.4.0/22
162.10.5.1/22
162.10.6.1/22
162.10.7.1/22

162.10.8.1/22	->	162.10.8.0/22
162.10.9.1/22
162.10.10.1/22
162.10.11.1/22

162.10.12.1/22	->	162.10.12.0/22
162.10.13.1/22
162.10.14.1/22
162.10.15.1/22


configure terminal
	interface fastEthernet [interface 번호]
		ip summary-address eigrp [AS] [ip] [서브넷 마스크]


key 설정
configure terminal
	key chain [key 이름]
		key [id 번호]
			key-string [password]
			exit
		exit
	
	int fa 0/1
		ip authentication key-chain [라우팅 프로토콜] [키 이름]
		ip authentication mode [라우팅 프로토콜] md5
		exit



OSPF 데이터 베이스 보기
sh ip ospf database


OSPF 프로토콜의 설정
configure terminal
	router ospf 1
		router-id [ip-id]
		network [네트워크 대역] [와일드 카드] [Area number]


OSPF에서의 축약
	조건1. ABR 또는 ASBR에서만 축약이 가능하다.(경계상에 있는 라우터)
	조건2. 동일 area 장비에게는 축약된 정보를 전달할 수 없다.
	interface에서가 아닌 라우터 설정에서 축약을 실시한다.
		router ospf [number]
			area [축약하려는 구역의 number] range [ip] [축약]



Router 설정 저장
copy running-config startup-config


<<재분배>>
- ASBR에서 설정하기!! :: eigrp - ospf
- from과 to를 잘 생각해야 한다.
configure terminal
	//eigrp의 내용을 ospf로 재분배(전달/전환) 한다
	router ospf [pid]
		redistribute eigrp [AS number] 10 subnets
		exit
	
	//ospf의 내용을 eigrp로 재분배(전달/전환) 한다
	router eigrp [AS number]
		redistribute ospf [pid] metric [b/w] [dly] [reliability] [loading] [MTU] 
		exit

	//ospf의 내용을 rip로 재분배(전달/전환) 한다
	router rip
		redistribute ospf [pid] metric [Hop-count]
		exit

	//직접 연결된 내용을 rip로 재분배(전달/전환) 한다
	router ospf [pid]
		redistribute connected subnets
		exit
```


## 7. 라우터의 보안 기능 - ACL

![IMAGE](/images/net_device_1/ACL_ground.PNG)

- ACL 접근 제어 목록
    - 특정 트래픽의 접근을 허용할지 차단할지 결정하는 리스트(Filtering)
    - 보안을 위해 많이 사용
    - 3계층 장비인 Router에서 사용하지만 Application Layer부분도 관리하기 때문에 Network Layer 까지라고 단정할 수 없다.
    - 하지만 Application Layer까지 완벽히 막을 수 없기 때문에 Firewall(방화벽) 등의 전문적인 보안 장비를 사용
    - ACL은 크게 Numbered와 Named 두 종류가 있다. 그리고 다시 Standard(1~99)와 Extended(100~199)로 구분할 수 있다.(이외에도 여러가지가 있다.)

- 기본 ACL : 1번 ~ 99번
    - Standard ACL의 경우 source address를 보고 permit, deny 여부를 결정
    - packet의 source address와 ACL에 정의된 source address가 일치하면 ACL의 내용을 수행한다.
    - permit이면 packet을 정해진 경로로 전송하고 deny면 packet의 흐름을 차단

>기본 ACL 적용
```
configure terminal
    //생성
    access-list [number] [permit | deny] [네트워크 대역] [와일드카드]
    //적용
    interface [cable] [nubmer/number]
        ip access-group [access list number] [in | out]

ex) R2는 출발지가 10.10.10.0/24인 트래픽이 fa 0/1으로 들어오는 것을 차단
//생성
configure terminal
    access-list 1 deny 10.10.10.0 0.0.0.255
    access-list 1 permit any
    exit
//적용
configure terminal
    int fa 0/1
        ip access-group 1 in
```

- 확장 ACL
    - Standart ACL은 source address만 조건으로 보고 filtering을 수행한다. 하지만 extended ACL은 source address와 destination address 모두를 조건으로 보고 제어한다. 
    - 또한 standard ACL은 TCP/IP에 대해 제어만을 하지만 extended ACL은 ip, tcp, udp, icmp 등의 상세 프로토콜을 선택해서 설정할 수 있다.

>확장 ACL 설정
```
configure terminal
    access-list [list number] [permit | deny] [protocol] [source addr] [mask] [destination addr] [mask] ['eq' operator port]

ex)

```

- ACL 설정 방법
    - inbound :: 내부로 들어올 때 필터링
    - outbound :: 외부로 나갈 때 필터링
    
    - 순서 : 생성 --> 적용
    
    - ACL 규칙
        1. ACL은 윗줄부터 순서대로 수행한다.
        2. ACL의 마지막에는 deny any가 생략되어 있다.
        3. numbered ACL은 순서대로 입력되기 때무에 중간 삽입이나 삭제가 불가능하다.
            - 예외로 named ACL의 경우는 중간 삭제 및 추가 삽입이 가능하다.

>실습 자료
```
Standard ACL
    1. R2는 출발지가 10.10.10.0/24인 트래픽만 fa 0/1으로 들어오는 것을 차단하시오.
    2. R2는 출발지가 10.10.10.0/24인 트래픽이 fa 0/1으로 들어오는 것을 차단하시오.
    3. R1에서 출발지가 20.20.20.0/24인 트래픽이 fa 0/0으로 나가는 것을 차단하시오.
    4. R1에서 출발지가 10.10.10.56/24인 트래픽만 fa 0/0으로 나가는 것을 허용하시오.
        새롭게 패킷을 만들기 전에 ACL검사를 한다.
        목적지에 가까운 곳에 in을 막는 것으로 설정을 한다.
Extended ACL
    1. 
    2. 
    3. 
    5. 
```