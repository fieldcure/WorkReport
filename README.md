# 작업 내용

## 2024-07-29~08-04
### 이미지 외곽에 선 나오는 버그 해결
### GTV 적용할 수 있도록 수정

![image](https://github.com/user-attachments/assets/f5b4091b-678a-44a3-b8f1-2e66ea0e32cd)

### 256사이즈가 아닌 데이터에서 동작하도록 수정
(288, 384, 192)로 테스트함

![image](https://github.com/user-attachments/assets/bfff6043-50bb-4f40-b9f2-863a036496bc)

## 2024-07-23~07-28
### External/Stage1(2D only)/Stage1(2D+3D)/Stage2로 나누었음
-> 정상적으로 동작 : 2022년 모델(Stage1 2D, Stage1 2D+3D, Stage2 2D), 2024년 모델(Stage1 2D, Stage2 2D) <br>
-> 비정삭적으로 동작 : 2024년 모델(Stage1 3D)

![image](https://github.com/user-attachments/assets/78e933e6-00ec-4382-b3f8-b81fe054676d)
![image](https://github.com/user-attachments/assets/9c32a6b9-924e-405d-bfca-0f3b2dc92443)
![image](https://github.com/user-attachments/assets/16789167-eade-4886-a6cc-6111fdeb145c)
![image](https://github.com/user-attachments/assets/c4e140e1-f88d-43a5-a9bc-cd918aedc191)
![image](https://github.com/user-attachments/assets/6657ad4e-8d70-4d83-8888-1eb0566f4cd1)

### 데이터 비교(Stage1의 2D의 결과값이 Stage1의 3D의 input으로 그대로 들어가기 때문에, Stage1의 3D가 필요한지 의문)
![image](https://github.com/user-attachments/assets/1b8b02b4-7a02-4448-9172-9f9ad82245dd)

## 2024-07-15~07-22
### 2022년도 모델로 돌린 결과 GPU 11기가 정도 잡아먹음
![image](https://github.com/user-attachments/assets/68f8d5dc-af47-4c4e-b92a-eb16399436e1)

### 2022년도 모델 결과
2024년도 모델에서도 적용 가능한 seperate & merge 코드로 동작하는 것을 확인함
8분 정도 소요됨
![image](https://github.com/user-attachments/assets/b970a3bf-e4b3-4d85-8a9f-41d85c59f470)

### 2024년도 모델 파일 에러
python에서의 모델은 <br>
인풋 데이터가 float32 <br>
아웃풋 데이터가 float16 <br>
인데 <br>
onnx 파일은 <br>
인풋 데이터가 float32 <br>
아웃풋 데이터가 float32 <br>
로 잘못되어 있음 <br>
c++ 코드로 돌리면 결과 사이즈가 예상 사이즈의 1/2 임 (4 * 128 * 128 * 128 이여야 하는데 4 * 128 * 128 * 128 / 2)  <br>
용하에게 새로 모델을 요청하였지만 언제 받을 수 있을지는 잘 모르겠음 <br>

![image](https://github.com/user-attachments/assets/3e9250fa-3282-471b-9e1b-c829f2ca587b)

## 2024-07-09~07-14
Seperate & merge 코드를 이용해 stage2D가 돌아가도록 적용
버그 수정 및 테스트

## 2024-07-01~07-08
seperate2D & merge2D 함수 간략화 <br>
seperate3D & merge3D 함수 구현 -> gpu 메모리 부족(사용하는 gpu가 2gb여서 그런 듯)이므로 회사 컴퓨터로 확인 필요 <br>
3D label 결과 확인중 -> 문제 없으면 stage2 구현할 예정 <br>
이미지 사이즈 padding&crop은 그 이후 구현 <br>

아래 사진은 patch size = (128, 128, 128), stride = (128, 128, 128)을 사용한 결과 -> 각 patch의 테두리에 경계선이 생기는데 특별히 문제가 없는지 의문

![image](https://github.com/fieldcure/WorkReport/assets/40055222/54bee062-89bc-4a1b-9951-fcd85f51cacf)

## 2024-06-25~30
seperate2D & merge2D 함수 구현 후 sigmoid 결과 확인

<img src="https://github.com/fieldcure/WorkReport/assets/40055222/40356d60-7406-42cb-a048-c33f6aabe642" width="200"/>

### 작업 예정 함수들
1.real_case_test_2D_3D의 <br>
real_dataset(for 2d) <br>
real_2D_test <br>
merge2 <br>

{ # 확인 후 필요한 경우 작업 <br>
    imgTemp = np.expand_dims(img, axis=0) <br>
    data_final = np.concatenate([imgTemp, output_2D], axis=0) # data_final = [7,256,256,256] <br>
}

real_dataset(for 3d) <br>
real_3D_test <br>
merge_cube <br>

2.real_case_test_2D의 <br>
real_dataset <br>
real_2D_test <br>
merge2 <br>

+α -> [256,256,256]인 데이터셋으로 정상적으로 동작하면 이후 작업 시작 <br>
resampling <br>
padding <br>

## 2024-06-15~16
gpu에서 동작가능하게 수정(방법은 전달할 예정)

필요한 환경
 - onnxruntime18.0
 - cuda 11.8
 - cudnn 8.9.7.29

최신 모델 동작은 정확히 어떤 부분이 어떻게 수정되었는지 확인 후 작업 시작

## 2024-06-12~14
roi만드는 부분 좌표계 변환하는 부분이 이상해서 확인 필요
-> 전기장 데이터도 결과도 이미지와 딱 떨어지 않았는데, 샘플 데이터(256,256,256에 임의 큐브 영역 1 대입)와 실제 이미지 데이터도 똑같이 딱 맞아 떨어지지 않는 문제가 있었음
-> 좌표계 변환하는 부분에서 x좌표 +0.05 y좌표 +0.05 하여서 임시 처리 하였으나, 원인을 찾을 필요가 있어보임.
-> 원인을 찾으면 전기장 데이터 값도 이미지 영역에 맞도록 일치시킬 수 있을 것으로 예상

샘플 데이터 결과
![image](https://github.com/fieldcure/WorkReport/assets/40055222/ce2deb2a-1d90-49c7-a808-3fc4070f2ea9)

x좌표 +0.05 y좌표 +0.05 처리 결과 (spacing 0.1(cm)) (내부 사각형은 1로 채워진 부분이며 무시하여도 무관함. 외부의 컨투어의 영역이 이미지의 영역과 맞아 떨어진 것으 중요함-> 밑의 roi가 이미지와 맞아떨어지는 결과로 이어짐)
![image](https://github.com/fieldcure/WorkReport/assets/40055222/4057db54-9bad-4769-9050-fbb9be6f510b)


## 2024-06-12
stage1과 stage2의 결과를 roi로 만들어 표시 -> roi만드는 부분 좌표계 변환하는 부분이 이상해서 확인 필요 

![image](https://github.com/fieldcure/WorkReport/assets/40055222/2ee90acc-4b7a-4dea-b420-5b3498cc474e)


## 2024-06-11
컨투어 만드는 부분 버그 수정

## 2024-06-10 
온코 필드에 ONNX 코드 이식 및 실행 가능 하도록 코드 수정

## 2024-06-07 ~ 2024-06-09

### stage1의 infer2D, infer3D가 동작하도록 수정
stage1의 infer2D 결과

<img src="https://github.com/fieldcure/WorkReport/assets/40055222/ca03b21d-dda6-4b6f-94b0-b883d381bd04" width="500">

stage1의 infer3D 결과

<img src="https://github.com/fieldcure/WorkReport/assets/40055222/e0f627a1-baa6-4c76-9d5b-cce0d2cfa016" width="500">

### stage2의 infer2D가 동작하도록 수정
stage2의 infer2D 결과

<img src="https://github.com/fieldcure/WorkReport/assets/40055222/664dc97e-3a82-4b33-924c-9e194ed0b0ec" width="500">
