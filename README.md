# Docker/Kubernetes 기반 티켓 시스템 인프라 구축

## 프로젝트 소개

Docker와 Kubernetes를 활용하여 오픈소스 헬프데스크 시스템(osTicket)을 구축하고, 컨테이너 오케스트레이션을 통한 서비스 운영 환경을 구현한 프로젝트입니다.

단순히 애플리케이션을 실행하는 것에 그치지 않고, Kubernetes의 Self-Healing 기능, Persistent Volume(PVC)을 이용한 데이터 영속성, ELK Stack 기반 로그 모니터링, Trivy를 이용한 컨테이너 보안 점검까지 실제 운영 환경을 고려하여 구축하였습니다.

---

## 프로젝트 기간

2026.06.30 ~ 2026.07.14

---

## 프로젝트 목표

- Docker 기반 컨테이너 환경 구축
- Kubernetes를 활용한 서비스 운영
- Pod 장애 발생 시 자동 복구(Self-Healing) 구현
- Persistent Volume(PVC)을 통한 데이터 영속성 보장
- ELK Stack을 이용한 로그 수집 및 모니터링
- Trivy를 활용한 컨테이너 보안 점검

---

## 기술 스택

### OS

- Ubuntu Server

### Container

- Docker
- Docker Compose

### Orchestration

- Kubernetes

### Database

- MySQL 5.7

### Application

- osTicket

### Monitoring

- Fluent Bit
- Elasticsearch
- Kibana

### Security

- Trivy

---

## 프로젝트 구조

```
Project1
│
├── Kubernetes
│   ├── namespace.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── mysql-pvc.yaml
│   ├── osticket-deployment.yaml
│   ├── osticket-service.yaml
│   ├── elasticsearch.yaml
│   ├── kibana.yaml
│   └── fluent-bit.yaml
│
├── security-images
│   ├── Dockerfile.mysql57-secure
│   └── Dockerfile.osticket-secure
│
└── docker-compose.yml
```

---

## 주요 구현 내용

### Docker 기반 서비스 구축

- Docker Compose를 이용하여 osTicket과 MySQL 컨테이너 구성
- 컨테이너 간 네트워크 연결

---

### Kubernetes 배포

- Namespace 구성
- Deployment 생성
- Service(NodePort) 구성
- Secret을 통한 환경변수 관리
- PVC(Persistent Volume Claim) 적용

---

### 장애 복구(Self-Healing)

- Pod 삭제 시 Kubernetes가 자동으로 새로운 Pod 생성
- 서비스 중단 없이 자동 복구 확인

---

### 데이터 영속성

- PVC를 사용하여 MySQL 데이터 저장
- Pod 삭제 후에도 데이터 유지 확인

---

### 로그 모니터링

- Fluent Bit를 이용한 로그 수집
- Elasticsearch 저장
- Kibana Dashboard를 이용한 로그 시각화

---

### 보안 점검

- Trivy를 이용한 컨테이너 이미지 취약점 검사
- 취약점 분석 및 보안 개선

---

##  주요 문제 해결

### MySQL CrashLoopBackOff

**문제**

- MySQL Pod가 반복적으로 종료

**해결**

- MySQL 5.7 이미지 적용
- Secret 및 PVC 설정 수정
- 리소스 설정 조정

---

### 로그 미수집 문제

**문제**

- Kibana에서 HTTP 요청 로그가 확인되지 않음

**해결**

- Fluent Bit 설정 수정
- Index Pattern 및 KQL 필터 점검
- nginx 로그 수집 경로 확인

---

### etcd 문제와 데이터 유실

**문제**

- etcd DB 손상(내부 인덱스가 깨짐)

**해결**

- kind 클러스터 재생성

---

##  프로젝트를 통해 배운 점

- Docker와 Kubernetes 기반 서비스 운영 경험
- 컨테이너 오케스트레이션 이해
- 장애 대응(Self-Healing) 및 데이터 영속성 구현
- ELK Stack 기반 로그 분석 경험
- PVC는 Pod 장애에는 강하지만 kind 클러스터 삭제에는 취약


