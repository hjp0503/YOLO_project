# YOLOv4_project 

### 🚢 자율운행 선박을 위한 카메라 기반 장애물 인식 및 회피 시스템 🚢  
![image](https://user-images.githubusercontent.com/60416651/113977243-43289880-987d-11eb-893f-fa6cb7ce69a8.png)

## 1. 개요 및 필요성
  차량이 인간의 도움 없이 스스로 주행하기 위해서는 주변 장애물에 대한 빠른 탐지와 신속한 대응이 중요하다. 그렇기 때문에 비디오 카메라, 레이더, LIDAR, GPS, SONAR 등의 기술들을 동시에 활용하여 자율주행 능력을 높인다. 그 중에서도 특히 비디오 카메라는 물체를 구별하고 장애물을 피하며 경로를 탐색하는 ‘시각적 인식’을 하는 데에 더욱 핵심적인 역할을 한다.  
  해양 환경에서 선박은 AIS(Automatic Identification System)를 사용하여 주변 배를 인식한다. 하지만 부표, 소형보트, 카약과 같이 규모가 작고 AIS 송신기가 없는 물체는 인식이 불가능하기 때문에 해양 사고가 발생할 수 있다. 그러므로 비디오 카메라를 이용하여 자율주행 선박에서 해양 환경의 장애물을 인식하고 회피할 수 있는 시스템을 제안한다. 


## 2. 개발 내용
   취지에 적합한 기술을 알아본 결과, 딥러닝의 Object Detection 기법 중 **YOLOv4**가 과제에 적합하다고 판단하였다.  
   YOLOv4는 1개의 GPU를 사용하는 일반적인 학습 환경에서도 실시간 수준의 빠른 속도와 기존 YOLO 모델보다 개선된 정확도를 제공하고 있다. 그러므로 YOLOv4를 해양 환경에 맞도록 커스터마이징하여 구현하는 것이 이번 과제의 목표이다.  
   학습에 사용하는 커스텀 데이터셋은 싱가포르 해양 데이터셋(SMD, singapore maritime dataset)로 알려진 공개 데이터셋을 가공하여 만들었다. 컴퓨터에 실행 환경을 구축하고 YOLO를 실행시키기 위한 신경망 프레임워크인 Darknet을 설치하였다. 실행 환경과 커스텀 데이터셋에 맞게 YOLOv4의 네트워크 구조와 학습 하이퍼파라미터를 수정한 후 본격적으로 학습을 시작하였다.  


## 3. 개발 환경
Hardware  
+ CPU: Intel(R) Xeon(R) CPU E5-2620 v3 2.4GHz * 2  
+ GPU: GeForce GTX 1080 Ti * 12  
+ RAM: 16GB  

Software  
+ OS: Ubuntu 18.04.5 LTS  
+ CUDA: 11.2  
+ cuDNN: 8.0.5  
+ Framework: Darknet  

## 4. 파일 설명

## 5. 실행 순서

### (1) github 저장소 복제
git을 clone하거나 현재 이 페이지에서 zip파일을 다운로드 한다.

```
git clone http://github.com/hjp0503/yolov4_project.git 
```
YOLO를 실행시키키 위한 신경망 프레임워크인 Darknet(https://github.com/AlexeyAB/darknet.git)은 이미 저장소 안에 설치된 상태이다.


### (2) darknet make
자신의 컴퓨터 환경에 맞게 makefile 파일을 수정하고, make 명령어를 통해 darknet을 컴퓨터에 make 한다.  
```
make
```


## 6. 현재까지의 수행 결과
  학습 모델이 결과로 도출되었고, 성능을 확인해보았다. 대표적인 성능 평가 지표인 mAP는 78.17%, precision, recall, average iou는 각각 90%, 93%, 76.10%로 나왔다.  
  샘플 이미지 몇 장으로 모델을 테스트해보았을 때, 10개의 클래스에 대하여 대부분 정확하게 분류하는 것을 확인하였다. 하지만 크기가 작거나 거리가 멀어서 작아 보이는 소형 object에 대한 탐지성능, 큰 object에 완전히 겹쳐진 object에 대한 탐지성능, 전체가 아닌 부분으로 보여지는 object에 대한 탐지성능이 다소 부족하여 이에 대한 개선이 필요하다고 판단하였다.
  
  
## 7. 기대효과 및 개선방향
  사람의 눈으로도 확인이 어려운 부분까지 잘 탐지하는 것으로 보아 모델을 조금 더 개선시키면, 현장에서의 실질적인 사용도 가능하다고 생각한다. 탐지성능이 떨어지는 문제는 관련 논문과 책에서 비슷한 사례를 찾아보고, 하나씩 고쳐나갈 예정이다.

