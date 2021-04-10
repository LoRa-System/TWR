## [IPv6-over-LoRaWAN](https://github.com/aenrbes/IPv6-over-LoRaWAN) 설치

### 필요 장비

* HT-M01 Mini LoRa Gateway : https://heltec.org/project/ht-m01/ 
* LoRa Node 151 : https://heltec.org/project/lora-node-151/ 
* ST-LINK/V2(LoRa Node 컴퓨터 연결 디버깅 usb) : https://www.devicemart.co.kr/goods/view?no=27492 

### 이런 오픈소스들을 사용함

* Contiki-NG(https://github.com/contiki-ng/contiki-ng)
  * 네트워크 계층(layer 3). 즉, IPv6 프로토콜 및 그 위쪽 모든 계층에서 동작. enddevice 와 (gateway + networkserver) 두 곳에서 각각 동작하여 네트워크 계층위에 애플리케이션 등이 잘 동작할 수 있게 구성해줌. 6Lowpan/SCHC를 담당한다고 보면 됨.
* libschc(https://github.com/imec-idlab/libschc)
  * SCHC의 C 프로그램. IP 계층과 MAC 계층 사이에 존재. 
* LoRaMac-node(https://github.com/Lora-net/LoRaMac-node)
  * contiki-ng의 밑에 Mac Layer의 LoRaWAN을 제공.
* ChirpStack(https://www.chirpstack.io/)
  * LoRaWAN 서버와 MQTT 통합을 제공. 

### [동영상 분석](https://www.bilibili.com/video/BV1ih411o7Uz)

```shell
Eenddevice
$ minicom
$ help
$ ip-addr 
주소목록나옴

Gateway
$ sudo ./border-router.native -a 1 fd00::1/64
$ ping fd00::1
$ ping6 -c 1 -w 500 -s 512 fd00::2
$ ping6 -c 1 -w 500 -s 512 엔드디바이스ipv6address

Gateway - CoAP
$ sudo ./border-router.native -a 1 fd00::1/64
$ ip-addr
$ ping fd00::1

Enddevice
$ coap-server -d 1
$ coap-client -m put -b 256 -f firmware-new.bin.ota coap://[::1]/ota
$ make flash
$ minicom

Host(App Server)
$ sudo ufw allow from fd00::~~
```

### 설치

1. 게이트웨이와 라즈베리파이 USB로 연결하기. (https://heltec-automation-docs.readthedocs.io/en/latest/gateway/ht-m01/qucik_start.html#usb-mode)
2. chirpstack 설치. (https://www.chirpstack.io/project/guides/debian-ubuntu/)
3. chirpstack 설정(https://www.chirpstack.io/project/guides/connect-gateway/)<br>
게이트웨이, chirpstack 연결(https://heltec-automation-docs.readthedocs.io/en/latest/gateway/ht-m01/connect_to_server.html#connect-to-chirpstack-server)
4. 게이트웨이
5. Enddevice랑 연결된 컴퓨터
6. Enddevice에서 hello-world.hex를 넣고 flash. 
7. ping command


## LoRa Dragino Hat, ICA880a, Chirpstack을 사용해 LoRaWAN 구축

엔드디바이스에서 otaa 동작과정을 시작하면 네트워크 서버까지 값이온 뒤 네트워크 서버에서 필요한 세션키 등을 생성해서 엔드디바이스까지 보내줘야 하지만 게이트웨이까지 오고 게이트웨이에서 엔드디바이스로 가지 않는 상황. 게이트웨이 packet-forwarder 프로그램(https://github.com/Lora-net/packet_forwarder)의 동작 속도 등을 조절해볼 예정
