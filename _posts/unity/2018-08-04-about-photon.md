---
layout: post
title:  "Unity3D Photon Server"
date:   2018-08-04
desc: "Unity3d의 UI를 담당하는 Canvas에 대해서 알아보자."
keywords: "Unity, Canvas, EventSystem, Rect Transform, Anchor, Component"
categories: [Unity]
comments: true
tags: [Unity, Canvas, EventSystem, Rect Transform, Anchor, Component]
icon: icon-html
---

최종 수정일 : 2018-08-04

# _Photon Server_

 이번에 작성할 내용은 unity 클라이언트와 연동해서 사용할 'Photon' 이라는 상용 네트워크 서비스 엔진입니다. Unreal Engine과도 연동이 되는 것으로 알고 있지만, 제가 사용할 곳은 Unity이기 때문에 그에 맞게 스터디 해볼 예정입니다. 이번에 회사에서 포톤 서버를 사용할 일이 생겨서 스터디하면서 기본 개념에 대해 정리해보고자 합니다.
기본 개념은 대체로 포톤 공식 홈페이지에 적혀있는 내용을 기반으로 작성되었으며, 번역이 이상할 수도 있으니 틀린점 있으면 댓글로 알려주시면 수정하겠습니다. 클라이언트 개발자로서 서버에 대한 이해도가 많이 낮은 상태에서 작성된 점 양해부탁드립니다.
 추가적인 부분은 지속적으로 수정해가며 업데이트할 예정입니다. 감사합니다.

###작업 환경
 - Windows 10
 - Unity 2018.1.5f1
 - Visual Studio 10 / ATOM
 - Photon-OnPremise-Server-SDK_v4-0-29-11263 

## 환경 구축 순서
1. Windows10 IIS 설치
2. Photon SDK 설치
3. 포톤sdk설치폴더\deploy\bin_Win64\PhotonControl.exe 실행
4. Visual Studio에서 콘솔 응용프로그램 프로젝트를 생성한다.
5. 생성한 프로젝트에서 프로젝트(P) 탭의 “생성한 프로젝트이름” 속성 페이지로 들어간다.
6. 응용 프로그램 탭에서 대상 프레임 워크를 .NET Framework로 맞추고, 출력 형식을 클래스 라이브러리로 설정한다.
7. 프로젝트의 참조에 Photon에 관련된 dll 파일들을 Import 시킨다.
8. 참조할 dll 파일은 Photon SDK를 설치한 폴더의 lib 폴더 안에 보면 준비되있다.
9. Logging.Log4Net / SocketServer / PhotonHostRuntimeInterfaces / Libs 등등
10. PhotonSDK폴더\deploy\ 에 내가 생성한 서버 프로젝트 이름의 폴더를 새로 생성 한후, 그 안에 bin 폴더를 생성한다.
11. 서버 로직을 구현한 후, 서버 프로젝트를 빌드한 후 생긴 파일들을 ‘h’에서 생성한 bin 폴더 안에 넣는다.
12. PhotonSDK폴더\deploy\bin_Win64 폴더 안에 있는 PhotonServer.config를 편집기로 실행해서,  Configuration 태그 안에 예제 프로젝트를 입력한 것과 동일한 방식으로 내 프로젝트에 맞게 값을 입력한다.
13. PhotonControl을 재시작하면 config파일 안에 입력한 내 프로젝트가 생성되있는데, 거기서 install Service를 한 뒤에, start Service한다.
14. 이제 포톤 서버가 제대로 실행되고 있는 것이다.
<br />
## 환경 구축 순서(클라이언트)
1. 유니티의 File탭 -> Build Settings -> Player Settings -> Resolution and Presentation에 들어가서 Run In Background 옵션을 켜준다.
2. 프로젝트의 assets 폴더 안에 plugins 폴더를 만들어서 그 안에 PhotonSDK 폴더 안에 있는 Photon3Unity3D.dll 파일을 추가한다.
3. plugins 폴더를 추가할 경우, 이는 Unity에서 빌드할 때 사용되는 예약어로, 자동으로 dll 파일(네이티브 라이브러리)가 빌드에 포함될 것이다.
4. 이후, 서버와의 통신 관련해서는 Photon library를 using문에 추가한 후 사용하면 될 것.
<br />
## Photon Application 응용 프로그램
 - Application은 서버 쪽에서 실행하는 게임 로직이며, 게임 내 특화된 기능(RPC, Data Storing, DB, etc..)이 Photon Application에서 구현되는 것.
 - C# Base로 로직을 구현하게 되며, 실행할 경우 DLL 파일이 생성되어 Photon 소스를 중심으로 로딩 후 실행된다. Photon Core에서 설정 파일 Configuration files를 읽어오고, 로딩 시 초기화와 일부 응용프로그램 관련 매개 변수를 편집.
 - 일반적으로, 한 Application에서 하나의 게임 내 운영 로직 모두를 제공.
<br /> 
## Game Logic
 - 클라이언트와 서버간 상호 정보 전달 방법 및 기능에 관한 것으로, 조작/이벤트 및 서버 자체 또는 외부와의 연결에서 반드시 실행해야 할 관련 과정을 구현해난다.
 - SocketServer에 대한 정보로는 photon.Socketserver.dll에 정의되어 있어서 참고 가능하다.
<br /> 
## Operation
 - Photon에서의 Operation은 RPC 구조와 동일하기 때문에, 클라이언트에서 operation call로 그들 간의 통신 전달 기능을 이용할 수 있다.
 - 매개 변수 전송은 서버쪽 애플리케이션에서 HashTable(keys & values)를 통한 데이터를 정의해놓은 후, 클라이언트와 서버 간의 직렬화(Serialize), 전송(Transfer) 및 비직렬화(Deserialize)를 진행한다.
 - 매 Operation call마다 리턴값은 서버가 클라이언트에게 보내주는 단방향 통신을 사용할 때 제공합니다.
<br /> 
## Events
 - 클라이언트에게 보내는 Message Notification. 
 - 클라이언트에서도 이벤트를 자체 설계해서 서버에게 보낼 수 있다.
 - 일반적으로 Event가 생성 또는 발생 될 경우, 해당 이벤트를 수신하고 있는 모든 클라이언트에게 이벤트가 전달된다.
<br /> 
## Connections & Timeouts
 - Reliable-UDP(R-UDP, 개량형 UDP)를 사용한다.
 - Sender에서 송출한 R-UDP의 패킷 내 commands에 시리얼 번호 및 flag를 가지고 있으며, Receiver에서는 반드시 해당 신호에 등답해야한다.
 - 발송 지점 R-UDP는 단시간 내재발송이 진행되며, 상대방의 Response가 도착해야 중지된다.
 - Response를 수신하지 못할 경우, Timeout error message 생성
 - Timeout이 발생할 경우, 바로 해당 연결을 끊으며, 정보동기화가 발생하지 않습니다.
<br />
## MMO Application
 - Actors / Items / Properties / Events의 기본 유형으로 구성되어있습니다.
 - 구역은 World / Region / InterestArea / Item 으로 구분됩니다.
 <br /> 
## Peers
 - 서버와 연결한 사용자의 Instance
 - App에 연결한 클라이언트 네트워크가 있다면, CreatePeer는 그에 상응하는 Peer를 만들고, 해당 클라이언트에서 전해오는 Operations 모두 그에 상응하는 Peer에서 처리하게 된다.
 - App 내의 매 Peer 마다 상태 지시의 RoomReference가 존재한다.
 - Join Room을 할 때, 해당 상태 지시 기능이 생성된다.
 - Peer 연결이 끊어질 경우, OnDisconnect를 호출한다.
 - 서버와 통신할 클라이언트의 객체는 IPhotonPeerListener를 상속받아서 구현한다.
<br /> 
## OnEvent(EventData eventData)
 - 서버에서 Broadcast를 통해 클라에게 데이터를 전달할 경우, 클라이언트에서 호출되는 메소드. eventData는 서버에서 전달하는 데이터를 담고 있는 객체
<br /> 
## OnOperationResponse(OperationResponse operationResponse)
 - 서버에서 특정 클라에게 데이터를 전달할 경우, 클라이언트에서 호출되는 메소드. operationResponse는 서버에서 전달하는 데이터를 담고 있는 객체	
<br /> 
## OnStatusChanged(StatusCode statusCode)
 - 서버에서 상태가 변경될 때 호출되는 메소드.
 - Connect, Disconnect, Timeout, etc…
 <br /> 
## DebugReturn(DebugLevel level, string message)
 - 디버그 메시지를 리턴해주는 메소드.
<br /> 
## PhotonPeer 객체
 - PhotonPeer 클래스는 Photon Server와 연결하고, communicate 하는데 사용되는 클래스입니다.
 - 이는 Photon Server 뿐만 아니라, Server 내에 있는 또다른 PhotonPeer 클래스와 Communicate 하는데도 마찬가지입니다.
 - 한 어플리케이션에서 하나 이상의 PhotonPeer를 사용할 경우, 각각 다르게 event 또는 operation에 대한 요청/응답을 설정 할 수 있습니다.
<br /> 
## Rooms 
 - 한 Room 당 플레이어 수가 제한되어 있다.
 - Room에는 하나 이상의 Peer가 존재하게 되며, 그 안에서 함께 데이터를 주고받으면서 게임이 시작된다.
 - 일반적으로 룸 안에서 모든 사람은 다른 사람이 전송한 것을 수신한다.
 - 룸으로 플레이어를 접속하게 하는 방법은 무작위 매치메이킹 / 특정 Properties를 가진 룸에 플레이어를 접속하게 하는방법 두가지이다.
 - Room끼리(각각의 Game)는 서로 완벽하게 독립된다.
 - Room은 모두 고유 식별자로서 이름을 가지고 있다.
 - Request는 받은 순서대로 처리된다.
 - 각 Room마다 모두 Balacing이 존재해서 Request마다 매 tick마다 처리되기 때문에 거의 실시간에 가까운 처리가 진행되며, 이후 프레임 확장에 사용할 수 있다.
 - Room 내 사용자 모두 Actor로 표시되고, Actor마다 ActorNumber를 가지고 있어, Event를 전송할 때마다, 해당 값으로 발송자를 식별할 수 있다.
 - 마스터 서버는 App을 통해 Room의 목록을 제공해 줄 수 있다.
<br /> 
## Robby
 - 마스터 서버에 존재하며, 게임의 룸 목록을 제공한다.
 - 아직 룸에 참여하지 않은 플레이어들이 모여서, 룸에 접속하기 위해 대기하는 장소.
<br /> 
## HandleRaiseEvent
 - 서버에서도 필요에 따라 모든 이벤트를 전송할 수 있는 이벤트.
<br /> 
## Properties
 - HashTable을 대표하는 구조.
 - 사용자의 데이터 설정 및 inout 작업에 용이함.
 - 보통 Actor 또는 Room에 추가.
 - 룸 내 일부 데이터 및 사용자 이름 설정에 사용할 수 있고, 클라이언트 데이터 획득도 가능.
 - SetProperties / GetProperties 로 관련 데이터를 set/get할 수 있다.
 - Room에 Join할 때 기존에 설정한 Room Data를 덮어쓰기 하는데, 새로운 Room을 생성해 Join을 진행해야만 데이터를 설정할 수 있고, 이후에 Room에 Join한 사람이 하는 설정은 무효가 된다.
<br /> 
## Photon Plugin
 - 사용자 정의 서비스 로직을 추가하고 싶을 때, Photon Server에 정의해 놓은 인터페이스(Hook)에 Injection해줘야한다.
 - Photon Plugin마다 각각의 식별자가 있으며, Event에 상응하는 CallBack을 구현해야 한다.
<br /> 
## Photon Server Method
<br /> 
### Intercept the hook call
 - 콜백 발생 시, 호스트에서 통제권을 Plugin으로 보냄.
<br /> 
### Alter call info (Option)
 - 실제로 hook call을 실행하기 전에, 클라이언트/서버에서 송출하는 Request를 액세스하고 수정한다.
<br /> 
### Inject custom code (Option)
 - Hook call을 실행하기 전에 호스트와 일부 과정을 처리한다.
ex) HTTP Request, Look up room/actor Reference, Count 값 설정 etc..
<br /> 
### Process hook call
 - 실제로 해당 요청 처리 방법(장소)을 결정한다.
 - ICallInfo Processing Method 참조
<br /> 
### Inject custom code (Option)
 - 실행 후, 클라이언트/서버에서 송출한 요청이 Read Only로 변경됨.
 - 단, 처리 실행 후 플러그인은 여전히 호스트와 상호 작용한다.
<br /> 
### Return
 - 플러그인 통제권을 호스트에 반환