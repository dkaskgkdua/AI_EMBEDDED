# 논문_Fast_mono_depth_estimation

1. Monocular Depth Estimation 개요
   * **깊이 추정(Depth Estimation)** 은 로봇의 맵핑, 위치 추정, 장애물 회피 등에서 중요한 역할을 합니다.
   * 단일 카메라 기반으로 깊이를 추정하는 방법을 제안하며, 비용 효율적이고 소형화된 솔루션을 제공합니다.
2. 딥러닝 네트워크 구조
   * Encoder-Decoder 구조:
     * Encoder는 MobileNet을 기반으로 하여 채널별로 다른 필터를 사용한 Depthwise 및 Pointwise Convolution을 수행합니다.
     * Decoder는 업샘플링 및 Transpose Convolution을 사용하여 원본 해상도로 복원합니다.
   * Skip Connection: Encoder의 출력을 저장하고 Decoder와 연결하여 공간 정보를 보존하고, 모델의 수렴 속도를 개선합니다.
3. 실험
   * NYU Depth v2 데이터셋을 사용하여 훈련하고, 다양한 성능 지표를 바탕으로 실험을 수행했습니다.
   * Jetson TX2에서 모델을 테스트하여, GPU와 CPU에서의 처리 속도 및 전력 소비를 비교했습니다.
   * Fastdepth 모델은 GPU에서 5.6ms의 짧은 실행 시간과 높은 정확도를 보여줍니다.
4. Ablation Study
   * Encoder: MobileNet, ResNet-50 등 다양한 인코더를 비교해 MobileNet이 낮은 연산량으로 빠른 실행 속도를 보여 최적의 선택으로 평가되었습니다.
   * Decoder: 여러 디코더 구조 중 NNConv5가 가장 효율적인 성능을 보였습니다.
   * Depthwise Separable Convolution을 적용하여 연산량을 줄이고 성능을 최적화하는 실험도 수행되었습니다.
5. 하드웨어 최적화
   * TVM Compiler를 사용하여 하드웨어에 맞는 최적화된 스케줄링을 통해 CPU 실행 시간을 5100ms에서 66ms로, GPU 실행 시간을 19.1ms에서 8.2ms로 단축시켰습니다.
6. 결론
   * 이 연구는 Jetson TX2에서 실시간 성능을 구현하는 저지연 네트워크 아키텍처를 설계하고, 추론 속도를 대폭 개선한 성과를 보여줍니다