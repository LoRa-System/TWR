### MQTT integration 준비 작업

<p align="center">
<img alt="character" width="700" src="https://user-images.githubusercontent.com/47745785/115045090-25a89e00-9f11-11eb-9d95-59f6c9a863e9.png" />
</p>

장비가 오기 전에 step4 이전 단계까지 어느정도 구축을 하고자 설치된 chipstack network-server와 app-server를 사용하여 end-device와 OTAA 과정을 진행함. 여러 차례 진행을 한 결과 동작이 한번 되긴 했지만 그 이후로는 동작이 되지 않는 상황임.

<p align="center">
<img alt="character" width="600" src="https://user-images.githubusercontent.com/47745785/115045219-4670f380-9f11-11eb-8325-09bb7c4341f3.png" />
</p>

<p align="center">
<img alt="character" width="600" src="https://user-images.githubusercontent.com/47745785/115045424-74eece80-9f11-11eb-902e-36e21fa1bcbc.png" />
</p>

<p align="center">
<img alt="character" width="600" src="https://user-images.githubusercontent.com/47745785/115045437-76b89200-9f11-11eb-9edb-a9714b60d6af.png" />
</p>

End-device에서 app-server까지 정상적으로 연결이 되었을 때 app-server에 등록된 Gateway와 end-device 페이지 각각에서 raw data가 출력됨. 그러나 한 번을 제외하고 설정값들을 변경하지 않은 상황에서 수차례 시도를 해 보았지만 End-device에서 돌아오는 데이터를 계속해서 받지 못하는 현상이 발생함. app-server에서 raw data가 출력되는 시점이 End-device가 txpk을 받은 시점에 출력되기 때문에 해당 데이터들도 볼 수 없음.

<p align="center">
<img alt="character" width="600" src="https://user-images.githubusercontent.com/47745785/115045611-a10a4f80-9f11-11eb-81e9-02de86f61736.png" />
</p>

위 사진은 gateway log를 캡쳐한 것인데 end-device로부터 받은 rxpk를 app-server까지 전달한 후 app-server로부터 받은 txpk이 출력되는 것을 확인할 수 있음. 그러나 end-device에서는 해당 패킷을 받지 못함. 


### 향후 계획

Dragino를 사용한 end-device로 chirpstack 네트워크 서버와 한 번의 OTAA 동작과정을 성공했지만, 또 다시 계속 연결이 되지 않는 상황임. 

<p align="center">
<img alt="character" width="700" src="https://user-images.githubusercontent.com/47745785/115045790-cd25d080-9f11-11eb-82ff-c9d9665c629f.png" />
</p>

Chirpstack의 End-device목록에 Dragino Hat이 나와있지 않고, 저희가 ChirpStack에서 지원하지 않는 로라 모듈에 Dragino에서 만든 (dragino + raspberry + OTAA) 오픈소스를 가지고 계속 시도를 해보고 있는 상황이라 모듈간의 통신이 불안정 할 수 밖에 없다고 판단함. 해당 문제는 장비 문제가 원인이라고 판단하고 이후 IPv6_over_LoRaWAN의 Readme에서 언급한 CoAP 오픈소스를 어떻게 사용해야 할지 분석할 계획임.
