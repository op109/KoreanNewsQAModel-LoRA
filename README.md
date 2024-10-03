# KoreanNewsQAModel-LoRA

이 프로젝트는 뉴스 기반 질문 답변 시스템을 구축하기 위해 한국어 자연어 처리를 활용한 모델을 개발한 것입니다. `LoRA`(Low-Rank Adaptation) 기법을 사용하여 대규모 언어 모델인 `Gemma`를 메모리 효율적으로 미세 조정하였습니다. 이 모델은 `🤗 Hugging Face` 허브에 업로드되어 있으며, 뉴스 데이터로 학습된 모델을 활용해 한국어 질문 답변 시스템을 제공합니다.

모델 링크: [KoreanNewsQAModel-LoRA on Hugging Face](https://huggingface.co/sonhy02/NewsBasedQuestionAnsweringModel)

학습 데이터 링크: [뉴스 데이터](https://drive.google.com/drive/u/0/folders/1zaAQIzOwlK-v81sKdm1yPQ4OkT-3MgBP)

## 모델 설명

### 1. 프로젝트 목적
뉴스 데이터를 기반으로 한 한국어 질문 답변 시스템을 개발하여, 다양한 뉴스 기사로부터 의미 있는 정보를 추출하고, 자연스러운 한국어 답변을 생성하는 것을 목표로 합니다. 이 모델은 한국어 뉴스의 문맥을 이해하고 질문에 대한 정확한 답변을 제공할 수 있도록 설계되었습니다.

### 2. 모델 구조 및 기술
- **모델 타입**: Causal Language Model
- **언어**: 한국어
- **베이스 모델**: `google/gemma-2b`를 기반으로 미세 조정
- **미세 조정 기법**: `LoRA`(Low-Rank Adaptation) 기법을 사용하여 `q_proj`, `k_proj` 등 특정 모듈에 저차 적응을 적용
- **학습 과정**:
  - `r=1` (저차 업데이트 행렬의 랭크), `lora_alpha=2` (스케일링 인자), 드롭아웃 비율 `0.05`를 적용해 모델을 최적화
  - `fp16` 혼합 정밀도 사용
  - 1에폭의 학습 진행, 장치 메모리 효율을 위해 배치 사이즈를 1로 설정하고 5 스텝 동안 기울기 누적
  - `8-bit AdamW` 옵티마이저를 사용하여 메모리 사용량 최소화

## 데이터셋
- 이 모델은 한국어 뉴스 기사와 관련된 데이터셋을 사용해 학습되었습니다. 뉴스 기사에서 추출된 문장과 질문을 바탕으로 모델이 문맥을 이해하고 적절한 답변을 생성하도록 훈련되었습니다.

## 코드 사용 방법

### 1. 모델 훈련
모델 훈련을 위한 코드는 `LoRA`를 적용하여 효율적으로 모델을 미세 조정하는 내용을 포함합니다. `Trainer` 객체를 사용하여 다음과 같은 설정으로 모델을 훈련할 수 있습니다:
- 배치 사이즈: 1
- 기울기 누적: 5
- 혼합 정밀도(`fp16`): 사용
- 학습 시 드롭아웃 비율: 0.05


## 참고 자료
- [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)
- [Hugging Face Transformers Documentation](https://huggingface.co/transformers/)

## 개발자 정보
- 손호영, 장이삭
