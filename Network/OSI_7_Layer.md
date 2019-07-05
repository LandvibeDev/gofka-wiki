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
	- 
6. 6계층 : Presentation Layer
	-
7. 7계층 : Application Layer
	-  
![OSI_7_Layer](https://t1.daumcdn.net/cfile/tistory/99B9493359B6408E23)
* 
* ???
* ??
* ??????.
<hr/>
<hr/>
### This is H3
#### Written by Woogon