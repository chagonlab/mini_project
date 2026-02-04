# 인공지능 작사가 만들기

본 프로젝트는 RNN(LSTM) 모델을 활용하여 주어진 시작 문구에 이어지는 자연스러운 노래 가사를 생성하는 인공지능 모델을 학습시킨 실험입니다.

## 1. 실험 목표
* 학습용 실험: 텍스트 데이터의 전처리, 토큰화, RNN 모델 구성 등 자연어 처리(NLP)의 전반적인 흐름을 이해합니다.
* 데이터 시퀀스를 분석하여 다음에 올 단어를 예측하고, 문장 형태의 가사를 생성하는 모델을 구축합니다.

## 2. 주요 실험 내용
* 데이터셋: 여러 개의 가사 텍스트 파일(txt)을 통합하여 사용하였습니다 (데이터 크기: 약 187,088행).
* 데이터 전처리:
    * 소문자 변환 및 특수문자 제거를 수행했습니다.
    * 문장의 시작과 끝을 알리는 <start>, <end> 토큰을 추가했습니다.
    * 제약 조건: 가사의 흐름을 유지하기 위해 토큰 개수가 15개를 초과하는 긴 문장은 제외했습니다.
* 토큰화: tf.keras.preprocessing.text.Tokenizer를 사용하여 12,000개의 단어 사전을 구축하고 패딩(Padding) 처리를 완료했습니다.

## 3. 모델 설계 및 시도
* 모델 구조: TextGenerator 클래스 (Subclassing 모델 구사)
    * Embedding Layer: 단어의 의미적 공간 투영 (Embedding Size: 512).
    * LSTM Layer: 두 개의 층으로 구성된 RNN 레이어 (Hidden Size: 2048).
    * Dense Layer: 최종 단어 예측을 위한 출력층.
* 학습 설정:
    * Optimizer: Adam.
    * Loss: SparseCategoricalCrossentropy (from_logits=True).
    * Batch Size: 64, Epochs: 5.

## 4. 실험 결과
* Loss 변화: 1 Epoch에서 약 3.00이었던 Train Loss가 5 Epoch 만에 1.38 수준으로 감소하였습니다.
* Validation Loss: 최종 약 2.18을 기록하며 안정적으로 학습된 수치를 보였습니다.
* 가사 생성 테스트:
    * 입력: "i love"
    * 출력: "<start> i love you , baby , <end>"
    * 결과 분석: 모델이 문법적으로 어색하지 않고 대중가요에서 흔히 쓰이는 자연스러운 표현을 생성해내는 것을 확인했습니다.
