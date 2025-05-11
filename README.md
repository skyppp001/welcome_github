좋아. 노트북의 주요 코드를 분석한 결과, 이 프로젝트는 **Teachable Machine에서 생성한 Keras 모델(`.h5`)과 클래스 레이블(`labels.txt`)을 이용해 이미지 분류 예측을 수행하는 Colab 기반 이미지 예측 서비스**로 구성되어 있다.

다음은 순서도 설명 및 주요 함수 흐름을 포함한 `README.md` 초안이다:

---

````markdown
# Teachable Machine 기반 이미지 예측 서비스

이 프로젝트는 [Teachable Machine](https://teachablemachine.withgoogle.com/)에서 학습한 Keras 모델을 활용하여, 업로드한 이미지를 분류하고 예측 결과를 출력하는 간단한 이미지 예측 서비스이다.  
Google Colab 환경에서 실행되며, `.h5` 모델과 레이블 파일만 있으면 누구나 쉽게 사용할 수 있다.

## 🔍 주요 기능

- Teachable Machine에서 훈련한 이미지 분류 모델 로드
- 이미지 전처리 및 예측 실행
- 예측된 클래스 이름과 확률 출력

## 🛠 실행 환경

- Python 3.x
- TensorFlow 2.12.0 (권장)
- Keras
- NumPy
- Pillow

Colab에서 아래와 같이 실행 환경을 구성한다:

```bash
!pip install tensorflow==2.12.0
````

## 📁 프로젝트 구조

```
├── keras_model.h5       # Teachable Machine에서 export한 Keras 모델
├── labels.txt           # 클래스 이름 목록
├── scissor1.png         # 예측 대상 이미지 예시
├── 티처블모델을_이용한_이미지예측서비스.ipynb  # 본 프로젝트 노트북
```

## 🔄 순서도 흐름

1. 필요한 라이브러리 설치 및 임포트
2. 모델(`keras_model.h5`) 로드
3. 클래스 이름(`labels.txt`) 로드
4. 이미지 불러오기 및 리사이즈 (224x224)
5. 이미지 배열 생성 및 정규화
6. 모델을 통해 예측 수행
7. 결과 출력

## 🧩 주요 코드 설명

```python
model = load_model("keras_model.h5", compile=False, custom_objects={'DepthwiseConv2D': tf.keras.layers.DepthwiseConv2D})
```

* Teachable Machine에서 생성한 모델을 로드하며, `DepthwiseConv2D` 레이어를 명시적으로 등록하여 호환성을 유지한다.

```python
class_names = open("labels.txt", "r").readlines()
```

* 예측 결과를 해석하기 위해 클래스 이름 목록을 불러온다.

```python
image = Image.open("scissor1.png").convert("RGB")
image = ImageOps.fit(image, (224, 224), Image.Resampling.LANCZOS)
```

* 입력 이미지를 모델 입력 크기인 224x224로 변환하고 정규화한다.

```python
prediction = model.predict(data)
```

* 모델을 이용해 예측을 수행하고, 가장 확률이 높은 클래스를 출력한다.

## ▶️ 실행 방법

1. [Colab 노트북 열기](#)
2. `keras_model.h5`, `labels.txt`, 예측할 이미지를 Colab에 업로드
3. 셀을 순서대로 실행하여 예측 결과 확인

## 📌 예측 결과 예시

```bash
[0.95 0.02 0.03]
예측된 클래스: 가위 (scissor)
```

## 📎 참고

* 모델은 Teachable Machine에서 `TensorFlow Keras (.h5)` 포맷으로 export해야 함
* 클래스 순서에 따라 `labels.txt`와 `.h5` 모델이 반드시 일치해야 정확한 예측이 가능함

```

---

다음 단계로는 README에 포함할 수 있도록 예측 결과의 이미지나 추가 설명이 있다면 제공해줘.  
또는 Colab 공유 링크가 있다면 넣어줄 수도 있어.

  
**Q1:** 이 README에 예측 이미지 시각화 결과도 포함하고 싶나요?  
**Q2:** Colab 노트북 링크를 README에 삽입할까요? (예: [노트북 바로가기](링크))  
**Q3:** 향후 Streamlit 등을 활용해 웹 인터페이스로 확장할 계획이 있나요?
```
