# 작업 내용

## 2024-08-12~2024-08-19
### 메디칼 계산 속도개선
CalculateCurrents함수 병렬처리 9초 -> 1.5초
InitializeVoxelsParallel함수 병렬처리 최적화 18초 -> 8초 (yield return은 한 번만 처리하는 것이 빠름, WithDegreeOfParallelism으로 최대 프로세스를 사용, tetrahedron도 병렬처리)
AnalyzeVoxels함수 병렬처리 11초 -> 3초

#### TriangulateFacetsParallel 버그 수정

#### 3mm resolution(width/height) + 3장씩 체크 
3분으로 줄임

#### 2mm resolution(width/height) + 2장씩 체크 
6분 -> 마지막에 파일 작성이 1분 30초 정도 걸림(필요한 데이터만 저장하는게 좋을지도?)

![image](https://github.com/user-attachments/assets/8030e688-f13f-4ab4-a5e5-1e4b060d0eca)

## 2024-08-04~2024-08-11
### 바디모델
용하에게 onnx 모델 요청함
어떻게 작업할지 코드 확인

### 메디칼 계산 속도개선 확인중(medical/data1/ 폴더에 존재하는 헤드 모델로 확인)

대략적으로 전극 부착 완료까지 30초 전기장 계산+파일 저장이 1분 정도 걸림(계속 확인중)


#### 5mm resolution(width/height)

![image](https://github.com/user-attachments/assets/545be85a-2759-42b2-8dc3-651d4a6a1563)

#### 5mm resolution(width/height) + 5장씩 체크(slice)

![image](https://github.com/user-attachments/assets/fe05f7ea-fe48-4f5b-be28-2ff7983ff9d3)
![image](https://github.com/user-attachments/assets/405ca5e9-f59d-47fc-84fb-4e64c2b3cb36)
![image](https://github.com/user-attachments/assets/a751782f-0eeb-4425-95ff-c7343021100d)


#### 10mm resolution(width/height) + 10장씩 체크(slice)

![image](https://github.com/user-attachments/assets/f6ab6512-7473-4394-8f13-11a88b94bff1)
![image](https://github.com/user-attachments/assets/09d14d7d-6769-4420-b165-87642e5fbe0f)
![image](https://github.com/user-attachments/assets/8fa6ea7d-3ac5-40f5-8413-724ad51d0723)

#### 5mm resolution(width/height) + 15장씩 체크(slice) -> 10장 이상씩 체크하면 너무 경사지게 만들어져서 에러가 날 가능성이 보임(전극 부착 실패 등)

![image](https://github.com/user-attachments/assets/8781ec76-6c37-4d5b-af29-35cf09e35e8b)
![image](https://github.com/user-attachments/assets/3370e10f-b1bf-4c72-be5f-7bfd0c1443e3)
![image](https://github.com/user-attachments/assets/35212e0d-6114-4ca5-8a3d-867eb31b2984)

#### qa40 스위치 제거하면 꽤 빨라짐
5mm resolution(width/height) + 15장씩 체크(slice)의 데이터의 경우 50초 정도 빨라짐 -> coarse일 경우에는 qa 스위치 제거하는 것도 방법일 수도 있을 것 같음(삼각형이 커지면 결과가 이상하게 보일 수는 있을 듯)

## 2024-07-29~08-04
### 이미지 외곽에 선 나오는 버그 해결
### GTV 적용할 수 있도록 수정

![image](https://github.com/user-attachments/assets/f5b4091b-678a-44a3-b8f1-2e66ea0e32cd)

### 256사이즈가 아닌 데이터에서 동작하도록 수정
(288, 384, 192)로 테스트함 -> release모드에서 adaptiveHistogram 적용할 필요가 있으나, debug 모드에서는 itk가 굉장히 오래 걸리기 때문에 빼 두었음
용하 코드로 동작하는지 확인할 필요가 있어보임(gtv적용할 때)

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
