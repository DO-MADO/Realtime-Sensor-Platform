<h1>🚀 실시간 센서 데이터 시각화 및 원격 제어 웹 플랫폼 개발</h1> 

### *FastAPI + WebSocket + Web UI*


센서 장비에서 수집된 실시간 데이터를
<strong>FastAPI WebSocket → Web UI</strong>로 스트리밍하고,<br>
UI에서 변경한 파라미터가 즉시 장비에 반영되는
<strong>End-to-End 실시간 제어 시스템</strong>을 구축했습니다.

<br>

## ✨ 핵심 요약 (What I Built)
- <strong>센싱(C/DSP) → FastAPI 서버 → WebSocket 스트리밍 → Web UI 그래프 시각화</strong> 전체 흐름을 단독으로 설계·구현
- 실시간 파라미터 변경(샘플링·필터·계수) → 장비 즉시 반영
- 배포, 재시작, 환경 변수 분리까지 <strong>운영 자동화 구축(systemd + deploy.sh)</strong>

<br>

## 🏗️ 시스템 아키텍처
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/85dbe282-314a-4906-acfa-4b2ba4370b13" />

<br>
<br>

## 🧩 주요 기능

### 📡 1) 실시간 스트리밍 파이프라인
- AD4858 8ch 실시간 데이터 → 10단계 DSP 처리 → JSON 직렬화
- FastAPI WebSocket 멀티 스트림 브로드캐스트


### 🛠 2) 원격 파라미터 제어 (양방향)
- UI에서 변경한 옵션(필터·계수·샘플링레이트)을 REST API로 서버 전달
- 서버 → DSP(C 프로세스)로 즉시 반영


### 📊 3) 실시간 Web UI 시각화
- Chart.js 기반 실시간 그래프
- Raw/Stage별 그래프 탭
- CSV 다운로드


### 🤖 4) 운영/배포 자동화
- <code>deploy.sh</code> 원클릭 배포 (PC → 보드)
- <code>systemd</code> 부팅 자동 실행
- <code>.env</code>로 민감정보 분리
  

<br>


<h2>🔧 구성 요소 & 역할</h2>
<table border="1" cellpadding="6" cellspacing="0">
<tr><th>구성 요소</th><th>파일</th><th>설명</th></tr>
<tr>
  <td>🧠 DSP 처리부 (C)</td>
  <td><code>iio_reader.c</code></td>
  <td>ADC → LPF/평균/다항식 보정 → Frame Packer</td>
</tr>
<tr>
  <td>🐍 FastAPI 서버</td>
  <td><code>app.py</code>, <code>pipeline.py</code></td>
  <td>Stream 파싱, JSON 직렬화, WebSocket 송출</td>
</tr>
<tr>
  <td>🌐 Web UI</td>
  <td><code>index.html</code>, <code>app.js</code></td>
  <td>실시간 그래프 표시 + 옵션 변경 UI</td>
</tr>
<tr>
  <td>🤖 자동화 스크립트</td>
  <td><code>deploy.sh</code>, <code>start.sh</code>, <code>adcserver.service</code></td>
  <td>배포 자동화, systemd 실행</td>
</tr>
<tr>
  <td>🔐 환경 구성</td>
  <td><code>.env</code>, <code>.env.example</code></td>
  <td>SSH/IP/서비스명 등 환경 변수</td>
</tr>
</table>

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
        • <b>Pydantic</b>을 활용한 엄격한 데이터 유효성 검증
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


## ✨ 결과 & 성과

- <strong>End-to-End 실시간 스트리밍 파이프라인</strong> 단독 구성

- UI ↔ 서버 ↔ 장비 간 <strong>양방향 제어</strong> 구조 완성

- 총 5개 DSP 스테이지 스트림을 WebSocket으로 동시 송출 (저지연 구조)

- 운영 자동화 구축으로 수동 재배포/재시작 문제 완전 해결



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


