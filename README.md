# 🌐 Network Study Roadmap

> 네트워크를 밑바닥부터 배우기 위한 5단계 로드맵  
> 실습 중심으로 기초부터 실무까지 단계별로 정리했습니다.

---

## 🧱 1️⃣ 네트워크 기초 이해 (OSI 7계층 중심)

**🎯 목표:** 네트워크 구조의 큰 틀과 기본 개념 이해

### 📚 학습 포인트
- 네트워크란 무엇인가? IP의 역할은?
- **OSI 7계층** (물리 → 응용 계층) 역할 정리
- LAN / WAN / 인터넷 구조
- 패킷, 프레임, 프로토콜 개념
- IP 주소, MAC 주소, 포트 번호 기초

### 🧩 학습 방법
- 교재: _그림으로 배우는 네트워크 원리_
- 유튜브: 생활코딩 네트워크편 / Computer Networking Crash Course
- 연습: OSI 7계층 도식화 + 각 계층 프로토콜 연결

---

## ⚙️ 2️⃣ IP, 서브넷, 라우팅 기본기

**🎯 목표:** IP 구조 및 네트워크 분할 개념 습득

### 📚 학습 포인트
- IPv4 구조 (Network / Host bit)
- 서브넷 마스크, CIDR 계산
- 게이트웨이 / NAT / DNS 동작 원리
- 라우팅: 정적 vs 동적
- ping / traceroute / nslookup 명령어

### 🧩 학습 방법
- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) 설치 후 ping 실습  
- CIDR 계산 연습 (`192.168.10.0/27` 등)
- 교재: _Do it! 네트워크 입문_ / _TCP/IP 쉽게, 더 쉽게_

---

## 🧩 3️⃣ TCP/IP 심화 및 통신 흐름 분석

**🎯 목표:** 실제 데이터 통신 과정을 패킷 단위로 이해

### 📚 학습 포인트
- TCP 3-way handshake / 4-way termination
- UDP vs TCP 비교
- 포트 개념, HTTP 통신 구조
- ARP, ICMP, DHCP, DNS 상세 동작
- NAT, 방화벽 동작 원리

### 🧩 학습 방법
- Wireshark로 패킷 캡처  
  → google.com 접속 시 TCP handshake 패킷 확인  
  → DNS 요청/응답 분석
- 인프런 「네트워크 올인원 패킷분석」 / KOCW 「컴퓨터 네트워크」
- 블로그 정리: “TCP 연결이 실제로 만들어지는 과정”

---

## 🖥️ 4️⃣ 실무 환경 & 서버 네트워킹

**🎯 목표:** 웹/서버 개발자가 알아야 할 네트워크 실무 감각 습득

### 📚 학습 포인트
- IP 할당, 라우터 설정, 포트포워딩
- 로드밸런싱, 프록시, 리버스 프록시
- DNS 레코드 (A, CNAME, MX, TXT)
- 클라우드 네트워크 (AWS VPC, Subnet, Security Group)
- HTTPS, SSL 인증서 구조

### 🧩 학습 방법
- AWS Free Tier로 VPC/Subnet 구성 실습
- Nginx Reverse Proxy 설정 (Node.js 3000 → 80포트)
- 교재: _그림으로 배우는 클라우드 네트워크_

---

## 🧠 5️⃣ 심화 & 문제 해결 중심 학습

**🎯 목표:** 네트워크 장애 대응 능력 및 면접 대비

### 📚 학습 포인트
- 패킷 손실, 지연, NAT loopback, MTU 이슈
- 네트워크 보안 (TLS handshake, Firewall rule)
- VPN, VLAN, SDN 개념
- HTTP/2, QUIC, CDN 동작 원리

### 🧩 학습 방법
- 장애 시뮬레이션: ping 안될 때 ARP → Routing → DNS → Firewall 순서 점검
- 면접 대비 질문 정리
  - TCP와 UDP의 차이점은?
  - 3-way handshake를 왜 하는가?
- 교재: _TCP/IP Illustrated_ (심화서)

---

## 🗂️ 정리된 학습 순서

| 단계 | 학습 주제 | 실습 도구 | 추천 기간 |
|------|------------|------------|------------|
| 1단계 | OSI 7계층, 기본 용어 | 없음 | 1주 |
| 2단계 | IP/Subnet/DNS | Packet Tracer | 1~2주 |
| 3단계 | TCP/IP, 패킷분석 | Wireshark | 2~3주 |
| 4단계 | 서버 네트워킹, AWS | AWS/Nginx | 2주 |
| 5단계 | 장애대응, 심화 | 문제풀이 | 상시 |

---

## 🚀 추천 레포 구조 (예시)

```bash
📦 zero-to-network/
 ┣ 📂 theory/           # 이론 정리
 ┣ 📂 labs/             # 실습 스크린샷, 구성 파일
 ┣ 📂 wireshark/        # 패킷 분석 캡처
 ┣ 📂 aws-vpc/          # 클라우드 네트워크 실습
 ┣ 📄 README.md         # 학습 로드맵
 ┗ 📘 notes.md          # 주차별 공부 기록
