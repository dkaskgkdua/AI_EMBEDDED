# CNN
CNN(Convolutional Neural Network)은 이미지, 비디오 처리와 같은 시각적 데이터 분석에 주로 사용되는 딥러닝 모델입니다. CNN은 이미지의 공간적 특성을 효율적으로 처리하기 위해 설계되었으며, 주로 Convolution Layer, Pooling Layer, Fully Connected Layer로 구성됩니다.
![image_1.png](image_1.png)

## Convolution Layer
Convolution Layer는 이미지에서 특징을 추출하는 역할을 합니다. 필터(커널)를 사용하여 입력 이미지에서 작은 영역을 슬라이딩하며, 각 필터는 특정 패턴이나 경계를 감지할 수 있습니다. 이렇게 추출된 특징 맵은 이미지의 중요한 정보(엣지, 모서리 등)를 학습할 수 있게 도와줍니다. 이 층에서는 다음 두 가지 중요한 개념이 있습니다:
Stride(스트라이드): 필터가 이미지를 슬라이딩할 때 이동하는 간격입니다. 큰 스트라이드를 사용하면 출력 크기가 줄어들며 더 빠르게 계산할 수 있지만, 작은 세부 정보는 놓칠 수 있습니다.
Padding(패딩): 이미지 가장자리에서 특징을 잃지 않기 위해 경계에 0을 추가하여 출력 크기를 조정할 수 있습니다.
![image_2.png](image_2.png)

## ReLU(Rectified Linear Unit)
ReLU는 활성화 함수로, Convolution Layer와 Fully Connected Layer에서 주로 사용됩니다. ReLU는 비선형성을 도입하여 모델이 더 복잡한 패턴을 학습할 수 있도록 도와줍니다. ReLU 함수는 입력 값이 0보다 크면 그대로 출력하고, 0보다 작으면 0으로 출력합니다. 수식으로 표현하면 다음과 같습니다:
![image.png](image.png)
이 함수는 학습 속도를 높이고, 기울기 소실 문제(vanishing gradient problem)를 완화하는 데 기여합니다.

## Norm Layer
**Batch Normalization (BN)**은 미니배치 단위로 입력값을 정규화하여 신경망의 훈련을 빠르고 안정적으로 만들어 줍니다. 정규화를 통해 활성화 함수로 들어가는 값의 분포를 일정하게 만들어, 학습 중 값들이 너무 크거나 작아지지 않도록 조정합니다. 이를 통해 기울기 소실(vanishing gradient)이나 폭발(exploding gradient) 문제를 완화할 수 있습니다.

## Pooling Layer
Pooling Layer는 특징 맵의 크기를 줄여 계산량을 줄이고, 중요한 특징을 유지하면서 불필요한 정보를 제거합니다. 일반적으로 Max Pooling(최대 풀링)이 사용되며, 이 방법은 특정 영역에서 최대 값을 선택하여 출력하는 방식입니다. 풀링은 모델의 복잡도를 줄이고 과적합(overfitting)을 방지하는 데 도움을 줍니다.

## Flatten Layer
Flatten Layer는 Convolution Layer 및 Pooling Layer에서 출력된 다차원 데이터를 1차원 벡터로 변환하는 역할을 합니다. 이는 Fully Connected Layer로 데이터를 전달하기 위한 준비 과정입니다. 이미지 데이터를 처리하는 CNN은 다차원 특징 맵을 출력하기 때문에, 이를 FC(완전 연결) 층에 전달하려면 1차원으로 변환해야 합니다.

## Fully Connected Layer
Fully Connected Layer는 네트워크의 마지막 부분에 위치하며, Convolution과 Pooling을 통해 추출된 특징들을 이용해 최종적으로 분류 또는 회귀 작업을 수행합니다. FC Layer에서는 모든 입력 뉴런이 다음 층의 모든 뉴런과 연결됩니다. 이 층은 CNN이 특정 클래스에 속할 확률을 계산하거나 다른 예측 작업을 수행할 수 있도록 합니다.


## 자주 사용하는 기법들
아래와 같은 이유 때문에 기법들이 필요로 함
* 비싼비용
* 죽은 채널들
* 채널 간 상관관계가 낮음

### Residual Connection
ResNet(Residual Networks)에서 소개된 개념으로, 딥러닝 모델이 너무 깊어질 때 발생하는 기울기 소실(vanishing gradient) 문제를 해결하는 데 사용됩니다. 이는 두 레이어를 직접 연결하지 않고, 입력을 출력에 더하는 방식으로 구현됩니다. 
* 동작 원리: ![image_3.png](image_3.png)
이 방식은 입력을 그대로 다음 레이어로 넘기므로, 모델이 더 깊어져도 성능 저하가 적고, 학습이 더 원활하게 이루어집니다.
* 장점: 매우 깊은 네트워크도 효율적으로 학습 가능하며, 성능이 개선됩니다. 

### Point-wise Convolution
1×1 커널을 사용하는 특수한 합성곱 연산입니다. 이는 각 픽셀의 채널 정보를 결합하는 데 사용됩니다.
* 용도:
  * 주로 채널 간의 정보를 결합하는 데 사용되며, 계산 비용이 적습니다.
  * 다른 합성곱 연산과 결합하여, 신경망의 복잡도를 줄이면서 성능을 유지하는 데 도움을 줍니다.

### Grouped Convolution
Grouped Convolution은 필터를 여러 그룹으로 나누어 각 그룹에 대해서 별도의 합성곱 연산을 수행하는 기법입니다. AlexNet과 ResNeXt에서 처음 제안되었습니다.
* 동작 원리:
  * 전체 입력 채널을 여러 그룹으로 나누고, 각 그룹에 독립적으로 합성곱을 수행합니다.
  * 예를 들어, k개의 그룹으로 나누면, 필터도 k개의 그룹으로 나뉘고 각 그룹에 독립적인 합성곱을 수행합니다.
* 장점: 계산량을 줄이고 메모리 효율을 높이면서도 성능을 유지할 수 있습니다.

### Depth-wise Convolution
Depth-wise Convolution은 각 채널에 대해 독립적인 필터를 적용하여 합성곱을 수행하는 방식입니다. 이 방식은 모든 채널에 동일한 필터를 적용하는 일반적인 합성곱과 달리, 채널별로 필터를 따로 적용합니다.
* 동작 원리:
  * 입력의 각 채널에 대해 별도로 합성곱을 수행하여 특징을 추출합니다.
  * 필터는 채널당 하나씩 독립적으로 적용되며, 이 과정에서 출력의 채널 수는 입력 채널과 동일하게 유지됩니다.
* 장점: 계산량을 크게 줄이면서도 효율적으로 특징을 추출할 수 있습니다.

### Depth-wise Separable Convolution
Depth-wise Separable Convolution은 Depth-wise Convolution과 Point-wise Convolution을 결합한 방식으로, Xception과 MobileNet에서 많이 사용됩니다. 이 기법은 계산 효율성을 극대화하는데 중점을 둡니다.
* 동작 과정:
  * Depth-wise Convolution으로 각 채널에 대해 독립적인 합성곱을 수행하여 특징을 추출합니다.
  * Point-wise Convolution으로 1×1 합성곱을 사용해 각 채널 간의 정보를 결합합니다.
* 장점: 표준 합성곱에 비해 계산량을 크게 줄일 수 있으며, 성능 손실이 거의 없습니다.

### Stacked Filter
Stacked Filter는 여러 개의 작은 필터(예:3×3)를 쌓아서 더 큰 필터(예:5×5 또는 7×7)의 효과를 내는 방식입니다. 큰 필터를 사용하는 대신 작은 필터를 여러 번 적용하면 더 적은 파라미터로 비슷한 표현력을 얻을 수 있습니다.
* 예시: 
  * 3×3 필터 두 개를 쌓으면 5×5 필터와 비슷한 표현력을 가질 수 있습니다.
  * 3×3 필터 세 개를 쌓으면 7×7 필터와 비슷한 효과를 얻습니다.
* 장점: 파라미터 수가 적어지며, 더 깊은 네트워크에서 비선형성의 이점을 얻을 수 있습니다.

### Global Average Pooling
**Global Average Pooling (GAP)**은 마지막 합성곱 층 이후에 사용되며, 각 채널의 공간적 정보를 평균내어 1차원 벡터로 변환하는 기법입니다. 이는 전통적인 Fully Connected Layer를 대체할 수 있습니다.

* 동작 원리: 각 채널에 대해 공간적으로 평균을 내어 하나의 값으로 압축합니다. 이를 통해 전역적인 특징을 추출할 수 있습니다.
* 장점:
  * 파라미터 수를 크게 줄여 과적합(overfitting)을 방지합니다.
  * Fully Connected Layer를 사용하는 대신, 파라미터가 없는 단순한 연산으로 글로벌 정보를 학습할 수 있습니다.
* 사용 예시: **GoogLeNet (Inception Network)**와 같은 최신 네트워크에서 사용됩니다.