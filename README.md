<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:7f7fd5,50:86a8e7,100:91eae4&height=200&text=🧠%20Brain-Trace&fontSize=45&animation=fadeIn&fontColor=ffffff" />
</p>

<div align="center">
**BrainTrace**는 클라우드 없이, 기밀 데이터를 로컬에서 ‘지식’으로
<br>
<strong>당신만의 Second Brain</strong>으로 만들어드립니다.
</div>

---
## 🧠 프로젝트 개요
<img src="https://raw.githubusercontent.com/brilliant13/portfolio/main/30%E1%84%8C%E1%85%A9_%E1%84%86%E1%85%AE%E1%84%86%E1%85%AE%20%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5.png" width="750" alt="mu_mu"/>

<!--<img src="https://github.com/user-attachments/assets/3c98fd2c-b38e-4ede-9704-d518111129e1" width="750" alt="mumu"/>-->

<!-- <img src="https://github.com/user-attachments/assets/3c98fd2c-b38e-4ede-9704-d518111129e1" width="750" alt="best_dou"/> -->
<br>

> **“자료를 넣으면 지식이 된다. 질문하면 문맥이 답한다.”**

현대의 업무/학습 환경에서는 수많은 학습 자료(PDF, 강의 녹음, 텍스트 파일 등)가 디지털화되어 존재하지만,  
이를 체계적으로 정리하고 활용하는 데에는 여전히 **사람의 수작업**이 필요합니다.  
또한 많은 AI 도구가 클라우드 기반이라 **기밀 데이터/개인정보를 올리기 어렵다**는 현실적인 제약이 있습니다

**Brain-Trace**는 이러한 문제를 해결하기 위해 기획된 **온디바이스 AI 기반 기밀 데이터 관리 애플리케이션**입니다.  
사용자가 PDF, 텍스트, 음성 파일을 업로드하면 Llama가 **개념**(노드)과 **관계**(엣지)를 추출해 **Neo4j 지식그래프에 저장**합니다.
또한 생성된 **노드 텍스트를 KoE5로 임베딩**하여 **Qdrant(Vector DB)에 저장**해, 이후 의미 기반 탐색이 가능하도록 준비합니다.

이후 사용자가 자연어로 질문하면, 내부적으로 **온디바이스 LLM을 사용하여 KoE5로 임베딩**하고, **Qdrant에서 유사 노드/문맥 후보를 검색**합니다.
검색된 노드를 시작점(seed)으로 Cypher 쿼리를 작성하여 **Neo4j에서 주변 관계를 확장 탐색**해 관련 지식 서브그래프를 구성한 뒤,
그 그래프 내용을 근거로 **Llama가 최종 추론형 답변을 생성**합니다.

또한 모든 프로세스는 로컬 디바이스에서 처리되므로,  
**클라우드 의존 없이 완전한 오프라인 환경에서도 작동**하며,  
**개인정보 보호 및 민감한 연구자료의 안전한 처리**가 가능합니다.

📌 결과적으로, Brain-Trace는 단순한 문서 분석 도구를 넘어 
"내 손안의 두 번째 뇌(Second Brain)"로서 작동하는  
**지식 구조화 + 문맥 질문 응답 + 보안 강화**의 종합 AI 시스템입니다.

---

## 🌟 주요 기능

### 🔐 Cloud-free / On-device (보안 중심 설계)
- 전처리 · 검색 · 추론 전 과정이 **클라우드 없이 로컬에서 실행**
- 외부 업로드 없이 기밀 데이터 처리 → **정보 유출 리스크 최소화**
- 네트워크 제약 환경에서도 **오프라인 동작** 가능

### 📄 멀티모달 자료 자동 수집·전처리 (PDF · 메모 · 음성)
- PDF/텍스트/메모를 자동 파싱 및 정규화
- 음성 파일은 **Whisper로 텍스트 변환(STT)** 후 파이프라인에 통합
- 문맥 기반 청킹/정제 처리로 **검색·그래프 구성 품질** 향상

### 🧩 지식그래프 자동 구축 & 시각화 (Llama → Neo4j → UI)
- LLM이 핵심 **개념(노드)** 과 **관계(엣지)** 를 추출해 그래프 구조로 변환
- 추출 결과를 **Neo4j 지식그래프**로 저장하여 “연결된 지식”으로 지속 축적
- 저장된 그래프를 **클라이언트 UI에서 실시간 시각화/탐색**  
- 노드/관계 하이라이트, 클릭 기반 확장 탐색으로 **답변 근거와 문맥 흐름**을 직관적으로 확인
- 데이터가 쌓일수록 연결 정보가 풍부해져 **의미 탐색·Graph-RAG 추론 품질**이 함께 향상

### 🔍 의미 기반 탐색 (KoE5 → Qdrant)
- 노드/문맥을 **KoE5 임베딩**으로 벡터화
- **Qdrant 벡터DB**에 저장/검색하여 키워드 없이도 유사 문맥 탐색
- “어렴풋한 단서”만으로도 관련 자료로 접근 가능 (검색 부담 감소)

### 💬 Graph-RAG 문맥 질의응답 (Qdrant → Neo4j 확장 → LLM 응답)
- 질문을 KoE5로 임베딩 → **Qdrant에서 관련 노드/문맥 seed 검색**
- seed를 시작점으로 **Neo4j에서 관계 확장 탐색**하여 서브그래프 구성
- 그래프 문맥을 근거로 **LLM이 최종 답변 생성** (단순 요약이 아닌 연결 기반 응답)

### 🧠 근거 그래프 시각화 UI (신뢰성 강화)
- 답변에 사용된 **노드/관계가 하이라이트**되며 동적으로 표시
- 그래프 탐색 화면 제공 + 노드 클릭/확대/필터 등 직관적 인터랙션
- (옵션) 그래프 물리 파라미터 커스터마이징, 다크/화이트 모드, 멀티 모니터 확장 지원

### ⚡ Snapdragon X Elite NPU 로컬 추론 가속 (BYOM)
- **PyTorch → ONNX Export → AIMET 양자화 → QNN Binary(BYOM)** 변환 파이프라인
- Snapdragon X Elite **NPU에서 온디바이스 추론** 구현 → 응답 속도 개선
- 클라우드 의존 없이도 **실사용 가능한 성능** 확보

---
## 🧬 시스템 아키텍처

```text
< 지식 축적 파이프라인 >
[PDF/메모/음성 업로드]
      ↓
[전처리 · 청킹 · STT(Whisper)]
      ↓
[Llama: 개념(노드) · 관계(엣지) 추출]
      ↓
[Neo4j: 지식그래프 저장]
      ↓
[KoE5: 노드/문맥 임베딩 생성]
      ↓
[Qdrant: 벡터DB 저장]

< 질의응답(Graph-RAG) 파이프라인 >
[사용자 질문(자연어)]
      ↓
[KoE5: 질문 임베딩]
      ↓
[Qdrant: 유사 노드/문맥 seed 검색]
      ↓
[Neo4j: seed 기반 관계 확장 탐색 (서브그래프 구성)]
      ↓
[Llama: 그래프 문맥 기반 답변 생성]
      ↓
[UI: 근거 노드/관계 하이라이트 & 그래프 시각화]
```
---

## 🛠️ 기술 스택

| 항목 | 기술 |
|------|------|
| 프론트엔드 | React, Vite |
| 백엔드 | FastAPI |
| 데이터베이스 | Neo4j (Embedded), SQLite |
| 음성 인식 | OpenAI Whisper |
| AI 모델 | llama, KoE5 |
| RAG 구성 | 자연어 → Cypher → Graph 응답 |
| 기타 도구 | Electron, VS Code, Git |

---

## 📑 API 문서 (Swagger UI)

<details>
<summary>📂 Swagger Docs 보기 (클릭해서 펼치기)</summary>

<br>

FastAPI 기반 REST API는 아래와 같은 Swagger UI 형태로 구성되어 있습니다.

<p align="center">
  <img src="https://github.com/yes6686/portfolio/blob/main/Swagger_API.png?raw=true" alt="Swagger UI Screenshot" width="85%" />
</p>

> 로컬에서는 `http://localhost:8000/docs`에서 직접 확인하실 수 있습니다.

</details>

---

## 🧪 성능 비교 (Graph-RAG vs 일반 RAG)

| Method | P | R | F1 |
|--------|----|----|----|
| **Community-GraphRAG (Local)** | **67.2** | **64.89** | **64.6** |
| 일반 RAG | 66.34 | 63.99 | 63.88 |

> 출처: [arXiv:2502.11371](https://doi.org/10.48550/arXiv.2502.11371)

---

## 💡 기대 효과
### 🔒 보안이 중요한 환경에서도 AI 도입 가능
- 사내 문서/연구자료/고객 데이터 등 민감 정보도 **외부 전송 없이** 활용
- 인터넷 차단/망분리 환경에서도 **오프라인 AI 워크플로우** 제공

### 📚 “정리”가 아니라 “축적되는 지식”으로 전환
- 자료를 넣는 순간 **지식그래프 형태로 구조화**되어 재사용성이 상승
- 데이터가 쌓일수록 연결 정보가 늘어나 **Second Brain 효과가 강화**

### 🔍 검색 피로 감소 + 탐색 효율 극대화
- 키워드가 없어도 의미 기반 탐색으로 **찾는 시간을 단축**
- 문서가 많아질수록 오히려 더 찾기 쉬워지는 구조 (탐색 부담 역전)

### ✅ 답변 신뢰성/추적 가능성 향상
- 응답이 “그럴듯한 말”이 아니라 **근거 그래프**로 확인 가능
- 업무/학습에서 중요한 **검증 가능한 AI** 사용 경험 제공

### 🏢 적용 시나리오 확장
- **교육/학습**: 강의자료·필기·녹음 기반 자동 구조화 + 질의응답
- **기업 지식관리**: 회의록/문서의 연결 구조화 + 빠른 검색/탐색
- **연구/개발**: 논문/실험 노트 축적 + 관계 기반 맥락 회수

---
## 🎥 시연 영상

| 소개 영상 | Demo Video |
|-----------|------------|
| [![Brain-Trace 소개](https://img.youtube.com/vi/wu7_yyd0TAI/0.jpg)](https://www.youtube.com/watch?v=wu7_yyd0TAI) | [![Brain-Trace Demo](https://img.youtube.com/vi/a6mMXmOi1NU/0.jpg)](https://www.youtube.com/watch?v=a6mMXmOi1NU&t=106s) |

---

<details>
<summary>📊 시스템 구조 패널 보기 (클릭해서 펼치기)</summary>

<br>

<p align="center">
  <img src="https://raw.githubusercontent.com/brilliant13/portfolio/main/30%E1%84%8C%E1%85%A9_%E1%84%86%E1%85%AE%E1%84%86%E1%85%AE%20%E1%84%8B%E1%85%B5%E1%84%86%E1%85%B5%E1%84%8C%E1%85%B5.png" width="750" alt="mu_mu"/>
  <!--<img src="https://github.com/user-attachments/assets/3c98fd2c-b38e-4ede-9704-d518111129e1" alt="시스템 구조 패널" width="80%"/>-->
</p>

</details>

## 🔗 참고 자료

- [React 공식 문서](https://reactjs.org/docs/getting-started.html)
- [Neo4j 공식 문서](https://neo4j.com/docs/)
- [OpenAI Whisper](https://github.com/openai/whisper)
- [GPT API Docs](https://platform.openai.com/docs/)
- [GraphRAG 논문](https://arxiv.org/abs/2502.11371)

---


## 👥 팀원 소개

| 이름       | 역할                   | 담당 업무                                                                                  |
|------------|------------------------|---------------------------------------------------------------------------------------------|
| **정웅**   | 팀장 / Full-stack & AI | 프로젝트 총괄, 프론트엔드 개발, 백엔드 로직 설계 및 API 연동, <br>AI 및 Graph DB 연동                                       |
| **김동혁** | Back-End               | FastAPI 기반 API 개발, 검색/답변/지식그래프 생성 로직 개발,<br>Graph DB & SQLite 설계     |
| **안예찬** | Full-stack              | 패널 및 소스 뷰어 개발, 로컬 DB 연동, 백엔드 API 구현 등 전체 시스템 UI/서버 통합 개발                                                |
| **유정균** | AI                     | AI 모델 양자화 및 경량화                                                                    |

## 📃 라이선스

```
Copyright (c) 2025 Brain-Trace Team
All rights reserved.

This code is provided for academic, non-commercial use only.
Redistribution and use in source and binary forms, with or without modification,
are permitted for academic non-commercial use provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice,
   this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation and/or
   other materials provided with the distribution.

This software is provided by the authors "as is" and any express or implied warranties,
including, but not limited to, the implied warranties of merchantability and fitness
for a particular purpose are disclaimed. In no event shall the authors be liable
for any direct, indirect, incidental, special, exemplary, or consequential damages
(including, but not limited to, procurement of substitute goods or services;
loss of use, data, or profits; or business interruption) however caused and on
any theory of liability, whether in contract, strict liability, or tort (including
negligence or otherwise) arising in any way out of the use of this software,
even if advised of the possibility of such damage.

```
