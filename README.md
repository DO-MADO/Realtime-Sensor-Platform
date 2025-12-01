<h1>🚀 실시간 대용량 데이터 시각화 및 원격 제어 플랫폼</h1> 

### *FastAPI + WebSocket + Web UI*


고성능 센서 장비(Edge)에서 발생하는 <strong>초당 10만 건(100kS/s)의 대용량 데이터</strong>를  
<strong>FastAPI WebSocket</strong>을 통해 웹 대시보드로 실시간 스트리밍하고,  
사용자 인터랙션을 장비 제어 로직에 즉시 반영하는 <strong>End-to-End 양방향 제어 시스템</strong>입니다.

<br>

## ✨ 핵심 성과
* **Full-Stack 아키텍처 설계:** [Edge Device ↔ Backend ↔ Frontend]로 이어지는 전체 데이터 파이프라인 단독 구축
* **실시간성(Real-time) 확보:** WebSocket 기반의 멀티 채널 브로드캐스팅 구현 (Latency 최소화)
* **안정적인 운영 환경:** `Systemd` + `Shell Script`를 활용한 **CI/CD 기반 배포 및 자동 복구(Auto-healing) 시스템** 구축
* **데이터 품질 관리:** **Pydantic**을 도입하여 I/O 데이터의 엄격한 유효성 검증(Validation) 및 타입 안정성 확보

<br>

## 🏗️ 시스템 아키텍처
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/85dbe282-314a-4906-acfa-4b2ba4370b13" />

<br>
<br>

## 🧩 주요 기능

### 📡 1. 실시간 데이터 스트리밍 파이프라인
* Edge Device의 Raw Data를 수집하여 **전처리(Pre-processing) 알고리즘** 수행
* FastAPI의 비동기(Async) 처리를 통한 고성능 **JSON 직렬화 및 WebSocket 송출**

### 🛠 2. RESTful API 기반 원격 제어
* 웹 UI의 설정값(파라미터)을 REST API로 수신하여 장비 동작 제어
* <strong>API 요청 검증(Request Validation)</strong>을 통해 잘못된 파라미터 유입 차단

### 📊 3. SPA 기반 실시간 모니터링 대시보드
* **Chart.js** 최적화를 통해 대량의 시계열 데이터를 끊김 없이 렌더링
* 사용자 편의성을 고려한 직관적인 UI/UX 배치 및 다크모드 지원

### 🤖 4. 배포 및 운영 자동화 (DevOps)
* **`deploy.sh`**: 환경 변수(`.env`) 분리 및 원클릭 배포 스크립트 작성
* **`systemd`**: 서비스 데몬 등록을 통한 부팅 시 자동 실행 및 프로세스 모니터링
  

<br>


## 🔧 구성 요소 및 역할

| 구분 | 파일 | 핵심 역할 |
| :--- | :--- | :--- |
| **🐍 백엔드 및 API 서버** | `app.py`, `pipeline.py` | API 라우팅, 데이터 스트림 파싱, JSON 직렬화 |
| **🧠 데이터 전처리 엔진** | `iio_reader.c` | 고속 데이터 수집 및 전처리 (Filter/Smoothing) |
| **🌐 프론트엔드 대시보드** | `index.html`, `app.js` | WebSocket 클라이언트 구현 및 차트 시각화 |
| **🤖 배포 및 운영 자동화** | `deploy.sh`, `adcserver.service` | CI/CD 스크립트 및 데몬 서비스 관리 |
| **🔐 환경 설정 관리** | `.env` | IP, Port, Secret Key 등 민감 정보 관리 |


<br>

## 🧑🏻‍💻 직접 사용한 기술
<table width="100%">
  <thead>
    <tr>
      <th width="15%">구분</th>
      <th width="45%">기술</th> <th width="40%">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><b>Backend & API</b></td>
      <td>
        <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white">
        <img src="https://img.shields.io/badge/Uvicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white">
        <img src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socket.io&logoColor=white">
        <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white">
        <img src="https://img.shields.io/badge/Pydantic-E92063?style=for-the-badge&logo=pydantic&logoColor=white">
      </td>
      <td>
        • <b>FastAPI + Uvicorn</b> 비동기 서버 구축<br>
        • <b>WebSocket</b> 기반 실시간 양방향 통신 구현<br>
        • <b>Pydantic</b>을 활용한 데이터 유효성 검증
      </td>
    </tr>
    <tr>
      <td align="center"><b>Frontend & UI</b></td>
      <td>
        <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black">
        <img src="https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chart.js&logoColor=white">
        <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
        <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
      </td>
      <td>
        • <b>SPA 구조</b>의 실시간 대시보드 UI 개발<br>
        • <b>Chart.js</b> 100kS/s 대용량 데이터 렌더링 최적화<br>
      </td>
    </tr>
    <tr>
      <td align="center"><b>DevOps & Infra</b></td>
      <td>
        <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black">
        <img src="https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white">
        <img src="https://img.shields.io/badge/OpenSSH-24292e?style=for-the-badge&logo=openssh&logoColor=white">
        <img src="https://img.shields.io/badge/Systemd-333333?style=for-the-badge&logo=linux&logoColor=white">
      </td>
      <td>
        • <b>Shell Script</b> 기반 원클릭 배포 자동화<br>
        • <b>OpenSSH 및 scp</b>를 이용한 보안 원격 접속 및 전송<br>
        • <b>Systemd</b> 서비스 자동 실행 및 복구 환경 구성
      </td>
    </tr>
    <tr>
      <td align="center"><b>Data Processing</b></td>
      <td>
        <img src="https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white">
        <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white">
        <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white">
      </td>
      <td>
        • Raw Data 노이즈 필터링 및 전처리 알고리즘<br>
        • 이기종 장비 간 직렬 통신 프로토콜 최적화
      </td>
    </tr>
  </tbody>
</table>


<br>

<h2>📁 디렉토리 구조 (요약본)</h2>
<pre>
zed/
 ├─ c/                       # DSP 처리부(C)
 ├─ python/server/           # FastAPI 서버 + WebSocket
 ├─ static/                  # Web UI
 ├─ service/                 # systemd + 자동화 스크립트
 ├─ logs/                    # 실시간 로그 저장
 ├─ deploy.sh                # 자동 배포
 ├─ .env                     # 환경 변수
 └─ README.md
</pre>

<br>

## 🚀 배포 및 운영 자동화
- 개발 환경(PC)에서 타겟 장비(Board)로의 코드 전송, 빌드, 서비스 재기동 과정을 스크립트로 자동화했습니다.


### ▶ 1) 원클릭 배포 자동화 (PC)
- 소스 코드 전송 -> 빌드 -> 서비스 재기동 (All-in-one)

<pre>
./deploy.sh
</pre>
### ▶ 2) 서비스 상태 모니터링 (Board)
- Systemd 기반의 자동 실행 및 상태 확인

<pre>
systemctl status adcserver.service
</pre>

### ▶ 3) 웹 대시보드 접속
- 브라우저에서 실시간 스트리밍 대시보드에 접속합니다.
<pre>
http://<BOARD_IP>:8000
</pre>

<br>



## 📜 프로젝트 성과
* **End-to-End 파이프라인 구축:** 데이터 발생부터 시각화까지 전 과정을 단독 설계하여 풀스택 역량 확보
* **양방향 제어 구조 완성:** 웹 UI의 변경 사항이 백엔드를 거쳐 즉시 장비 로직에 반영되는 **실시간 제어 루프** 구현
* **고성능 데이터 처리:** WebSocket 멀티 스트리밍을 통해 **초당 100k 샘플**의 데이터를 지연 없이(Low-latency) 웹으로 전송
* **운영 자동화:** 수동 배포의 번거로움을 제거하고, `Systemd`를 도입하여 **무중단 운영 환경** 기초 마련


<br>

<h2>📡 시스템 아키텍쳐 및 DSP 상세 파이프라인</h2>

<img width="1920" height="1080" alt="현재구성시스템아키텍쳐" src="https://github.com/user-attachments/assets/8eada624-0c1e-468e-aaab-0015253267ae" />
  
<img width="1013" height="1111" alt="보드DSP처리(C로직에서PYTHON)" src="https://github.com/user-attachments/assets/54c45ab9-de34-469b-a06a-26b6998fb8bf" />









<br>
<br>

<h2>🖼️ PC 모니터링 화면 및 UART0 실시간 로그</h2>
<img width="1913" height="899" alt="RawData탭" src="https://github.com/user-attachments/assets/1c6501e9-1c36-41a3-a6fa-0b5bc4b91bec" />
<img width="1907" height="887" alt="Configuration탭" src="https://github.com/user-attachments/assets/304ecaa8-193a-4ff8-b379-672a798e90e0" />
<img width="1909" height="899" alt="4ch탭" src="https://github.com/user-attachments/assets/de8bce6a-1a82-4464-a09e-94224362dc63" />
<img width="1073" height="1539" alt="4ch세부채널탭" src="https://github.com/user-attachments/assets/de50e702-9ffd-4883-96d8-fe41e3c60a23" />
<img width="1881" height="883" alt="Reset탭" src="https://github.com/user-attachments/assets/cb95ff0b-ed50-4c24-952e-9fd986ac9b4b" />
<img width="1905" height="909" alt="Save탭" src="https://github.com/user-attachments/assets/e6531251-7b3b-412d-bfb0-6efec36dfac7" />
<img width="1677" height="857" alt="UART0로그동시확인" src="https://github.com/user-attachments/assets/77f99098-9177-46a8-990d-a83fad71a908" />

<br>
<br>
<br>

<h2>🖥️ PC 모니터링 화면 상세 설명 </h2>


<img width="1913" height="899" alt="RawData탭_설명" src="https://github.com/user-attachments/assets/149951b9-32c8-463f-94cc-e1502c787101" />
<img width="1907" height="887" alt="Configuration탭_설명" src="https://github.com/user-attachments/assets/83ce8cf3-f275-4004-a36f-c45a2c8df860" />
<img width="1909" height="899" alt="4ch탭_설명" src="https://github.com/user-attachments/assets/71014b86-ff50-48f2-afae-b5092cef839f" />
<img width="1073" height="1539" alt="4ch세부채널탭_설명" src="https://github.com/user-attachments/assets/459a6ac8-71d5-42b4-9781-2843ef062d33" />
<img width="1881" height="883" alt="Reset탭_설명" src="https://github.com/user-attachments/assets/b50e9adf-ad3c-42b3-9978-74929c861db4" />
<img width="1905" height="909" alt="Save탭_설명" src="https://github.com/user-attachments/assets/b55961f1-ef23-4a0c-9e59-b15199f0f6a4" />



<h2>📜 라이선스</h2>
이 프로젝트는 사내 배포 및 테스트 목적으로 작성되었으며,<br>
외부 배포 시에는 관련 라이선스 및 NDA 정책을 준수해야 합니다.


