## IPv6-over-LoRaWAN raspberrypi test

주문한 장비가 오기 전 해당 레포지토리의 내용을 라즈베리파이를 사용하여 테스트 중에 있음. 

<img alt="character" width="900" src="https://user-images.githubusercontent.com/47745785/114259804-a1838180-9a0b-11eb-84ca-90d7f4004f4d.png" />

위 과정을 통해 border-router 역할을 하게 만든 라즈베리파이는 영상과 비교해보았을 때 정상 동작하는 것으로 판단됨.

<img alt="character" width="900" src="https://user-images.githubusercontent.com/47745785/114259822-d1328980-9a0b-11eb-89f1-eee966dca77b.png" />


<br><br><br><br>
그러나 현재 문제가 되는 부분은 end-device 부분임.

<img alt="character" width="900" src="https://user-images.githubusercontent.com/47745785/114259833-ed362b00-9a0b-11eb-8e00-2d1e27da1689.png" />

5번 과정을 거쳐 생성된 .hex 파일을 flash를 통해 장비에 넣어야 하는데 현재 모듈 구조상 매끄럽지 못함. 이번에 구매한 lora-node-151의 경우 해당 장비에 lora칩과 라즈베리파이의 역할을 하는 모듈이 같이 들어가 있어서 직접 노트북에 연결하여 .hex 파일을 flash 한 후 진행할 수 있을 것으로 보이지만, 현재는 그 구조가 만들어지지 못함.

라즈베리파이에는 .hex 파일을 flash 할 수 없기 때문에 아두이노 우노에 해당 파일을 flash 해야하고 현재 작업환경은 라즈베리파이의 raspbian이기 때문에 두 장비 간 연결을 usb 형태로 진행하고 avrdude를 사용하여 .hex 파일을 아두이노에 넣는 것을 진행하고 있음. 그러나 명령어 실행 시 정상 동작하지 않고 있음.


<img alt="character" width="900" src="https://user-images.githubusercontent.com/47745785/114259858-1b1b6f80-9a0c-11eb-9af3-4931021b0e79.png" />

<img alt="character" width="900" src="https://user-images.githubusercontent.com/47745785/114259859-1c4c9c80-9a0c-11eb-99ef-19b8782282e8.png" />


아두이노에서 파일을 컴파일 시 programmer를 설정하는 부분이 있는데 첫 번째 사진에서 해당 부분에 문제가 있을 것 같다고 판단되어 컴파일 시 여러 설정들로 바꾸어 진행을 해보았으나 아직 성공하지 못함. 추후 이 부분을 좀 더 진행해볼 계획임.

라즈베리파이와 아두이노를 usb가 아닌 pin mapping을 통해 연결하는 방법도 존재하지만 두 장비 사이의 전력이 차이가 나기 때문에 연결 부분 중간에 변환기 역할을 하는 장비가 필요하다는 이야기도 있고, 현재 라즈베리파이에 dragino lora hat이 mapping 되어 있기 때문에 우선적으로는 usb 형태로 연결하는 것을 진행해볼 계획임.