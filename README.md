# OD-SHEILD
PyTorch Implementation of __OD-SHIELD__

## Datasets
OD-SHEILD를 학습하기 위해 총 3가지의 데이터셋(COCO DATASET, VISDRONE DATASET, ARGOVERSE DATASET)을 사용하였다. COCO DATASET은 여러 객체가 포함된 데이터셋인 반면, ARGOVERSE DATASET과 VISDRONE DATASET은 교통 상황에서의 데이터셋이다. 따라서 OD-SHIELD는 자율 주행상황에서의 공격이 들어왔을 때 효과적으로 방어하기 위한 기법이기 때문에 COCO DATASET의 CLASS를 4개(HUMAN, CAR, TRUCK, BUS)로 줄여서 실험을 진행하였다(해당 처리코드는 첨부돼있지 않음). 너는 _다운로드.sh_ 만 실행하게 되면 주어진 경로로 데이터 셋이 다운로드가 될 것이고, OD-SHIELD를 학습하기 위해서 다운받은 데이터셋이 ./XXXX 폴더 내에 하위폴더로 ./XXXX/images, ./XXXX/labels로 있으면 준비는 끝났다.
```
DSSD
```
