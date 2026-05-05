# 🎨 Art Robot; Pointillism Drawing

> **Team:** ROKEY_영차영차   
> **Name:** 문홍일_박지훈_이승민_이창석_최대혁  
> **Project Type:** Robotics + Computer Vision + Web  
> **Core:** “디지털 이미지를 물리적 점묘화로 변환하는 자동 드로잉 시스템”

---

# 1. 📌 프로젝트 개요

## 1-1. 프로젝트 정의

이미지 처리 알고리즘과 협동 로봇을 활용하여
**입력 이미지를 점묘화로 변환하고 실제 로봇이 물리적으로 드로잉하는 시스템을 구현한다.** 

## 1-2. 기획 배경

* 생성형 디지털 이미지들의 범람  → 아날로그, 물리적 결과물에 대한 갈증
* 특히 점묘화는 반복 노동 중심 → 자동화 가치 높음
* 체험형 콘텐츠 및 커스텀 아트 시장 확대
* 관광지 or 컨벤션 등에서 추억과 경험의 소재로 활용가능

## 1-3. 핵심 가치

* 디지털에서 나오는 아날로그 감성 (실제 펜 드로잉)
* 사용자 맞춤형 결과물 생성 (파라미터값 설정 가능)
* 반복 작업 자동화 (효율성 향상)

---

# 2. 🧠 시스템 아키텍처

## 2-1. 전체 구조
### 시스템 아키텍쳐
<img width="1280" height="720" alt="슬라이드7" src="https://github.com/user-attachments/assets/afbb6460-1e8d-46ec-bb8f-7a2a649bc858" />
### 노드 아키텍쳐
<img width="1280" height="720" alt="슬라이드8" src="https://github.com/user-attachments/assets/506e1ec6-0034-4605-af04-22a1c7365b82" />


## 2-2. 핵심 특징

### ● 로봇 / 클라이언트 분리구조
* 실시간 제어 시스템(로봇)과 사용자 인터페이스(UI)의 요구사항을 둘다 충족시키기 위함
* 로봇: 안정성, 실시간성, 예외처리 중요
* 클라이언트: 사용자 경험, 확장성, 접근성 중요

### ● Action 기반 비동기 처리

* Goal / Feedback / Result 구조
* 진행률 실시간 피드백 제공 

### ● Web-ROS 연동

* HTTP → ROS2 Action 변환
* UI에서 작업 제어 및 상태 확인 가능

---

# 3. 🔄 전체 동작 흐름
<img width="468" height="851" alt="image" src="https://github.com/user-attachments/assets/e8a742bd-a579-4325-a8c6-2442e1a9b3f7" />

## 3-1. End-to-End Flow

1. 이미지 입력 (스마트폰 / DB)
2. 이미지 전처리 (Grayscale, Resize)
3. 점묘화 변환
4. 좌표 데이터 생성
5. ROS Action으로 전송
6. 로봇 점묘화 수행
7. 진행률 피드백
8. 작업 완료 및 UI 출력 

---

# 4. 🧩 핵심 기능 구성

## 4-1. Image Processing

### ● 점묘화 변환

* 밝기 기반 확률 샘플링
* 어두운 영역 → 높은 점 밀도
* 밝은 영역 → 낮은 점 밀도 

### ● 경계 보존

* Canny Edge Detection 활용
* 윤곽선 영역 점 밀도 증가

### ● 좌표 변환

* Pixel → Robot Coordinate(mm)

---

## 4-2. 점 분포 최적화

### ● 문제

* 격자 기반 → 인위적 패턴 발생

### ● 해결

* 확률 기반 Sampling 적용
* 자연스러운 점 분포 구현

---

## 4-3. 중복 점 방지

### ● 문제

* 동일 위치 반복 → 번짐 발생

### ● 해결

* 최소 거리 기반 필터링
* 마스크 기반 점 제거 로직 적용 

---

## 4-4. 색상 클러스터링

### ● 목표

* 실제 펜(18색)에 맞는 색상 매핑

### ● 방법

* LAB Color Space 기반 클러스터링
* 인간 시각 기준 색상 유사도 반영 

---

## 4-5. 경로 최적화

### ● 목표

* 이동 거리 최소화
* 작업 시간 단축

### ● 방법

* Grid 기반 Nearest Neighbor
* Local 탐색으로 연산량 감소

---

## 4-6. 로봇 제어

### ● 주요 기능

* 점 찍기 (movec / movel)
* 펜 교체 (18 colors)
* Z축 제어로 점 크기 조절

### ● 최적화

* Vel / Acc 기반 속도 제어
* 흔들림 최소화 파라미터 적용 

---

# 5. ⚙️ 시스템 안정성 설계

## 5-1. 서버 다운 대응

* 일정 시간 feedback 미수신 → 장애 감지
* 서버 복구 후 이어서 작업 수행 

## 5-2. 외력/비상정지 대응

* Safe Stop 상태 감지
* 작업 위치 저장 후 Resume

## 5-3. 충돌 방지

* 작업 영역 제한
* Z값 기반 충돌 회피

---

# 6. 🖥️ 개발 환경

| Category        | Stack             |
| --------------- | ----------------- |
| OS              | Ubuntu            |
| Middleware      | ROS2              |
| Language        | Python            |
| Vision          | OpenCV            |
| AI              | PyTorch           |
| Web             | HTML / JS / Flask |
| Version Control | GitHub            |

---

# 7. 🛠️ Hardware

* Doosan Robot M0609
* Robot Gripper
* Camera (Vision)
* Pen Palette (18 Colors)
* Custom Jig System 

---

# 8. ▶️ 실행 방법

```bash
# 1. ROS 환경 설정
export ROS_DOMAIN_ID=16

# 2. 빌드
cd ~/workspace
colcon build
source install/setup.bash

# 3. 노드 실행
ros2 run workflow_node
ros2 run vision_node
ros2 run planner_node
ros2 run robot_node
```

---

# 9. 🚀 성과 및 결과

* 점묘화 자동 생성 및 물리 드로잉 구현
* 18색 기반 실제 색상 표현
* 실시간 진행률 피드백 시스템 구축
* 작업 자동 복구 기능 구현

---

# 10. 📈 활용 가능성

* 관광지 체험형 콘텐츠
* 커스텀 아트 제작 서비스
* 전시/교육용 로봇 시스템
* 이벤트 및 마케팅 콘텐츠 

---

# 11. 📌 핵심 요약

* AI + Robotics 융합 시스템
* Image → Dot → Robot Execution 파이프라인
* ROS2 기반 모듈화 구조
* 안정성(복구/정지/재개)까지 고려한 설계

---

