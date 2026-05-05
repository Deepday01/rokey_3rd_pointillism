# AI Pointillism Robot System

## Overview  
AI 이미지 처리 결과를 기반으로 협동로봇이 실제 펜으로 점묘화를 수행하는 자동화 시스템을 구현한다.  
Web–Server–ROS–Robot 전체 파이프라인을 통합하여 물리적 드로잉 시스템을 구축한다. 

---

## My Role
- ROS2 기반 로봇 제어 구조 설계 및 구현
- Web ↔ ROS ↔ Robot 통신 파이프라인 구축
- 로봇 Motion 제어 및 점묘화 로직 최적화
- 시스템 안정성 및 작업 복구 로직 구현

---

## System Architecture
[Web / Mobile]
↓
[Backend Server]
↓
[ROS2 Action Client]
↓
[ROS2 Action Server]
↓
[Robot]

---

## Key Contributions

### ROS2 Action 기반 제어
- Goal / Feedback / Result 구조 설계
- 실시간 진행률 피드백 구현
- Cancel / Resume 기능 구현

### Web–ROS 통신 브릿지
- HTTP → ROS2 Action 변환 구조 설계
- Token 기반 작업 분리
- 작업 상태 실시간 모니터링

### 로봇 Motion 제어
- MoveJ / MoveL / MoveC 혼합 제어
- Vel / Acc 기반 속도 최적화
- Z축 제어로 점 품질 균일화

### 안정성 및 복구 시스템
- Feedback 기반 서버 상태 감지
- 서버 다운 시 작업 이어서 수행
- 비상 정지 및 재개 로직 구현

---

## Tech Stack
- ROS2 (Humble)
- Python
- FastAPI, Flask
- OpenCV
- HTML / CSS / JavaScript
- Firebase
- Ubuntu
- GitHub
---

## Results
- 로봇 점묘화 자동화 시스템 구현
- 작업 효율 약 90% 향상
- 실시간 피드백 기반 안정적 시스템 구축

---

## Keywords
ROS2, Robotics, System Integration, Automation, Robot Control