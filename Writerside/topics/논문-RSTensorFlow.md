# 논문_RSTensorFlow

RSTensorFlow라는 안드로이드 기기에서 딥러닝 모델을 가속화하기 위한 프레임워크에 대해 설명하고 있습니다. 주요 내용을 간략하게 요약하면 다음과 같습니다:

1. Abstract
   * RSTensorFlow는 안드로이드 기기에서 이기종 컴퓨팅을 사용해 딥러닝 모델의 성능을 향상시키기 위해 TensorFlow를 확장한 프레임워크입니다. 이를 통해 CPU 외에 RenderScript를 사용하여 RNN, CNN과 같은 모델의 성능을 비교할 수 있습니다.
2. Introduction
   * 모바일 기기에서 딥러닝 실행을 가속화하는 방법의 필요성을 설명하며, 기존 프레임워크(Torch, TensorFlow, Caffe)가 모바일 버전에서 CPU만 사용하는 한계를 언급합니다.
3. 관련 연구 (Related Work)
   * DeepX와 같은 기존 연구들과 비교하며, GPU와 DSP를 활용한 딥러닝 가속화를 설명합니다. 그러나 대부분의 방법은 모델 변환이 필요하거나 특정 하드웨어에 종속적이라는 한계를 지적합니다.
4. 시스템 디자인 (System Design)
   * Inception 모델과 같은 CNN 모델에서 RenderScript를 활용한 성능 개선 방법을 설명하며, Conv2D와 **행렬 곱셈(MatMul)** 의 최적화 과정을 다룹니다.
5. 실험 결과 (Experiments)
   * Nexus 5X 및 Nexus 6에서 실험을 수행한 결과, RenderScript를 사용했을 때 Matrix Multiplication 연산에서 최대 6배의 성능 향상을 확인했습니다. 하지만 Convolution 연산에서는 큰 성능 개선이 없었습니다.
6. 결론 (Conclusion)
   * RSTensorFlow는 안드로이드 기기에서 딥러닝 모델의 성능을 향상시키기 위한 가능성을 제시했지만, 일부 연산에서는 성능이 제한적이며 하드웨어별 최적화가 필요하다는 점을 지적합니다