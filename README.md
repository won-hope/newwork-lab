# 🌐 Network Deep Dive Roadmap for Backend Engineers

> 단순한 패킷 전달을 넘어, 대규모 분산 시스템과 모바일 클라이언트 환경에서
> 네트워크 인프라가 백엔드 애플리케이션 성능에 미치는 영향을 밑바닥부터 파고드는 로드맵입니다.

## 🧱 1️⃣ 네트워크 기초와 추상화의 층위 (OSI 7계층)
**🎯 목표:** 네트워크 구조의 큰 틀을 이해하고, 각 계층의 캡슐화/역캡슐화 비용 인지하기

### 📚 학습 포인트
- **OSI 7계층 vs TCP/IP 4계층:** 왜 현대는 TCP/IP 모델을 실질적 표준으로 사용하는가?
- 패킷, 프레임, 세그먼트, 데이터그램의 차이와 페이로드(Payload) 구조.
- IP 주소(논리)와 MAC 주소(물리)의 매핑 원리 (ARP).
- **Deep Dive (Why):** 응용 계층의 데이터가 물리 계층으로 내려가며 붙는 헤더 오버헤드는 얼마나 되는가? 이것이 시스템 처리량에 미치는 영향은?

---

## ⚙️ 2️⃣ OS 커널과 네트워크의 만남 (IP & Socket)
**🎯 목표:** IP 라우팅의 기초를 다지고, 애플리케이션과 OS 네트워크 스택의 경계 허물기

### 📚 학습 포인트
- IPv4/IPv6 구조와 CIDR(서브넷 마스크) 계산.
- 정적/동적 라우팅 및 NAT, 방화벽의 기본 원리.
- **Socket Programming:** 커널 공간(Kernel Space)과 사용자 공간(User Space) 간의 네트워크 데이터 복사 비용.
- **Deep Dive (Why):** 백엔드 스레드가 네트워크 I/O를 대기할 때 OS 레벨에서 벌어지는 일 (Blocking vs Non-blocking, `epoll`, `kqueue`).

### 🧩 실습 및 적용
- AWS VPC, Subnet 직접 구성해 보기.
- Java/Spring Boot에서 단순 Socket 통신 구현 후, 스레드 덤프(Thread Dump) 분석해 보기.

---

## 🧩 3️⃣ TCP/IP 심화와 백엔드 병목 탐색
**🎯 목표:** 데이터 통신의 신뢰성 보장 메커니즘을 이해하고, 그것이 DB 및 API 성능에 미치는 영향 분석

### 📚 학습 포인트
- **TCP vs UDP의 본질:** 상태 기반(Stateful) 통신과 무상태(Stateless) 통신의 설계 철학 차이.
- TCP 3-Way Handshake & 4-Way Termination의 물리적 레이턴시 비용.
- 혼잡 제어(Congestion Control)와 흐름 제어(Flow Control) 메커니즘.
- **Deep Dive (Why):** 이 TCP 연결 비용 때문에 왜 DB Connection Pool(HikariCP)을 미리 맺어두어야 하며, HTTP Keep-Alive가 시스템 성능에 필수적인가?

### 🧩 실습 및 적용
- Wireshark로 로컬 서버 ↔ DB 간의 Handshake 패킷 캡처 및 RTT(Round Trip Time) 분석.

---

## 🖥️ 4️⃣ 실무 환경 아키텍처와 프로토콜 최적화
**🎯 목표:** 현대 웹/모바일 서비스에 맞는 네트워크 아키텍처 설계와 프로토콜 트레이드오프 분석

### 📚 학습 포인트
- L4 / L7 로드밸런싱의 차이점과 리버스 프록시(Nginx) 동작 원리.
- DNS 동작 과정과 레코드 타입(A, CNAME 등) 심화 분석.
- HTTPS와 TLS/SSL Handshake 과정에서의 암호화 연산 오버헤드.
- **Deep Dive (Why):** 지하철에서 IP가 바뀌거나 네트워크가 끊기는 모바일(App) 환경에서 TCP 연결은 어떻게 무너지는가? 이를 극복하기 위한 HTTP/3(QUIC)의 Connection Migration 원리는 무엇인가?

### 🧩 실습 및 적용
- Nginx로 리버스 프록시 구성 후 백엔드 서버 다중화 및 부하 분산 테스트.
- Project OHANA 등 실제 모바일-백엔드 연동 환경에서 네트워크 단절/지연 시나리오 구축 및 복구 테스트.

---

## 🧠 5️⃣ 장애 대응 및 대규모 시스템 아키텍처 (Staff Level)
**🎯 목표:** 시스템 장애 시 네트워크 계층부터 애플리케이션까지 Top-Down / Bottom-Up 디버깅 역량 확보

### 📚 학습 포인트
- 패킷 손실, 네트워크 지연, MTU(Maximum Transmission Unit) 불일치로 인한 원인 불명의 장애 해결법.
- 대규모 트래픽 시 발생하는 TIME_WAIT 소켓 고갈 문제와 OS 커널 파라미터 튜닝(`sysctl`).
- CDN의 엣지 캐싱(Edge Caching) 원리와 글로벌 트래픽 분산 전략.
- **Troubleshooting:** 장애 시뮬레이션 논리적 접근법 (ping → DNS → 라우팅 → 방화벽 → 애플리케이션 로그 순차 점검).

---

## 🚀 Repository Structure

```bash
📦 zero-to-network-deepdive/
 ┣ 📂 01_theory/           # TCP/IP, OSI 계층 등 핵심 개념 마크다운 정리
 ┣ 📂 02_wireshark/        # 3-Way Handshake, DB Connection 패킷 캡처 및 분석 로그
 ┣ 📂 03_architecture/     # AWS VPC, Nginx 로드밸런싱 구성도 및 설정 파일
 ┣ 📂 04_troubleshooting/  # 장애 시뮬레이션 및 트러블슈팅 일지 (TIME_WAIT 고갈 등)
 ┣ 📄 README.md            # 전체 학습 로드맵 및 진도표
 ┗ 📘 dev_notes.md         # 주차별 딥다이브 회고록 (Why에 대한 스스로의 답변)
