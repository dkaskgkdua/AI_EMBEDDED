# tpu

## Introduction to Tensor Processing Unit (TPU)
* TPU는 Google에서 개발한 딥러닝을 가속화하기 위한 전용 하드웨어 가속기입니다.
* TPU는 대규모 병렬 처리를 위해 설계되었으며, Google의 데이터 센터에 배치되어 있습니다

## Practical Example: Google TPU v1 (2016)
* TPU v1은 Google에서 2016년에 처음으로 공개한 하드웨어로, 딥러닝 모델 학습 및 추론을 가속화하는 데 중점을 둔 하드웨어입니다.
* TPU는 기존 CPU 및 GPU에 비해 높은 성능을 제공하며, 특히 대규모 데이터 처리에 적합합니다

## The Heart of the TPU: A Systolic Array
* **시스톨릭 배열(Systolic Array)** 은 TPU의 핵심 구조로, 병렬 행렬 연산을 최적화합니다.
* **시스톨릭 실행(Systolic Execution)** 은 데이터가 배열의 셀에 규칙적으로 도착하고 결합되어, 연산이 동시에 이루어지도록 설계되었습니다.
* 이를 통해 TPU는 데이터를 실시간으로 처리하며, 효율적인 연산이 가능합니다.

## Practical Example: Google TPU (Systolic Array 계산 과정)
* 슬라이드에서 설명한 TPU의 작동 원리는 시스톨릭 배열을 통한 행렬 연산으로, 입력값과 가중치를 곱하고 더하는 과정이 병렬적으로 수행됩니다.
* 각 셀에서 가중치와 입력값이 결합되어, 출력 값이 생성되는 방식입니다.
* 예를 들어, 입력값 x11, x12, x13과 가중치 w11, w12, w13이 결합되어 y11 값이 생성됩니다

## Log Roofline 및 Linear Roofline
* Roofline 모델은 CPU, GPU, TPU의 성능을 비교하는 그래프입니다.
* 이 모델은 하드웨어가 주어진 계산 작업에서 얼마나 효율적으로 작동하는지를 시각적으로 나타냅니다.
* Log Roofline과 Linear Roofline은 각각 CPU, GPU, TPU의 상대적 성능을 보여주며, TPU가 특정 작업에서 더 뛰어난 성능을 나타냅니다

## TPU와 GPU의 CPU 대비 상대적 성능 비교
* TPU와 GPU는 CPU에 비해 멀티 레이어 퍼셉트론(MLP), LSTM, CNN 등 다양한 딥러닝 모델에서 우수한 성능을 보입니다.
* 예를 들어, TPU는 MLP와 CNN 작업에서 GPU보다 더 높은 성능을 나타내며, GPU는 LSTM에서 더 나은 성능을 보일 수 있습니다

## Perf/Watt(성능 대비 전력 효율) 비교
* TPU는 CPU 및 GPU와 비교했을 때 성능 대비 전력 효율이 훨씬 뛰어납니다.
* 예를 들어, TPU는 Haswell CPU 대비 80배, K80 GPU 대비 30배 더 높은 전력 효율을 제공합니다

## TPU와 Eyeriss 비교
* TPU와 Eyeriss는 각각 다른 목적을 위한 하드웨어입니다.
  * TPU는 주로 딥러닝 모델 학습에 사용되며, Eyeriss는 추론에 더 최적화되어 있습니다.
* 메모리 계층 구조 및 프로그램 가능성 측면에서도 TPU는 Eyeriss보다 더 높은 프로그래밍 가능성을 가지고 있으며, 일반적인 AI 작업에 더 적합합니다