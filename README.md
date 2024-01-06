# 2023-12-29~2024-01-05 (휴일이여서 작업할 시간이 있었음..)
- 표면을 따라가며 distance 계산
1. U, V 벡터가 존재할 때, Transducer Array의 U or V벡터 방향으로 진행
3. surface 표면에 projection
4. Normal 벡터 계산
5. bitangent 벡터 계산
6. 이전의 포인트와 1.을 통해 진행한 포인트로 다음 진행 방향 계산(tangent 벡터 계산)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/eea8cd63-592b-47cb-8769-74196925d327" width="500">

- 각 포인트의 bitangent 방향으로 포인트를 추가생성
(패치 중심을 기준으로 upper-right/lower-left/lower-right/upper-left 순)
<img src="https://github.com/fieldcure/WorkReport/assets/40055222/a0dd8168-5b04-4f7b-9153-e981ff093606" width="500">

- 반시계 방향으로 삼각형 패치 생성
1. 중심부
2. upper-right/lower-left/lower-right/upper-left 순으로 삼각형화(십자 모형의 base point와의 연결(x 기호) + 패치 삼형화(ㅁ기호)) <br>
// |xㅁㅁㅁㅁ<br>
// |xㅁㅁㅁㅁ<br>
// |xxxxxxxx<br>
// ㅡㅡㅡㅡㅡ<br>

- 검증 -> (표면이 매끄러운 경우)면적을 계산하여 직사각형의 패치의 넓이와 비교한 결과 98.75%의 면적을 보존하였으나,
          표면이 매끄럽지 않은 경우 거리 계산에 오류가 있음을 확인함(당연한 결과이지만 구현 후 확인 함,
          패치의 거리 계산 방법이, 1. V벡터로 위아래 포인트 생성, 2. ㅣ 모양의 포인트들의 bitangent vector를 이용해 좌우로 포인트를 생성
          이기 때문에, ㅣ 모양의 포인트의 한 지점에서 계산한 좌우 거리가, 상하의 거리에는 영향을 주지 못함.)

- 2차 시도 -> 중심점을 기준으로 360도를 돌며, 정해진 거리를 계산하여 시도해 보았지만, 위에 언급한 문제는 해결하지 못할 것으로 예상(중심점에서 포인트를 생성하기 위해 진행한 방향에서 굴곡진 부분이 존재하면, 해당 방향의 길이는 짧아지지만, 다른 부분에는 영향을 주지 못함)
             또한, acos과 asin을 이용하여 직사각형 위에서 중심점과의 거리를 계산했지만 floating error가 있을 수 있다고 판단함(확실하지는 않음)

- 3차 시도 -> 처음 만든 패치에서 장애물이 있는(굴곡이 있는) 부분의 좌우로만 영향을 받았서, 좌우로의 영향을 없애는 방향으로 바꿈(Convex triangulation -> Delaunay triangulation 2D를 이용해 삼각형화를 시도)
           -> 좀 더 의미 있는 패치를 만들기 위해서는 단위길이(u,v 진행)의 미소 사각형을 이어 붙이는 방식으로 만드는 방법이 있다고 생각해 보았지만, 


