# KoreanNewsQAModel-LoRA

# KoreanNewsQAModel-LoRA

KoreanNewsQAModel-LoRA는 뉴스 기반의 한국어 질문 답변 시스템을 구축하기 위해 LoRA(Low-Rank Adaptation) 기법을 사용하여 미세 조정된 대규모 언어 모델(Causal Language Model)입니다. 이 모델은 Gemma 모델을 베이스로 하며, 메모리 효율성을 높여 훈련 시간을 단축하고 성능을 향상시킵니다.

## 프로젝트 소개
- **개발자**: 손호영, 장이삭
- **모델 유형**: Causal Language Model (한국어)
- **미세 조정 기법**: LoRA (Low-Rank Adaptation)
- **활용 데이터**: 뉴스 기사 기반 데이터
- **활동 관련**: MLB 2024, Gemma Sprint

### LoRA를 사용한 미세 조정
이 프로젝트는 대규모 모델인 `google/gemma-2b`를 기반으로 하며, LoRA 기법을 통해 모델의 일부 모듈(q_proj, k_proj 등)에 저차원 업데이트를 적용하여 메모리 사용량을 크게 줄이면서 효율적인 미세 조정을 수행합니다.

## 데이터 및 전처리
- **데이터셋**: 한국어 뉴스 기사 데이터
- **데이터 전처리**: 불용어 제거, 토큰화 등 일반적인 전처리 작업을 거쳤으며, 질문 답변 작업에 맞게 적절한 형태로 데이터셋을 구성하였습니다.

## 모델 학습
모델 학습에는 LoRA 기법을 적용하여 메모리와 연산량을 최적화했습니다.
- **훈련 설정**:
  - Mixed Precision (`fp16=True`)
  - 1 에포크(epoch) 동안 훈련
  - 배치 크기: 1 (메모리 최적화를 위해 5 스텝의 그래디언트 누적 사용)
  - 8-bit 옵티마이저 (`adamw_bnb_8bit`) 사용
  - 학습 결과를 TensorBoard로 로깅
- **LoRA 설정**:
  - 업데이트 랭크 (`r`): 1
  - 스케일링 인자 (`lora_alpha`): 2
  - 드롭아웃: 0.05
- **저장 전략**: 에포크 종료 시 모델(최종 상태)만 저장하며, 옵티마이저 상태는 저장하지 않습니다.


## 참고
- [LoRA (Low-Rank Adaptation)](https://arxiv.org/abs/2106.09685): 본 프로젝트의 모델 미세 조정에 사용된 기법에 대한 연구 논문입니다.
- [Hugging Face Transformers](https://huggingface.co/transformers/): 본 프로젝트에서 사용한 모델과 사전 학습된 언어 모델을 제공하는 라이브러리입니다.




---

