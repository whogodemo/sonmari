# sonmari
수어 번역 프로그램입니다.

# 프로젝트 소개
농인과 수어에 대한 사람들의 인식 부족과 관련 서비스 부족으로 기본적인 서비스, 특히 의료권을 보장받기 어려운 현실입니다. 의료수화통역사가 존재하기는 하지만, 이는 보편화가 되지 않아 농인들이 의료 서비스를 제공받을 때 실질적인 도움을 주지는 못하고 있다고 합니다.
이 부분에서 수어 통역 시스템의 필요성을 느끼고 이를 개발하기로 했습니다. 기존의 관련 프로그램을 찾아보면 무엇보다 수어 통역 프로그램 자체가 많지 않은 데다가  이미지 상태의 정적인 수어만을 번역하거나 기역, 니은, 디귿과 같은 자모음을 뜻하는 지화 이미지에 대한 번역만을 제공하기 때문에 실생활에서 사용하기에는 제한적입니다. 따라서 저희는 연속적인 수어 동작을 인식하고 이를 문자언어로 번역하는 프로그램을 개발하는 것을 목표로 삼았습니다.

# 필요 하드웨어
<img src="https://user-images.githubusercontent.com/74365895/120751737-7f0d7080-c543-11eb-95da-89724a2c51e9.jpg"  width="500" height="400">

의사와 환자 각각 방향의 모니터 두 대와 환자 방향의 웹캠을 이용합니다.

# 사용 방법
손마리의 사용자는 의사와 환자이며 진료를 시작한 의사가 환자에게 전송할 메시지를 클릭합니다. 이 메시지는 어디가 아프세요와 같이 병원에서 진료 시 자주 묻는 기초적인 질문을 미리 수어영상으로 프로그램 데이터에 등록해놓은 것입니다. 그러면 이 수어 영상이 환자의 모니터에 출력이 됩니다. 다음으로 이 질문을 본 농인 환자가 수어로 질문에 대한 대답을 하면, 프로그램이 해당 수어 동작을 인식하여 문자 언어로 번역을 해서 의사 화면에 출력을 하게 됩니다. 

<img src="https://user-images.githubusercontent.com/74365895/120751974-d7447280-c543-11eb-9afa-c0a896c8b74c.png"  width="800" height="400">
<img src="https://user-images.githubusercontent.com/74365895/120751990-dc092680-c543-11eb-88fd-e800d170ec9e.png"  width="600" height="400">

# 시연 영상
https://www.youtube.com/watch?v=oVhpUMyGJrw

# 필요 기술
RNN과 CNN의 결합으로 동적인 영상에 대한 번역을 구현한 경우 속도가 느리거나 실시간이 아니라는 한계가 있습니다. 빠른 속도를 내면서도 영상을 번역할 수는 없을까?라는 고민을 하게 되었고 그 과정에서 빠른 속도로 실시간 객체 탐지를 제공하는 YOLO를 찾게 되었습니다.

<img src="https://user-images.githubusercontent.com/74365895/120753068-977e8a80-c545-11eb-8ac1-7914844aac8c.png"  width="800" height="400">

YOLO는 변형된 R-CNN구조를 가지고 있습니다. R-CNN은 선택적 탐색 알고리즘으로 입력값으로 주어지는 하나의 이미지를 cnn을 통과하는 2000개의 서브 이미지로 추출하는 구조입니다. 그러나 욜로는 이와 달리 합성곱 신경망을 단 한번 통과 시킵니다. 결과로 각 객체의 바운딩 박스와 해당객체가 무엇인지 분류 확률을 출력합니다. 최종적으로는 이 값을 non-max suppression을 통해 리전을 결정합니다.

트레이닝 후 나오는 가중치 값을 이용해서 실시간 카메라와 함께 띄우면 데이터와 비슷한 손동작을 인식해 바운딩 박스가 뜨게 되고 클래스 이름이 출력됩니다. 이 때 쓰러지다 1과 쓰러지다 2가 순차적으로 인식이 되면 쓰러지다가 출력되도록 했습니다.
<img src="https://user-images.githubusercontent.com/74365895/120752859-4a9ab400-c545-11eb-9f7b-ce19e137ae6f.png"  width="800" height="400">

# 사용 방법
위 프로그램을 다운받아 이용하려면 우선적으로 YOLO와 CUDA가 설치되어있어야 하고, GPU가 내장된 컴퓨터여야 합니다.
욜로 설치는 다음 레퍼런스를 참고하세요.
https://wiserloner.tistory.com/m/1247

# 번역 단어
이틀,삼일,감기,콧물,쓰러지다,설사,예,아니,머리,배,아프다 등 11개 단어에 대한 번역을 제공합니다.

<img src="https://user-images.githubusercontent.com/74365895/120754272-656e2800-c547-11eb-90b1-b93bb4e0fbef.png"  width="600" height="600">


# license
해당사항 없음


