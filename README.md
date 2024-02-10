## 목표 스케줄

### 2024-02-19~2024-02-25
### 2024-02-12~2024-02-18
- [ ] 테스트?

## 작업 내용

### 2024-02-05~2024-02-11

전극 생성은 하이드로겔, 세라믹, 메탈을 나누어서 직육면체 혹은 실린더를 생성하는 방식으로 바뀌었습니다.
전극이 사각형인 경우에는 one patch의 생성 방식과 동일하게 4개의 꼭지점을 찾은 후 두 쌍의 꼭지점 사이의 거리를 조밀하게 subdivision 한 후 인체의 3d object 데이터에 projection하는 방식을 사용합니다.

- [x] 전극 on/off처리
- [x] 종료시 에러라는 부분 수정
- [x] 필요 없는 함수 제거
- [x] 포인터 해제 처리
- [x] one patch(코드 좀 더 정확하게 개선)
- [x] 전극 intersection 체크 부분 수정
- [x] 코드 정리 & 주석 추가

- vtk의 들로네 삼각형이 기능이 별로여서 그냥 따로 만듦(포인트 subdivition -> 인체에 progection -> 삼각형화)
- 현재는 0.05mm 간격으로 포인트를 생성하고 있음-> 좀 더 resolution을 높이고 싶으면 간격 설정을 줄이면 됨
<br><img src="https://github.com/fieldcure/WorkReport/assets/40055222/d96b0eb0-d4ee-4326-b168-c047e86050d3" width="400">
<br><img src="https://github.com/fieldcure/WorkReport/assets/40055222/f1a4fa89-1787-4214-8c2e-ce46a0da8825" width="400">

### 2024-01-22~2024-02-04
- 클릭시 보이는 전극(템플릿), 회전&이동 함수 연동중
- one patch도 성능 개선을 위해 코드 수정중
- [x] 사각형 전극(템플릿)
- [x] 원형 전극(템플릿)
- [x] one patch(템플릿)
- [x] 사각형 전극, 원형 전극, one patch(이동&회전)
- [x] one patch(코드 개선)

- hydrogel one-patch(?)를 사용한 경우(임의의 값을 집어 넣어 테스트 함)
 ->사각형, one-patch의 경우 경계선을 구하여 들로네2D 적용(기존의 코드가 시간이 오래 걸려서 심플하게 패치를 만들 수 있도록 수정.)
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/0e919fff-8e3a-4551-86c7-3846a632c9ad" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/18cac37c-732d-4569-9ca8-836b10a2ea0a" width="400"></td>
</table>
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/d49f2c2c-de5e-4b2c-9319-7fce38a2f5fc" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/9a179799-2ea3-47fc-ad2b-c68f999b7c0a" width="400"></td>
</table>

- 헤드 모델 없앤 후의 모습
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/f8290264-c99b-4a80-82e3-44ccce595036" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/faf90da0-3104-4d3a-95cc-4eef6162f772" width="400"></td>
</table>

- translation
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/8a55bde9-8fbe-48a4-b63e-3a511cd43ada" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/84bdb0a3-c12b-49b0-b0fe-a3c58484bfb7" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/3392fd07-c9fa-4fd9-bed3-85fdb5b418f6" width="400"></td>
</table>

- rotation
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/5ecd526c-1b2c-4415-b645-8da2ae21723c" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/f14159f6-5eeb-4370-86a4-947eac5c25ee" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/083dc583-7782-470f-ab74-dab6c635abf5" width="400"></td>
</table>

- 직각으로 파고드는 메쉬(ㄱ 모형으로 파고드는 부분)에는 전극이 살짝 묻히는 현상이 있으므로 시간이 있으면 개선 예정(직각인게 말이 안되서 굳이 해당 경우를 예외 처리 해야하나 싶은 생각은 있지만...)





### 2024-01-15~2024-01-21
- 코드 정리(함수 인자가 너무 많아서 클래스 작성)
- OncoField 적용 시작 -> [https://github.com/hwkim0325/fieldlab-oncofield](https://github.com/hwkim0325/fieldlab-oncofield/tree/OncoField1.2(KFDA))
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/ae85ceb3-4242-4b5a-b480-74a0fd5c4547" width="400">

- 전극 사이즈가 커서 임의로 조절해서 헤드에서 작업중
- 이외의 질문 사항 월요일 오전에 전달 예정
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/e4c7a565-b080-4494-bf8f-ea64b2b12215" width="700">

- 사각형 전극(사이즈는 임의로 조절해서 작업중)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/b12b164f-4f8a-425d-8a1a-c5815ceee876" width="700">

- 하이드로겔의 width, height가 ceramic or copper보다 살짝 큰 값이 들어가 있어서, 값 수정이 필요할 것으로 보임. -> 전달 예정
- 좀 더 심플한 방법도 생각 중(tolerance의 조정으로 좀 더 정확한 patch를 만들 수 있지만 시간이 오래걸림)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/b04600cf-92a4-4c98-a08e-b44d42dc05ff" width="700">


### 2024-01-09~2024-01-14
- transducer array set의 개수(row m개, column n개)에 대응하여 각 transducer array set의 위치 확인 및 생성 완료(정확한 노말 계산은 온코필드에서 적용 예정)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/d3a832db-19a8-4161-844b-82e95a6ee2d1" width="400">

### 2024-01-06 ~ 2024-01-08
- 전극을 부착할 표면이 매끄럽지 않은 경우를 대비하여, 전극 중심점에서 평면을 생성하여 일정 거리 내부에 존재하는 점들이 적절한 방향으로 projection되는지 확인.
  projection 방향에 문제가 있으면 중심점을 surface로 부터 멀어지도록 이동. (전극의 두께도 고려하여 이동시킴)
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/93a8fb2f-1a43-4d8d-a266-d378fd7b309e" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/cd18c4c3-2777-4dd1-b969-939e00f3a733" width="400"></td>
</table>

- 실린더 전극 작성, 중심점을 기준으로 회전을 통해 점들을 생성하고 메쉬를 생성
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/8dffd39d-7691-456a-9ff8-1ea5aebe98d3" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/b8defd8f-69b9-40e7-9c95-f08dc3cb4688" width="400"></td>
</table>

- 사각형 전극 작성, 각 꼭지점을 회전을 통해 점들을 생성하고 메쉬를 생성, cos, sin을 이용해 점을 생성하는 방법은 오차가 존재함(라디안 계산이므로 오차가 생각보다 큼), 사각형의 대각선 길이를 이용해 각 꼭지점을 생성하고 그 사이의 점을 메꾸는 방향이 적절할 듯
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/a3919e44-c524-425e-81d0-f5bdba730125" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/51f9ffff-360b-4b1a-987a-61a898504610" width="400"></td>
</table>

- hydrogel patch가 onePatch(?)가 아닌 경우도 대응, 하이드로겔, 세라믹, 메탈 순으로 전극 생성 가능, 층이 올라 갈 수록 반지름이 작아지거나 같은 경우는 메쉬에 오류 없이 지원.(역순의 경우에는 뷰어에서는 문제가 없지만 실제 계산에서는 intersection 있을 수 있음)
<table>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/abe3def4-5c80-46cd-b012-cbeb1332456c" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/e9b41f41-d7db-4ab8-a490-db9506ab4660" width="400"></td>
</table>

- hydrogel patch를 만들 때 계산한 포인트를 이용하여, 패치 내부의 전극 중심점을 계산
<table>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/b3285190-c2c9-43f7-b2f7-06f0b14884ce" width="400"></td>
           <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/cfceb88f-d208-4237-8d7c-e7a21ed80655" width="400"></td>
</table>


### ~2024-01-05
- 표면을 따라가며 distance 계산
1. U, V 벡터가 존재할 때, Transducer Array의 U or V벡터 방향으로 진행
3. surface 표면에 projection
4. normal 벡터 계산
5. bitangent 벡터 계산
6. 이전의 포인트와 1.을 통해 진행한 포인트로 다음 진행 방향 계산(tangent 벡터 계산)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/eea8cd63-592b-47cb-8769-74196925d327" width="400">

- 각 포인트의 bitangent 방향으로 포인트를 추가생성
(패치 중심을 기준으로 upper-right/lower-left/lower-right/upper-left 순)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/a0dd8168-5b04-4f7b-9153-e981ff093606" width="400">

- 반시계 방향으로 삼각형 패치 생성(1차 시도)
1. 중심부
2. upper-right/lower-left/lower-right/upper-left 순으로 삼각형화(십자 모형의 base point와의 연결(x 기호) + 패치 삼형화(ㅁ기호)) <br>
// |xㅁㅁㅁㅁ<br>
// |xㅁㅁㅁㅁ<br>
// |xxxxxxxx<br>
// ㅡㅡㅡㅡㅡ<br>

<table>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/9d183b2b-309d-49e1-87ef-78b8eec6a131" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/430e8be2-1322-48c8-af29-ffcd5c378253" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/cf7220d0-0484-44fa-98a7-c0eeadc2c958" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/43458f44-af24-4e12-875c-6a9db68bbf99" width="400"></td>
</table>

- 검증 -> (표면이 매끄러운 경우)면적을 계산하여 직사각형의 패치의 넓이와 비교한 결과 98.75%의 면적을 보존하였으나,
          표면이 매끄럽지 않은 경우 거리 계산에 오류가 있음을 확인함(당연한 결과이지만 구현 후 확인 함,
          패치의 거리 계산 방법이, 1. V벡터로 위아래 포인트 생성, 2. ㅣ 모양의 포인트들의 bitangent vector를 이용해 좌우로 포인트를 생성
          이기 때문에, ㅣ 모양의 포인트의 한 지점에서 계산한 좌우 거리가, 상하의 거리에는 영향을 주지 못함.)
(첫번째-좌우로 밖에 영향을 받지 않는 surface mesh, 두번째-delaunay삼각형을 이용하여 굴곡에 인해 수축하는 현상을 제거 -> 수축을 고려하여 작성하려면 미소 사각형을 확장시키는 방법으로 거리를 측정할 필요가 있어 보임(예상))
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/b60b57ef-61d8-464e-b7d1-f40291c5fdb4" width="400">

- 2차 시도 -> 중심점을 기준으로 360도를 돌며, 정해진 거리를 계산하여 시도해 보았지만, 위에 언급한 문제는 해결하지 못할 것으로 예상(중심점에서 포인트를 생성하기 위해 진행한 방향에서 굴곡진 부분이 존재하면, 해당 방향의 길이는 짧아지지만, 다른 부분에는 영향을 주지 못함)
             또한, cos과 sin을 이용하여 직사각형 위에서 중심점과의 거리를 계산했지만 floating error가 있을 수 있다고 판단함(확실하지는 않음)

- 3차 시도 -> 처음 만든 패치에서 장애물이 있는(굴곡이 있는) 부분의 좌우로만 영향을 받았서, 좌우로의 영향을 없애는 방향으로 바꿈(Convex triangulation -> Delaunay triangulation 2D를 이용해 삼각형화를 시도)
           -> 좀 더 의미 있는 패치를 만들기 위해서는 단위길이(u,v 진행)의 미소 사각형을 이어 붙이는 방식으로 만드는 방법, 혹은 패치를 붙일 타겟 surface mesh의 곡면을 완만하게 만드는 방법(surface mesh 데이터가 손실 되지만)이 있다고 생각해 보았지만,
              추후 필요하다고 판단될 경우 작업을 진행하기 위해서 일단 보류

(투명하게 비춰지는 부분은 z-fighting)
<table>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/c763c6e8-57b0-4262-a06e-0d80aad11570" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/3ab9be09-3cde-4a0b-af3c-f53487b11a03" width="400"></td>
</table>

- 패치 중심의 노말 방향으로 hydrogel의 높이만큼 두께 생성
<table>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/cb89d354-b330-4361-ba1d-af9bd01f810d" width="400"></td>
          <td><img src="https://github.com/fieldcure/WorkReport/assets/40055222/449772e8-5d9a-4d7a-9c87-44bb69493052" width="400"></td>
</table>
