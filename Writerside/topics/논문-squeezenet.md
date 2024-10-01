# 논문_squeezenet

1. SQUEEZENET: ALEXNET-LEVEL ACCURACY WITH 50X FEWER PARAMETERS
   * SqueezeNet은 AlexNet과 비슷한 정확도를 유지하면서 50배 적은 파라미터를 사용하여 모델을 경량화한 신경망 구조입니다. 이 구조는 특히 모델 크기와 메모리 효율성을 강조합니다.
2. Introduction
   * 최근 CNN의 정확도를 높이기 위한 연구가 진행되고 있으며, 작은 CNN 아키텍처가 여러 가지 이점을 제공함.
   * SqueezeNet의 주요 장점은 다음과 같습니다:
     * 50배 적은 파라미터로 AlexNet 수준의 정확도를 달성.
     * 모델을 압축하여 0.5MB 이하의 크기로 줄일 수 있음.
3. Motivation
   * 작은 CNN 아키텍처의 장점:
     * 분산 학습 시 더 빠른 속도로 학습 가능.
     * 클라이언트에 새로운 모델을 배포할 때 오버헤드가 적음.
     * 메모리가 제한된 하드웨어, 특히 FPGA나 ASIC 같은 시스템에 더 적합.
4. Distributed Training
   * 분산 데이터 병렬 학습에서는 모델 파라미터의 수에 따라 통신 오버헤드가 발생하므로, 작은 모델이 더 적은 통신을 필요로 하고 빠르게 학습할 수 있음.
5. Less Overhead When Exporting New Models to Clients
   * 실시간 처리가 중요한 시스템, 예를 들어 자율 주행 차량이나 IoT 기기에서는 모델 업데이트가 자주 필요합니다.
   * SqueezeNet은 AlexNet과 유사한 정확도를 유지하면서 50배 적은 파라미터를 사용하므로, 모델 업데이트 속도가 빠르고 네트워크 대역폭 사용량이 감소합니다.
6. Embedded Deployment
   * FPGA 메모리 제한: FPGA는 종종 10MB 미만의 메모리를 가지고 있어, 작은 모델이 필요합니다.
   * ASIC 적용: 작은 모델은 ASIC에서 칩 크기를 줄일 수 있으며, 온칩 메모리에 저장할 수 있습니다. 이를 통해 실시간 비디오 처리가 가능해집니다.
7. SQUEEZENET DESIGN STRATEGIES
   * SqueezeNet 설계 전략은 다음과 같습니다:
     * 3x3 필터를 1x1 필터로 대체하여 파라미터 수를 줄임.
     * 3x3 필터의 입력 채널 수를 감소.
     * 네트워크의 후반부에서 다운샘플링을 적용하여, 초기 레이어에서 더 큰 활성화 맵을 유지.
8. Fire Module
   * Fire 모듈 구조:
     * Squeeze 레이어: 1x1 필터로 구성.
     * Expand 레이어: 1x1 필터와 3x3 필터로 구성.
   * 하이퍼파라미터:
     * s1x1: Squeeze 레이어의 1x1 필터 수.
     * e1x1 및 e3x3: Expand 레이어의 1x1 및 3x3 필터 수.
9. Delayed Downsampling
   * 다운샘플링은 CNN에서 특징 맵의 공간적 크기를 줄이는 작업으로, 보통 풀링이나 스트라이드 컨볼루션을 통해 이루어집니다.
   * Delayed Downsampling은 다운샘플링을 네트워크 후반부에 적용하여, 초기 레이어에서 더 큰 활성화 맵을 유지하게 합니다. 이를 통해 모델의 표현력을 높일 수 있습니다.
10. Architectural Dimensions 및 각 레이어 구조
    * SqueezeNet의 아키텍처는 다양한 레이어로 구성되며, 각 레이어의 입력 크기, 필터 크기, 스트라이드, 채널 수 등을 설명합니다.
      * Conv1 레이어: 입력 크기 224x224, 96개의 채널.
      * MaxPool1 레이어: 111x111 입력, 96 채널.
      * Fire2 (Squeeze 레이어): 1x1 필터, 55x55 입력, 16 채널.
      * Fire2 (Expand 레이어): 1x1 및 3x3 필터, 55x55 입력, 64 채널.
    * 이 구조는 SqueezeNet이 어떻게 효율적으로 파라미터 수를 줄이면서도 성능을 유지할 수 있는지를 보여줍니다.
11. AVGPOOL10
    * **전역 평균 풀링(Global Average Pooling)** 을 사용하여, Fully Connected 레이어 대신 파라미터 수를 줄이고 성능을 유지합니다.
12. Average Pooling vs Fully Connected Layer (Parameter Comparison)
    * 전역 평균 풀링은 Fully Connected Layer에 비해 파라미터 수가 훨씬 적음.
      * 전역 평균 풀링: 0개의 파라미터.
      * FC 레이어: 약 169,001,000개의 파라미터.
13. SqueezeNet Architecture 및 Bypass 구조
    * SqueezeNet 아키텍처는 Simple Bypass와 Complex Bypass를 통해 병렬 연산을 지원하여 네트워크의 효율성을 높입니다.
14. Conclusion
    * SqueezeNet은 AlexNet 수준의 정확도를 유지하면서도 50배 적은 파라미터를 사용하여 모델을 경량화함.
    * 모델 압축 기법을 통해 SqueezeNet은 크기를 510배까지 줄일 수 있음.
    * Fully Connected 레이어 대신 전역 평균 풀링을 사용하여 파라미터 수를 줄이고 성능을 유지