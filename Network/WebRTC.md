# WebRTC

> [High Performance Browser Networking](https://hpbn.co/)의 [18. WebRTC](https://hpbn.co/webrtc/)를 번역하며 정리한 문서입니다.

> 내용 오류나 논리적 비약이 있을 수 있으니 참고하시고 있다면 이슈 등록 부탁드립니다.

> 또한 2019년 6월 27일 기준 완성되지 않은 작성중인 문서입니다.


## Introduction

- **WebRTC**(Real-Time Communication): 브라우저 간 `peer-to-peer` 오디오, 비디오, 데이터 실시간 통신을 가능하게 하는 표준, 프로토콜, Javascript API의 집합

- **MediaStream**: 오디오, 비디오 스트림의 취득물(acquisition)

- **RTCPeerConnection**: 오디오, 비디오 데이터의 통신

- **RTCDataChannel**: 임의의 응용 데이터(arbitrary application data) 통신

- WebRTC는 `UDP` 기반, 그러나 UDP는 시작점(starting point)일 뿐 실시간 통신을 위해 더 많은 것들이 필요

## Standard and Development of WebRTC

- WebRTC Architecture은 응용 프로그램 및 브라우저 API뿐만 아니라 `프로토콜 및 데이터 형식`을 포함하는 수십 가지 표준으로 구성

- VOIP(voice over IP), PSTN(public switched telephone network) 등 기존 통신 시스템과 통합 가능

## Audio and Video Engines

- 실시간 통신을 위해서는 
  
  - 오디오, 비디오 스트림은 품질을 향상시키기 위해 처리되어야 하고
  
  - 동기화(synchronized)되어야 하며
  
  - `출력 비트 전송률은 클라이언트들 사이에서 지속적으로 변화하는 대역폭(bandwidth)과 지연 시간(latency)에 맞춰 조정`되어야 함
  
- 수신할 때는, 스트림을 `실시간으로 디코딩하고 네트워크 지터(jitter) 및 지연 시간에 맞게 조정`할 수 있어야 함

- WebRTC는 `오디오, 비디오 엔진`을 브라우저에 제공

    - Video codec
    
    - Jitter/packet loss concealment
    
    - Synchronization
    
    - Image enhancement

### Acquiring Audio and Video with getUserMedia

- **MediaStream**: 오디오, 비디오 스트림의 취득물(acquisition)

    - MediaStream 객체는 한개 이상의 MediaStreamTrack으로 구성
    
    - MediaStream 객체 안의 Track들은 서로 동기화(synchronized)
    
    - MediaStream의 output은 `후처리를 위한 Javascript 코드, 원격 피어(remote peer)` 등에 보내질 수 있음
    
- `getUserMedia()`를 통해 응용 프로그램의 요구에 맞는 필수(mandatory), 선택(optional) `제약 조건(constraints)을 지정`하여 MediaStream을 요청

- WebRTC의 오디오, 비디오 엔진에 의해 MediaStream은 `자동으로 최적화, 인코딩, 디코딩` 된 후 라우팅

## Real-Time Network Transports

- 오디오, 비디오의 실시간 통신은 간헐적(intermittent) `패킷 손실을 견디도록(tolerate)` 디자인(`timeliness over reliability`)

    - 코덱이 출력 품질에 영향을 최소화 하며 데이터 간격을 채울 수 있음
    
- WebRTC는 `transport layer로 UDP` 사용

    - No guarantee of message delivery
    
    - No guarantee of order of delivery
    
    - No connection state tracking
    
    - No congestion control
    
- UDP는 실시간 통신의 기초일 뿐 WebRTC의 요구사항 만족을 위해서는 추가적인 프로토콜, 서비스 필요

    - ICE: Interactive Connectivity Establishment
    - STUN: Session Traversal Utilities for NAT
    - TURN: Traversal Using Relays around NAT
    - SDP: Session Description Protocol
    - DTLS: Datagram Transport Layer Security
    - SCTP: Stream Control Transport Protocol
    - SRTP: Secure Real-Time Transport Protocol
    
    - ICE, STUN, TURN: UDP를 통한 `peer-to-peer` 연결을 설정하고 유지
    
        - 사설망에 위치한 STUN 클라이언트는 인터넷망에 위치한 `STUN 서버에 공인 IP 주소와 포트를 요청`
        
            - 공인 IP주소와 포트로 NAT 라우팅 항목(routing entries)을 설정하여 공인 IP와 포트로 전달된 패킷이 사설망의 호스트 어플리케이션으로 돌아 갈 수 있음
        
        - STUN이 실패한다면, TURN 프로토콜을 대비책으로
        
            - `TURN 서버(릴레이 서버)`에 의존하여 peer 간 데이터를 중개
            
            - 이 경우, peer-to-peer 연결이 더 이상 아니라는 단점
            
        - ICE 프로토콜은 두 클라이언트가 `서로 통신할 수 있는 최적의 경로`를 찾을 수 있도록
        
            - Direct Connect → STUN → TURN  순서로 시도
            
    - DTLS: 통신되는 모든 데이터를 보안
    
    - SCTP. SRTP: 서로 다른 스트림 다중화(multiplex), 혼잡 및 흐름 제어
    
    - SDP: peer-to-peer 연결의 `매개변수를 negotiate`하는데 사용되는 데이터 포맷, 대역 외 통신으로 프로토콜 다이어그램에서는 제외

### Brief Introduction to RTCPeerConnection API

- **RTCPeerConnection**: `peer-to-peer 연결의 라이프 사이클`을 관리하는 인터페이스

    - `NAT traversal을 위한 ICE workflow` 관리
    
    - peer 간 자동 (STUN) keepalives 전송(The STUN protocol defines a simple mechanism  for keepalives pings to keep the NAT routing entries from timing out)
    
    - 연결 Offer 생성, Answer 수락, 상태에 대한 연결을 query 할 수 있는 API 제공

## Establishing a Peer-to-Peer Connection

- WebRTC peer은 `서로 다른 private network에 존재`하므로, 서로 직접 연결이 불가능

- 세션을 시작하기 위해서는

    - 연결 가능한 IP와 port를 수집하고
    
    - NAT traversal 후
    
    - Connectivity check
    
- peer-to-peer 연결에서는 상대방이 항상 새로운 연결을 듣고(listen)있다는 보장이 없음

- 성공적인 peer-to-peer 연결을 위해 풀어야 하는 문제들

    - 다른 peer가 peer-to-peer `연결을 열어(open)` 패킷을 받을 수 있도록 `알려줘야(notify) 함`

    → Signaling

    - peer-to-peer 연결의 `잠재적 라우팅 경로를 식별`(identify)하고 이 정보를 peer 간 `공유`해야 함

    → WebRTC의 built-in ICE 프로토콜에 의해 해결

    - 프토토콜, 인코딩 방식 등 `매개 변수 관련 정보를 교환`해야 함

    → Session Negotiation

### Signaling and Session Negotiation

- Connectivity check나 Session Negotiation 전 다른 peer가 현재 연결을 원하는지를 파악해야 함

    - `Signaling Channel` 이용(Offer and Answer)
    
- Signaling 프로토콜에 대한 권고(recommendation)이 없으므로 상호 운용(interoperability) 가능

    - Session Initiation Protocol(SIP), Jingle, ISDN User Part(ISUP) 등
    
    - 기존 Signaling 프로토콜과 게이트웨이를 사용해 기존 통신 시스템과 negotiation 가능, `다른 peer에게 Offer을 전달하고 Answer을 다시 라우팅`하는 것은 네트워크의 책임
    
    - Custom Signaling 프로토콜과 게이트웨이를 사용해 자기만의 Signaling Service 구현 가능, 두 peer가 `동일한 Signaling Service에 연결되어 있다면 서로 통신 가능`(ex. Skype)

- peer 간 Signaling Channel 공유가 완료되면, WebRTC는 `SDP(Session Description Protocol)를 사용해 peer-to-peer 연결의 매개변수`를 표현(description)

    - SDP는 Media가 아닌 `peer-to-peer 연결의 특성`들을 표현
    
        - Media Type(오디오, 비디오 등)
        
        - Network Transport
        
        - Codec
        
        - Bandwidth
        
        - Metadata...
        
    - `createOffer()`을 통해 `SDP description 생성`
    
    - Signaling Channel을 통해 SDP description을 교환하고 `setLocalDescription(), setRemoteDescription()`을 통해 `peer-to-peer 연결의 매개변수 negotiate`

### Interactive Connectivity Establishment(ICE)

- 동일 네트워크에 방화벽, NAT 기기가 없는 경우

    - 각 peer은 단순히 OS에 IP 주소를 쿼리하여 SDP에 추가하고 이를 교환하여 peer-to-peer 연결 가능
    
- 서로 다른 네트워크인 경우

    - peer 간 `public routing path`가 필요
    
    - RTCPeerConnection은 `ICE agent`를 포함하고 있음. ICE agent는
    
        - candidate IP 수집
        
            1. `OS에 local IP` 주소 쿼리
            
            2. `STUN 서버`에 쿼리하여 `공인 IP` 및 포트 검색
            
            3. `TURN 서버`를 통해 데이터 중개
            
            - 새로운 candidate IP가 발견될 때 마다, `RTCPeerConnection에 등록`하고 onicecandidate 콜백을 호출해 어플리케이션에 알림
            
            - RTCPeerConnection에 등록 후, `SDP Offer을 생성하고 Signaling Channel을 통해 다른 peer로 전송`
            
            - 다른 peer가 SDP Offer를 수신하면, 수신한 `candidate IP가 포함된 description을 setRemoteDescription()`
        
        - peer 간 Connectivity check
        
            - setRemoteDescription() 후, ICE agent는 STUN 바인딩 요청을 보내고, 다른 peer는 STUN 응답으로 확인
            
                - 성공 시, `peer-to-peer 연결을 위한 라우팅 경로 식별`
                
                - 실패 시, TURN 서버로 중개
                
        - Connection keepalives 전송
        
            - ICE agent는 정기적으로 다른 peer에게 STUN 바인딩을 요청
