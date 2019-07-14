# OSI 7 Layer
1. 국제표준화기구(ISO)에서 개발한 모델
2. [표준]이므로 전세계적으로 네트워크 구성에 있어 참조되는 모델
3. 현재는 TCP/IP Protocl Suite (5 Layer or 4 Layer)를 더 많이 사용하는 추세
# OSI 7 Layer가 필요한 이유
1. 예전 네트워크 장비 업체들은 자신들의 업체 장비만 연결하여 통신을 할 수 있는 등 호환성이 부족
2. 이러한 문제를 해결하기 위해 국제단체에서 표준을 제정
3. 각 계층에 맞는 장비를 개발 후, 계층 간 통신을 위한 Interface만 일치시켜주면 호환성 문제 해결 가능
# 각 계층별 이름과 역할, 장비
1. 1계층 : Physical Layer
	- Hardware적인 매체를 통해 Bit를 전송
	- Cable (Copper / Optic)
2. 2계층 : Data-Link Layer
	- Hop to Hop Delivery를 담당 (즉, 한 장비에서 다른 장비로의 Frame 전송을 의미)
	- Bridge, Switch (MAC Address를 이용)
3. 3계층 : Network Layer
	- Packet을 목적지까지 최적의 경로로 전송하는 것을 담당
	- Router (IP Address를 이용)
4. 4계층 : Transport Layer
	- Segment의 전송 방식을 담당 (가장 대표적으로 신뢰성있게 전송하는 TCP, 그 반대인 UDP)
	- Load Balancer (Port를 이용)
5. 5계층 : Session Layer
	- Session을 담당하는 계층(?).. 잘 모르겠음
6. 6계층 : Presentation Layer
	- Data를 안전하게 전송하기 위해 암호/복호화 하는 작업 수행... 이라고 나와있는데 사실 잘 모르겠음
7. 7계층 : Application Layer
	- User가 직접 볼 수 있는 (최종 사용자에게 가장 가까운) 계층
![OSI_7_Layer](https://t1.daumcdn.net/cfile/tistory/99B9493359B6408E23)
* 최근에는 OSI 7 Layer가 아니라 TCP/IP 4 layer model로서 네트워크를 표현하는 경우가 훨씬 많음 (불필요한 계층 통합 및 제거)
# 각 계층에서 사용하는 주소
* Data-link layer에서 사용하는 MAC Address
	- 6byte로 구성 ex) AA:BB:CC:DD:EE:FF
	- 주로 NIC 카드에 고유하게 설정되어있고, 전세계에서 유일한 주소 (단, 중복되는 경우가 있기는 함)
	- MAC address를 보고 NIC 카드의 Vendor사를 알 수 있음
* Network layer에서 사용하는 IP Address
	- 4byte로 구성 ex) 172.23.35.12
	- Internet과 통신이 가능한 public IP, Internet과 통신이 불가능한 private IP 영역이 존재
	- Public IP는 전세계에서 유일한 주소, Private IP의 경우 중복 가능
	- 4byte(32bit)로 표현할 수 있는 IP의 개수는 약 43억개, 연구용/예약된 IP를 제외하면 훨씬 적은 수
	- 최근 IoT 기기의 보급 등으로 IP 주소가 모자라짐에 따라 128bit IPv6 주소로의 변환 얘기가 나오고 있지만 적극적이지는 않음
* Transport layer에서 사용하는 port number
	- 16bit로 구성 (0~65535)
	- 0~1023번 port의 경우 일반적으로 잘 알려진 (Well-Known) 포트 번호로 구성
	- 대표적으로 HTTP 80, HTTPS 443, SSH 22, DNS 53, FTP 20/21 등
	- 각 Service를 제공하기 위한 구분자라고 생각해도 될 듯
# Data의 Encapsulation 과정
![Data_Encapsulation](https://i.stack.imgur.com/Hi3zX.jpg)
# Sender와 Recevier측에서의 대략적인 전송과정
![Transmission](https://ccnabasics.files.wordpress.com/2012/12/122012_1626_osireferenc6.png?w=600)
<hr/>
<hr/>
#### Written by Woogon