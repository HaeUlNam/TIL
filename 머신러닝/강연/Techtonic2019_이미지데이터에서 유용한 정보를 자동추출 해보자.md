### 성공사례

1) 결함 검출: 딥러닝 이미지 처리 기술을 통한 외관 품질검사 자동화'

2) 설계 도면 인식: 설계 도면 업무에 딥러닝 이미지처리를 적용하여 도면상 설계기호인식을 자동화하여 작업 효율화 달성

3) 암 발병 위험 예측: EHR, MRI 이미지를 분석하여 암 발병 위험 및 치료 예후를 예측

4) 심전도 등의 의료 데이터를 분석하여 부정맥 진단에 도움 (부정맥 패턴을 찾음)

### 전통적인 머신러닝 vs 딥러닝

![스크린샷 2020-03-19 오후 12 30 06](https://user-images.githubusercontent.com/26040955/77028850-5f8d3500-69dd-11ea-9b1a-c4438dfa91bf.png)

### No Free Lunch Theorem

- 모든 상황에 항상 잘 동작하는 것을 사전에 보장하는 단 하나의 recipe는 없다. 아래의 두 데이터는 서로 다른 데이터 전처리를 적용해야 한다.

![스크린샷 2020-03-19 오후 12 45 17](https://user-images.githubusercontent.com/26040955/77029604-7e8cc680-69df-11ea-9782-6aa5d45a85bf.png)

- 현실에 있는 데이터는 굉장히 지저분하다.

### OCR(Optical Character Recognition)

- AICR: AI-based OCR

- 대부분의 문서는 인쇄체이다. 따라서, 보통은 폰트를 학습하게 된다. 폰트가 굉장히 여러가지가 있다.

- 학습한 폰트에 대해서는 잘할 것이다. 하지만, 현실의 데이터는 이렇게 흐리기도 하고, 백그라운 색상이 너무 강하기도 하다.

- 학습하는 측면에서 이러한 오염들을 대응하기 위해서는 학습 데이터를 여러 형태로 부풀려주는 작업이 필요하다. 이것을
Data Augmentation이라고 한다.

- 아래와 같이 블러 처리를 한다던지, 일부러 로스를 만들어서 학습하여 대응하게 된다. 하지만 Data Augmentation은 끝이 없다. 따라서, 
자신의 상황에 맞는 Augmentation을 적용하는 등의 노력이 필요하다....

![스크린샷 2020-03-19 오후 12 57 00](https://user-images.githubusercontent.com/26040955/77030146-2060e300-69e1-11ea-83e5-548cf56a6e48.png)

출처: https://erikbern.com/2016/01/21/analyzing-50k-fonts-using-deep-neural-networks.html

### Automatic Augmentation

- 효과적인 학습데이터를 자동으로 생성하는 기술

### 워터마크 개선

- 인식 성능에 영향을 준다. 따라서, 모델을 건드리지 않고 데이터를 전처리를 통해 인식 성능 향상('명도' 기준으로 인식에 주는 영향을 약화)

### 회전 보정

1) 90도 이상 회전되어있는 것을 원래 상태로 회전
  * 참고자료: https://hal-enpc.archives-ouvertes.fr/hal-01864755/document

2) 많이 회전되지 않은 것들은 컴퓨터 비전을 이용하여 가로 선을 추출하고, baseline과 비교하여 회전을 수행.


![스크린샷 2020-03-19 오후 1 15 32](https://user-images.githubusercontent.com/26040955/77031012-b7c73580-69e3-11ea-9e57-234dc164e99f.png)

### 문자 특성 반영

![스크린샷 2020-03-19 오후 1 17 38](https://user-images.githubusercontent.com/26040955/77031130-0379df00-69e4-11ea-968d-4c2445f267f2.png)

### 직인 제거

- 색상 분할(Color Clustering)을 통해서 직인 부분을 제거하고, 인식 진행.

![스크린샷 2020-03-19 오후 1 19 39](https://user-images.githubusercontent.com/26040955/77031232-4b006b00-69e4-11ea-844b-04c4a6afd8e7.png)

  * 참고자료: https://youngest-programming.tistory.com/92

### 손상 이미지 처리

https://github.com/cvlab-stonybrook/DewarpNet

### 결과 신뢰도

- 은행에서 이 모델을 사용하고 있는데, 우리가 추측한 것이 신뢰할 수 있는지를 알려줘야 한다. 따라서, Confidence Score를 통해 
이러한 작업을 할 수 있도록 했다.

![스크린샷 2020-03-19 오후 1 28 11](https://user-images.githubusercontent.com/26040955/77031624-7c2d6b00-69e5-11ea-9264-a97d38ed8ce9.png)


#### 삼성SDS가 생각하는 Enterprise AI라는 건 분석가의 역량과 노력이 플랫폼화가 이 플랫폼을 사용하는 누구나 분석가에 준하는 성능을 낼 수 있도록 하는 것




















