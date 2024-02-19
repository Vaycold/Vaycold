# OD-SHEILD
PyTorch Implementation of __OD-SHIELD__

## Datasets
OD-SHEILD를 학습하기 위해 총 3가지의 데이터셋(COCO DATASET, VISDRONE DATASET, ARGOVERSE DATASET)을 사용하였다. COCO DATASET은 여러 객체가 포함된 데이터셋인 반면, ARGOVERSE DATASET과 VISDRONE DATASET은 교통 상황에서의 데이터셋이다. 따라서 OD-SHIELD는 자율 주행상황에서의 공격이 들어왔을 때 효과적으로 방어하기 위한 기법이기 때문에 COCO DATASET의 CLASS를 4개(HUMAN, CAR, TRUCK, BUS)로 줄여서 실험을 진행하였다(해당 처리코드는 첨부돼있지 않음). 너는 _다운로드.sh_ 만 실행하게 되면 주어진 경로로 데이터 셋이 다운로드가 될 것이고, OD-SHIELD를 학습하기 위해서 다운받은 데이터셋이 ./XXXX 폴더 내에 하위폴더로 ./XXXX/images, ./XXXX/labels로 있으면 준비는 끝났다.
```
./다운로드.sh
```
## Training 
OD-SHILED는 train.py를 통해 각기 다른 argument를 추가함으로써 실험의 다양성을 제공한다. 데이터셋의 이미지 파일 경로와, 라벨 파일의 경로는 각각 --data_path, --label_path 뒤에 인자로 받는다. 뿐만 아니라 데이터셋에 대한 배치사이즈, 학습률, 반복수는 --bs, --lr, --epochs 뒤의 인자로 주어 각각의 환경에 맞게끔 실험을 실시할 수 있다. 학습된 모형은 --checkpoint_path 경로로 저장이 되며, 기본적으로 100번의 반복마다 모델 학습이 저장된다. 해당 모형이 학습되는 과정을 텐서보드로 시각화를 하고 싶다면 --visualize 값을 준 후 --log_path에서 해당 학습 기록을 로그파일 형식으로 받아볼 수 있다. 

## Patchs
OD-SHILED는 여러 가지 패치를 학습에 사용한다. 해당 패치들의 경로는 ./패치 이며 여기에 있는 패치들을 무작위로 선택하여 학습에 사용된다. 사용자는 학습에 사용될 커스텀 패치가 따로 있을 경우, train.py 의 --patch_paths 경로에 커스텀된 패치들의 경로를 넣어주면 된다.다음은 예시 학습코드 파일이다. 

```
train.py --bs 16 --lr 0.001 --epochs 1200 --gpu_id 0
```
    parser.add_argument('--bs', action='store', type=int, default = 2, required=False)
    parser.add_argument('--lr', action='store', type=float, default = 0.0001, required=False)
    parser.add_argument('--epochs', action='store', type=int, default = 700, required=False)
    parser.add_argument('--gpu_id', action='store', type=int, default=0, required=False)
    
    parser.add_argument('--checkpoint_path', action='store', type=str, default = './checkpoints/', required=False)
    parser.add_argument('--log_path', action='store', type=str, default = './logs/', required=False)
    parser.add_argument('--visualize', action='store_true')
    
    parser.add_argument('--data_path', default='/Data1/hm/DRAEM_TRAIN_DATASET/argoverse/images') # modify the dataset images path
    parser.add_argument('--label_path', default='/Data1/hm/DRAEM_TRAIN_DATASET/argoverse/labels') # modify the dataset labels path
    parser.add_argument('--patch_paths', default='/Data1/hm/OD_SHIELD/yolov5_adversarial/patch/patch_sample') 

    args = parser.parse_args()

    with torch.cuda.device(args.gpu_id):
        train_on_device(args)
