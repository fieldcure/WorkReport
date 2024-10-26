# 작업 내용
## 2024-10-21~2024-10-27
### 오토 세그멘테이션 예외 처리 버그 수정
- VOI가 존재하지 않을 때 오토 세그멘테이션 진행되지 않는 문제 해결
- VOI가 존재할 때 VOI가 제거되지 않는 문제 해결
- 바디 오토 세그멘테이션은 같은 예외 처리가 없는데 괜찮은 건가요?
![image](https://github.com/user-attachments/assets/bc4339c8-1d0e-4be9-8af9-eb8a5f2b95f1)
  
### 전극 생성 코드 리팩토링

## 2024-10-14~2024-10-20
### 서버PC(?) 랜섬웨어 걸린 것 같네요
### 전극 생성 코드 리팩토링
- including 정리
- Bouding box 코드 사용하지 않으므로 제거 
- ElectrodePatch 클래스 추가(메탈, 세라믹, 하이드로겔 및 템플릿 전극 관리)
- Debugger 클래스 추가하여 디버깅 코드 분리

- 오버라이드된 함수(CreateElectrodePatch)의 로직이 중복이여서 하나의 함수로 통일<br>
C3DWnd > OnUpdateSpecificElectorde > CreateElectrodePatch 수정해도 문제가 없는지 확인 부탁드립니다
![image](https://github.com/user-attachments/assets/d51fcd4e-f8ac-4e19-8f97-1d9f9054fa1a)

## 2024-10-06~2024-10-13
### 오토 세그멘테이션 클래스 세분화2(autoSeg 클래스)
-> template method 디자인 패턴 적용
![image](https://github.com/user-attachments/assets/c3bbae37-a72d-4cf7-8d17-9d2e7a92e923)

### 전극 하이드->프로그램 재부팅->전극생성 에러 수정완료

## 2024-09-30~2024-10-06
### 오토 세그멘테이션 클래스 세분화(autoSeg 클래스)
![image](https://github.com/user-attachments/assets/b62af445-a3bb-453c-acd1-7dd8b2471c6d)

## 2024-09-23~2024-09-29
### 오토 세그멘테이션 cpu/gpu 자동 로드
-> gpu cuda가 사용할 수 있는 경우에는 gpu를 자동으로 로드, 사용할 수 없는 경우에는 cpu를 자동으로 로드하도록 수정

### 전극 에러확인(원래 코드에서의 에러)
-> 간격이 넓어지면 에러가남(특히 TriangulateFacetsParallel에서)<br>
-> 기존의 코드에서는 x,y축으로만 샘플링하므로 사이드에서 붙이는 전극의 에러는 적을 수 있음(위나 아래에서 붙이는 전극은 x,y의 리졸루션의 영향을 크게 받기 때문에 에러날 가능성이 높아짐)<br>
-> x,y,z축으로 샘플링하는 코드는 z축으로도 샘플링을 하므로, z축 샘플링 간격이 넓어질 경우 사이드에서 붙이는 전극이 영향을 받아 에러가 날 가능성이 높아짐)<br>
![image](https://github.com/user-attachments/assets/fb477ea2-ce0f-4496-9863-9e7231986cd4)

## 2024-09-16~2024-09-22
### 2D/3D/Body Inference 공통 부분 리팩토링
![image](https://github.com/user-attachments/assets/0d711560-dace-4f81-ace1-fc640305e425)

### 신경이 쓰이는 부분(?)
오토 세그멘테이션 결과로 출력되는 VOI의 색상이 너무 비슷해서 구별이 어려운 점이 있음<br>
랜덤으로 색상을 지정하고 있는지 잘 모르겠으나, rbg가 아니라 hsl의 hue 부분을 random 으로 설정하는 방법을 사용하면 색상이 비슷한 문제를 해결할 수 있을 듯<br>
아직 정해진 내용이 아니기 때문에 상의 후 진행
- body 오토 세그멘테이션 결과<br>
![image](https://github.com/user-attachments/assets/57ae14be-862a-4893-bb2e-841df4106f63)
- hsl모델에서 hue 부분만 랜덤으로 적용하여 VOI를 추가한 결과<br>
![image](https://github.com/user-attachments/assets/83f225f5-1bc1-4820-94d0-31a9fb1a42d7)

## 2024-09-09~2024-09-15
### UI 수정
- Study 생성하기 전 클릭하면 프로그램 종료되는 에러 해결
- Head 모델에서는 Head auto segmentation이, Body 모델에서는 Body auto segmentation이 활성화되도록 수정
![image](https://github.com/user-attachments/assets/5eaa3f22-b783-4c56-9144-2aa7296027c5)

### ROIMaker 클래스 함수 세분화
![image](https://github.com/user-attachments/assets/b2f8f474-c4e9-464c-8e20-92f6c5e5446f)

### Study 생성시 만들어지는 Contour 부분
- 기존에 존재하는 자동으로 External Contour 생성하는 코드가 필요한지 잘 모르겠음(헤드 모델의 경우 1분 정도 걸림)
- auto segmentation으로 바꾸는 방법은 생각해봤지만, Head 모델과 Body 모델이 나누어져 있는 점, 그리고 Body 모델에서 external이 출력 결과에 존재하지 않는 점은 고려해서 결정해야 할 듯
  
![image](https://github.com/user-attachments/assets/73fd28e5-c23d-46ed-bbbc-deedd42dbc17)

## 2024-09-02~2024-09-08
### conductivity & Permittivity 계산
--> 주파수 150000(Study에 저장된 기본값)으로 계산한 결과, conductivty & permittivity 값이 문제 없는지 확인 필요
#### GTV
-> 받은 목록에 GTV 속성 값이 존재하지 않음
![image](https://github.com/user-attachments/assets/53a86a12-c020-4974-9088-38d0ecb0136f)

#### 헤드 모델
![image](https://github.com/user-attachments/assets/4589b30c-e9af-464b-affb-cbf80a2c7058)

#### 바디 모델
![image](https://github.com/user-attachments/assets/8b93ecae-3122-42c5-b2f5-f82487b5aaeb)
![image](https://github.com/user-attachments/assets/0ffcad35-6efe-4f86-9969-96e61f052c7f)

### 바디모델 컨투어 추출
![image](https://github.com/user-attachments/assets/c832eeee-69ad-429a-acb7-9eeee592bea5)

## 2024-08-27~2024-09-01
### 메디컬 계산 속도개선(병렬 처리 검증 (2mm에서))
-> 값의 차이가 많이 나므로 병렬처리는 사용하지 않는 것이 맞을 듯(z축으로 resolution 설정하는 코드만 적용해도 1.6mm~10mm까지 계산한 결과의 시간이 나옴)

기존 : 00:16:21.5442381 <br>
CalculateCurrents, AnalyzeVoxels도 병령 처리 :  00:15:46.6076131 / 오리지날 ElectricField01과의 차이값의 합 : 14417.622683560106 <br>
CalculateCurrents, AnalyzeVoxels, InitializeVoxelsParallel의 병렬 처리 : 00:14:59.5028426 / 오리지날 ElectricField01과의 차이값의 합 : 15119.780249248848 <br>
![image](https://github.com/user-attachments/assets/06d3b05f-481b-4ffb-9947-491dfa40e02c)

### 바디모델 오토 세그멘테이션
각 모델 별 결과 샘플<br>
![image](https://github.com/user-attachments/assets/ce1ba7d1-1939-4ebb-9026-795af3437203)

합쳐서 하나의 이미지에서 추출한 결과 샘플<br>
![image](https://github.com/user-attachments/assets/ce6a3f84-df91-4151-a423-fd4f25f3053d)

gpu메모리 사용량&처리시간<br>
![image](https://github.com/user-attachments/assets/eb2ed6f4-1981-4034-9445-b65ca1a85709)

온코필드에서 출력하는 부분 작업중

## 2024-08-20~2024-08-26
### 바디모델 오토 세그멘테이션
온코필드에서 바디 이미지 로드할 수 없음
![image](https://github.com/user-attachments/assets/37e30968-4357-44ec-960c-7f433d57e0d5)
파이썬 코드 확인중

https://github.com/fieldcure/fieldlab-deepedge/blob/3567238a7d99e768ad13c99ff81c70d4f8c52890/deepedge/inferers/inferer_total.py#L784
https://github.com/fieldcure/fieldlab-deepedge/blob/3567238a7d99e768ad13c99ff81c70d4f8c52890/deepedge/inferers/dic_rt.py#L67

### 메디컬 계산 속도개선
병렬처리 -> 결과에 영향이 있으므로 제외<br>
InitializeVoxelsParallel의 병렬 처리가 가장 영향이 크고,<br>
CalculateCurrents, AnalyzeVoxels도 병령 처리에 영향이 다소 있음<br>
속도보다 정확도가 더 중요한 경우는 "레이블맵 z축 resolution 수정"만 적용하는 것이 맞을 듯<br>
![image](https://github.com/user-attachments/assets/3347714d-1ac1-48ba-a884-cba7b5a7ae7b)

## 2024-08-12~2024-08-19
### engraved.poly 확인이 필요할 듯->TriangulateFacetsParallel에서key가 없다고 에러가 남
![image](https://github.com/user-attachments/assets/035e6f9f-9e89-480d-943f-00fe4ba4f408)
![image](https://github.com/user-attachments/assets/f1b511de-4068-4349-bc9d-f8c0f9223159)

### 메디칼 계산 속도개선
CalculateCurrents함수 병렬처리 9초 -> 1.5초 <br>
InitializeVoxelsParallel함수 병렬처리 최적화 18초 -> 8초 (yield return은 한 번만 처리하는 것이 빠름, WithDegreeOfParallelism으로 최대 프로세스를 사용, tetrahedron도 병렬처리) <br>
AnalyzeVoxels함수 병렬처리 11초 -> 3초 <br>

#### Smoothing 평균 곡률 변화량 측정하여 정지 조건 설정
인터섹션 체크하는 부분을 수정해야할 듯

#### depth resolution도 적용한 결과 (256x256x256 헤드)
~ 1.6mm : 전기장 계산에서 시스템 메모리 용량(32GB)를 초과하는 공간을 요구하여 계산 딜레이가 발생하므로 속도 확인에는 의미가 없음<br>
1.6mm : 01:47:22.2549589(메쉬 25분/전기장 계산1 20분/전기장 계산2 1시간) -> 메모리 32기가인데 전기장 계산 2번 째부터 메모리 차지하는 영역이 40기가가 넘어서 계산 딜레이 발생<br>
1.7mm : 00:29:45.5238958<br>
1.8mm : 00:12:20.4134863<br>
2.0mm : 00:07:14.7022259<br>
3.0mm : 00:03:24.4200601<br>
4.0mm : 00:02:21.7411175<br>
5.0mm : 00:01:48.6029094<br>
6.0mm : 00:01:46.6005471<br>
7.0mm : 00:01:37.0357475<br>
8.0mm : 00:01:34.5769245<br>
9.0mm : 00:01:25.5644573<br>
10.0mm : 00:01:38.8276500<br>

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
