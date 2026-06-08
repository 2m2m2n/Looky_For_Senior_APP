# 👕 Looky - 시니어 전용 지능형 디지털 옷장 및 AI 가상 피팅 플랫폼

> An AI-powered virtual try-on & smart wardrobe platform designed for seniors (Built with Flutter, FastAPI, and CatVTON)

<br>

## 💡 프로젝트 소개 (Overview)

**Looky**는 시니어 계층의 독립적인 의생활을 지원하기 위해 개발된 인공지능 기반 디지털 옷장 애플리케이션입니다 기존의 패션 앱들이 20~30대 중심의 체형 데이터와 트렌드에 편향되어 있는 한계를 극복하고자 기획되었습니다 

본 프로젝트는 고가의 AI 서버 인프라 없이도 모바일 환경에서 고품질 서비스를 제공하기 위해 **Flutter(클라이언트) - FastAPI(백엔드) - Google Colab T4 GPU(AI 서버)**를 ngrok 터널링으로 연계한 비용 제로 하이브리드 분산 아키텍처를 구현했습니다

<br>

## 🌟 주요 기능 (Key Features)

### 📸 AI 의류 자동 등록 (MobileNetV2)
- `remove.bg` API를 통해 이미지의 배경을 자동 제거하고 옷의 지배적인 색상을 추출
- Kaggle 패션 데이터셋으로 전이학습된 MobileNetV2 모델이 12종의 의류 카테고리를 자동 분류하여 복잡한 수동 입력 과정을 완전히 제거

### 👗 실사 기반 AI 가상 피팅 (CatVTON)
- ICLR 2025에 채택된 최첨단 의류 가상 피팅 모델인 `CatVTON` 적용
- `DensePose`로 신체 부위를 감지하고 `SCHP`로 의류 영역을 정밀 파싱
- `Stable Diffusion Inpainting` 50단계를 거쳐 시니어의 체형 왜곡 없는 자연스러운 피팅 이미지 생성

### 🌤️ 기상 및 목적 맞춤형 스마트 코디 추천
- GPS와 OpenWeatherMap API를 연동해 실시간 기온 데이터 수신
- 자체 개발한 7단계 기온 알고리즘을 통해 날씨에 최적화된 상·하의 및 아우터 조합 추천
- 산책, 병원, 모임 등 시니어의 주요 외출 목적에 따른 맞춤형 가중치 반영

### 🛡️ 시니어 의생활 안전 태그 시스템
- 고령층의 낙상 사고 및 활동 불편을 예방하기 위해 '입고벗기편함', '미끄럼주의', '긴기장주의' 등의 특화 안전 태그 도입
- 의류 조합에 따른 '편안함 점수'를 산출하고 위험 요소 감지 시 보호자 확인 메시지 자동 생성 기능 구현

<br>

## 🏗️ 시스템 아키텍처 (System Architecture)

- 모바일 클라이언트 환경의 연산 성능 한계를 극복하기 위해 서버간 역할 분리
- 백엔드(FastAPI) 서버는 외부 API 연동 및 MobileNetV2 추론 중계를 담당
- 무거운 가상 피팅 연산 파이프라인(CatVTON)은 16GB VRAM을 제공하는 클라우드 환경의 Google Colab T4 GPU에서 처리

<br>

## 🛠️ 기술 스택 (Tech Stack)

- **Frontend:** Flutter 3.x / Dart
- **Backend:** Python 3.10 / FastAPI / Uvicorn / ngrok
- **AI Models:** MobileNetV2 (TensorFlow) / CatVTON (PyTorch) / DensePose / SCHP / Stable Diffusion Inpainting
- **Infrastructure & DB:** Google Colab (Tesla T4 GPU) / Hive 2.x NoSQL

<br>

## 📊 모델 성능 (Performance)

- **의류 분류 정확도:** 10 Epochs 전이학습 결과 최종 검증 정확도 76.94% 달성
- **모델 일반화 증명:** 학습 정확도와 검증 정확도의 차이가 1.18%p 수준으로 과적합 없는 안정적 상태 확보
- **추론 지연 최소화:** 단일 이미지당 평균 추론 시간 약 180ms를 기록하여 모바일 실시간 대응 요건 충족

<br>

## 🚀 실행 방법 (Getting Started)

### 1. Backend (FastAPI) 실행
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 2. AI Server (Google Colab) 셋업
1. `ai/` 폴더 내의 노트북 파일을 Google Colab에 업로드
2. 런타임 유형을 **T4 GPU**로 변경 후 셀을 순차적으로 실행
3. 가중치 다운로드 완료 후 발급된 ngrok URL을 백엔드 환경변수에 연동

### 3. Frontend (Flutter) 빌드
```bash
cd frontend
flutter pub get
flutter run
```

<br>

## 📄 참고 자료 (References)

- [CatVTON: Concatenation Is All You Need for Virtual Try-On (ICLR 2025)](https://github.com/Zheng-Chong/CatVTON)
- [MobileNetV2: Inverted Residuals and Linear Bottlenecks (CVPR 2018)](https://arxiv.org/abs/1801.04381)
- [DensePose: Dense Human Pose Estimation in the Wild (CVPR 2018)](https://github.com/facebookresearch/DensePose)
