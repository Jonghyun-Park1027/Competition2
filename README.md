# AIFactory 위성영상을 활용한 컨테이너 탐지

## 23. 7. 20. ~ 23. 7. 26. Yolo v8m 모델을 활용한 Object Detection 모델 작성(최종순위 : 19등)

> ## 전략 및 아이디어
>
> <p align="center"><img src="images/계통도.png" width="100%" height="100%"></p>
> 
> github : https://github.com/Jonghyun-Park1027/competition2
> ## 분석 모델
> ### 1. 개요
> - 본 공모전은 Pretrained weight / Pretrain 모델 사용을 금지함 따라서 필요 데이터를 구해 직접 Pretrain 모델을 작성해야함.
> - Yolo v8m을 통한 Object Detection 모델 학습 및 추론
> - Pretrain Model : 공공데이터포털 위성영상 객체판독의 빌딩, Object dataset의 3379장의 png파일 및 labeling data
> - Finetuning : AIFactory 주최측 제공 데이터셋의 272장의 png파일 및 labeling data
>  
> ### 2. 분석 과정
>
> - Train Dataset을 4:1 = Train:Valid 로 나누어 모델 학습
> - geojson 파일을 Yolo v8 모델에 맞는 형식으로 치환하기 위해 xyxy 형식을 바운딩 박스의 4개 모서리 형태로 전처리
> - cv2, matplotlib, os 등의 라이브러리를 적극 활용하여 코드 실행만으로 자동화된 전처리가 가능하도록 노력함.
> 
> ## 분석 결과 (Conf >= 0.1, IOU >= 0.5)
> 
> ### 1. Confusion Matrix
> <p align="center"><img src="images/confusion_matrix.png" width="100%" height="100%"></p>
>
> 
> 
> ### 2. Label, Prediction 비교 예시(사진)
> - Label
> <p align="center"><img src="images/val_batch2_labels.jpg" width="100%" height="100%"></p>
> - Prediction
> <p align="center"><img src="images/val_batch2_pred.jpg" width="100%" height="100%"></p>
>
> ### 3. 종합 결과
> <p align="center"><img src="images/PR_curve.png" width="100%" height="100%"></p>
>
> <p align="center"><img src="images/results.png" width="100%" height="100%"></p>
>
> - Pretrain의 Test에 대한 AP : 0.446 / Submission AP : 0.0257
> 
>
## 결론 및 제언 
### 1. 사용된 데이터의 부족
 - 데이터 증강을 위한 방법론 적용(Crop, Rotate 등) 및 Roboflow를 통한 커스템 데이터셋을 작성하였으나, 시간 부족으로 모델 학습에 사용하지 못함.
### 2. 과대적합 및 적절한 Dataset 선정 필요
 - Finetuning이 미세한 성능향상을 이뤘으나, Pretrain Model부터 좋지 않은 정확도를 보였다. 오히려 Finetuning 없이 파라미터를 높힌 Yolo v8m 모델이 좋은 성능이 나옴.
### 3. 다양한 모델링 기법 사용 필요
 - 단적으로 이번 모델은 최초 Yolo v8n을 사용했지만 Yolo v8m을 사용하면서 파라미터 수를 높힌 것이 가장 주요했음.
 - 그러나 과대적합 및 제대로 된 Pretrain 모델을 작성하지 못함.
 - Pretrain 및 Finetuning도 상황에 맞춰 더 다양한 방법을 적용해보는 것이 필요함.