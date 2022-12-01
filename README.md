# find_my_doggy
### 해당 모델은 제가 키우는 강아지들과 다른 강아지들을 모두 학습시켜 구분하는 CNN 모델입니다.
### 작동환경은 google colab입니다. 
### 모델의 실행 절차를 다음과 같이 하였습니다.
## 1. Data Crawl
- 제가 키우는 강아지가 아닌 다른 강아지들의 사진 데이터를 얻기 위해 아래 API 서버를 이용하여 데이터를 수집하였습니다.
('https://api.thedogapi.com/v1/images/search')
![image](https://user-images.githubusercontent.com/71024217/205002645-56b933ab-6531-428a-966c-1752c1929b05.png)

- 해당 API 서버로 접속하면 다음과 같은 사진 정보가 주어지는데, 여기서 HTML 링크를 parsing해 이동하면 아래와 같이 random하게 강아지 사진을 수집할 수 있습니다.

![image](https://user-images.githubusercontent.com/71024217/205002799-85d72555-4add-4c5a-af78-95c818ad5302.png)

- 제가 키우는 강아지들은 drive에서 바로 업로드 할 수 있도록 세팅되었습니다.


## 2. Face Recognition
- 강아지를 인식하는데 주변 사물이나 배경이 인식을 저해할 수 있기 때문에, python dlib을 이용한 face recognition 처리를 진행하였습니다.
- 해당 코드를 정상적으로 실행하기 위해서는 dlib이 설치되어있어야 하며, tureckova님이 작성하신 얼굴 인식 모델을 설치하셔서 경로 상에 배치하셔야 합니다. (필요한 파일은 dogHeadDetect.dat, landmarkDetector.dat 두개입니다.)
[강아지 얼굴 인식 모델 링크](https://github.com/tureckova/Doggie-smile)

- face_recognition 라이브러리가 설치되신 분들은 install하지 않고 진행하시면 됩니다.

- opencv를 활용해 face_recognition된 부분을 rectangle처리하여 나타내는 함수인 find_dog_face와 시각화 하지 않고 저장하는 save_dog_face 함수를 설정하여 경로를 지정해 실행하시면 됩니다.
![find_dog_face실행화면](https://user-images.githubusercontent.com/71024217/205005736-6bc50e6d-6f21-4ae3-bceb-a39cd7730555.png)

- 전처리된 파일들을 세팅해주시고 find_my_dog 파일을 실행하시면 됩니다.

## 3. CNN
- 파일 내부에는 2개의 model이 있습니다.
- 첫번째 모델은 dropout이 적용되지 않은 기본 CNN 모델입니다.

![image](https://user-images.githubusercontent.com/71024217/205006176-0b72839c-b256-4c3f-856b-a38ae8be3210.png)

- 데이터셋이 부족하여 overfitting이 발생하였습니다. 추후에 작성된 data argumentation을 기반으로 데이터를 증량하여 시도해볼 예정입니다.

![image](https://user-images.githubusercontent.com/71024217/205006438-ba111631-3dbf-492c-a44a-ddb6957bd162.png)

- 두번째 모델은 dropout을 적용한 CNN입니다. 새로운 test 데이터 8장에 대해서도 잘 작동하였습니다.
![image](https://user-images.githubusercontent.com/71024217/205006635-e88e8570-0011-46c4-b647-927e336819d2.png)
![image](https://user-images.githubusercontent.com/71024217/205006739-3e57ab8c-c0d0-42d9-af26-e730f36a6f27.png)
![image](https://user-images.githubusercontent.com/71024217/205006780-87ece005-d284-4af3-8551-c742d2c26d2b.png)

