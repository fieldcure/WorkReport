# 작업 내용

## 2024-06-25~30
소스 코드 확인 중

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
