# [cite_start]👕 Looky - 시니어 전용 지능형 디지털 옷장 및 AI 가상 피팅 플랫폼 [cite: 1797]

> An AI-powered virtual try-on & smart wardrobe platform designed for seniors. (Built with Flutter, FastAPI, and CatVTON)

![Looky Banner](assets/looky_main.png) ## 💡 프로젝트 소개 (Overview)
[cite_start]**Looky**는 시니어 계층의 독립적인 의생활을 지원하기 위해 개발된 인공지능 기반 디지털 옷장 애플리케이션입니다[cite: 1797]. [cite_start]기존의 패션 앱들이 20~30대 중심의 체형 데이터와 트렌드에 편향되어 있는 한계를 극복하고자 기획되었습니다[cite: 1798, 1811]. 

[cite_start]본 프로젝트는 고가의 AI 서버 인프라 없이도 모바일 환경에서 고품질 서비스를 제공하기 위해 **Flutter(클라이언트) - FastAPI(백엔드) - Google Colab T4 GPU(AI 서버)**를 ngrok 터널링으로 연계한 비용 제로 하이브리드 분산 아키텍처를 구현했습니다[cite: 1818, 1822].

## 🌟 주요 기능 (Key Features)

* [cite_start]**📸 AI 의류 자동 등록 (MobileNetV2)** * `remove.bg` API를 통해 이미지의 배경을 자동 제거하고 옷의 지배적인 색상을 추출합니다[cite: 1826, 1836].
  * [cite_start]Kaggle 패션 데이터셋으로 전이학습된 MobileNetV2 모델이 12종의 의류 카테고리를 자동 분류하여 복잡한 수동 입력 과정을 생략했습니다[cite: 1800, 1815].
* **👗 실사 기반 AI 가상 피팅 (CatVTON)**
  * [cite_start]ICLR 2025에 채택된 최첨단 모델인 `CatVTON`을 적용하였습니다[cite: 1799, 1813].
  * [cite_start]`DensePose`로 신체 부위를 감지하고, `SCHP`로 의류 영역을 정밀하게 파싱한 뒤, `Stable Diffusion Inpainting`(50 steps)을 거쳐 시니어의 체형 왜곡 없는 자연스러운 피팅 이미지를 생성합니다[cite: 1799, 1814].
* **🌤️ 기상 및 목적 맞춤형 스마트 코디 추천**
  * [cite_start]GPS와 OpenWeatherMap API를 연동해 실시간 기온을 수신하고, 7단계 기온 알고리즘을 통해 날씨에 최적화된 상·하의·아우터 조합을 추천합니다[cite: 1800, 1816].
  * [cite_start]산책, 병원, 모임 등 외출 목적에 따른 맞춤형 가중치를 적용합니다[cite: 1816].
* **🛡️ 시니어 의생활 안전 태그 시스템**
  * [cite_start]고령층의 낙상 사고 및 활동 불편을 예방하기 위해 '입고벗기편함', '미끄럼주의', '긴기장주의' 등의 특화 안전 태그를 도입했습니다[cite: 1800, 1817].
  * [cite_start]의류 조합에 따른 '편안함 점수'를 산출하고 보호자 확인 메시지를 자동 생성하여 안전성을 확보했습니다[cite: 1817].

## 🏗️ 시스템 아키텍처 (System Architecture)

[cite_start]![Architecture Diagram](assets/architecture.png) * 연산 성능의 한계를 극복하기 위해 역할을 완벽하게 분리했습니다[cite: 1823].
* [cite_start]FastAPI 서버는 날씨 연동과 MobileNetV2 추론 중계를 담당하며, 무거운 이미지 합성 파이프라인(CatVTON)은 16GB VRAM을 제공하는 Colab T4 GPU에서 처리됩니다[cite: 1820, 1821].

## 🛠️ 기술 스택 (Tech Stack)

* [cite_start]**Frontend:** Flutter 3.x, Dart [cite: 1832]
* [cite_start]**Backend:** Python 3.10, FastAPI, Uvicorn, ngrok [cite: 1832]
* [cite_start]**AI / ML Models:** * MobileNetV2 (TensorFlow/Keras) [cite: 1832]
  * [cite_start]CatVTON (PyTorch) [cite: 1832]
  * [cite_start]DensePose (Facebook Research) [cite: 1832]
  * [cite_start]SCHP (Self-Correction Human Parsing) [cite: 1832]
  * [cite_start]Stable Diffusion Inpainting [cite: 1832]
* [cite_start]**Infrastructure / DB:** Google Colab (Tesla T4 GPU), Hive 2.x (Flutter NoSQL) [cite: 1832]

## 📊 모델 성능 (Performance)
* [cite_start]**의류 분류 (MobileNetV2):** 10 Epochs 전이학습 결과, 최종 검증 정확도 76.94% 및 학습-검증 차이 1.18%p로 과적합 없는 일반화를 달성했습니다[cite: 1884, 1885]. [cite_start]단일 이미지 평균 추론 시간은 약 180ms입니다[cite: 1888].
* [cite_start]**가상 피팅 (CatVTON):** Colab T4 환경에서 ngrok 중계를 통해 모바일 디바이스로 고화질 합성 결과를 안정적으로 반환합니다[cite: 1850].

## 🚀 실행 방법 (Getting Started)

### 1. Backend (FastAPI) 실행
```bash
# 로컬 PC에서 실행 (포트 8000)
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000
