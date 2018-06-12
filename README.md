# u-Health-Care-System
# u-Health-Care_client_comteam

광운대학교 제 2회 산학협력 S/W 개발

<COMTEAM 결과물>


프로젝트 명 : 인공지능 U-Health-Care System -웨어러블 디바이스를 통한 딥러닝 생체 리듬 분석
 
참여 기업 : 아이센스

지도 교수 : 

컴퓨터공학부  이혁준 교수


팀     원 :	

컴퓨터공학부  이명진 lmjin4050@naver.com		

컴퓨터공학부  김기선 rionkingk1@naver.com

컴퓨터공학부  김지웅 hosin2004@naver.com

컴퓨터공학부  이호영 ghdud4006@gmail.com
      
      
      
      
사용 영상 : https://www.youtube.com/watch?v=Xk8d8NQWQCY


===============================================

사용 환경

1. 웨어러블 디바이스 : Xiaomi mi-band2

2. 클라이언트 : 안드로이드 모바일 (API 23 이상)

===============================================

사용 방법

1. 회원가입

2. 로그인

3. 운동하기

4. 디바이스 Mac Address 입력 후 connecting 버튼 클릭 

-> 먼저 mi fit 앱을 설치 후 설정창에서 mac address 확인 

5. 운동하고 싶은 강도 선택

6. Music On 버튼 클릭

7. start 버튼을 길게 눌러 운동 시작

8. 64초 주기로 운동 강도를 조절 

===============================================


1. 개요

본 프로젝트는 인간에게 가장 가까운 기기인 웨어러블 디바이스와 최신 인공지능 기술인 딥러닝 기술을 결합해 사용자에게 새로운 유의미한 데이터를 제공하는 데에 목적을 둔다.

 사용자가 원하는 운동량을 적합하게 하고 있는지 확인하고 사용자의 컨디션에 따른 운동 강도를 추천해 준다. 추천은 음악의 속도를 조절하여 사용자로 하여금 자연스럽게 운동 강도를 조절할 수 있게 하며 동시에 운동데이터를 저장한다. 저장한 운동데이터를 이용하여 사용자의 운동 패턴과 몸 상태를 예측하며 사용자가 기록을 볼 수 있도록 하는 헬스 케어 시스템을 구현한다.


2. 전체 구조

가. 전체 시스템 구성 
 위의 시스템 전체 구조도를 보면 알 수 있듯이 웨어러블 장치, 안드로이드 장치, 구글 핏 SDK 및 구글 피트니스 스토어, 아마존 서버, 텐서플로우 딥러닝 프레임워크로 구성된다.




 나. 안드로이드와 구글 핏 SDK
 먼저 웨어러블 디바이스인 MI Band2에서 전용 어플리케이션인 Mi Fit으로 추출 데이터가 이동한다. Mi Fit에서 Google Fitness의 API를 사용해 안드로이드 어플리케이션으로 데이터가 이동한다. 안드로이드 어플리케이션에서 웨어러블 장치(Wearable device) 정보를 구글 중앙 저장소로부터 얻어, 서버와 통신하게 된다. 이 때 안드로이드 어플리케이션에서 JSON 자료형으로 HTTP통신을 통해 서버와 통신하게 된다. 본 시스템에서는 아마존 클라우드 시스템을 이용하여 추후 이용자가 늘어날 경우에도 유연하게 대처할 수 있도록 하였다.



다. 아마존 클라우드 시스템
 본 서비스에서 이용하는 아마존 클라우드 서비스는 총 3가지로, 데이터베이스를 관리하게 되는 RDS, 가상 리눅스 환경을 구성하는 EC2, 모델과 데이터를 저장할 수 있는 스토리지인 S3이다. RDS는 NodeJS를 통한 AWS 내부 DB 환경을 구성하고, EC2에서는 딥-러닝을 통해 얻어진 모델을 적용하기 위한 가상 리눅스 시스템 환경을 저장하고, 트레이닝 모델과 생체 데이터를 저장하기 위해 RDS를 이용한다.



라. 텐서 플로우 프레임워크
 기존의 생체정보로부터 새로운 정보를 얻어내기 위해 구글이 제공하는 딥-러닝 프레임워크를 사용하여 새로운 모델을 개발하고 적용하고자 한다.
 
 
 
 3. 결론
 
  우리는 웨어러블 디바이스와 스마트폰을 연동하여 클라우드 서버에 의한 헬스 케어 관련 정보를 사용자에게 제공하는 시스템을 설계하여, 이를 통해 축적된 정보를 딥-러닝 기법을 활용해 의미 있는 정보로 가공하기 위한 시스템을 설계해 보고자 하였다.
  
 64초 동안의 심박 수를 하나의 패턴으로 인식하고 CNN을 사용하였는데 그 이유는 웨어러블 장치의 부정확함에 있다. 우리가 사용한 미-밴드는 저가형 웨어러블 디바이스이다. 또한 현재 웨어러블 디바이스의 기술력이 1초마다 정확한 심박 수를 계속해서 가져오기는 무리가 있다. 이러한 이유 때문에 측정 중 부정확한 입력을 필터링하고, 걸러 내야한다. 따라서 우리는 심박 수 전체의 평균이나 순간의 심박 수를 활용할 수 없었고, 중간 중간 값이 이상하더라도 각각의 강도마다 정해진 패턴이 있을 것이라 생각하여 CNN기반의 딥-러닝을 사용하였고 99%의 정확도를 가지게 되었다. 이렇게 우리가 측정한 예측 값과 사용자가 선택한 운동 강도가 다를 시 우리는 음악 속도 조절을 통해 사용자가 선택한 운동 강도를 맞출 수 있도록 하였다.
 
 지금은 사용자의 수에 한계가 있어서 데이터 수집에 한계가 있지만 많은 사용자들이 사용하기 시작하면 더 많은 데이터가 모이게 되고 더 나은 서비스를 제공할 수 있다고 생각한다.
 
 또한, 우리의 서비스는 운동 강도와 사용자가 원하는 운동 강도를 맞추기 위해 음악속도 조절을 이용하는데 지금은 어플리케이션에 저장되어 있는 음악을 사용한다. 하지만  더 나아가 다른 음악 스트리밍 어플리케이션의 음악 플랫폼을 이용해 사용자가 더 가깝게 접근할 수 있는 음악을 제공할 것을 기대한다.
 
 
 
