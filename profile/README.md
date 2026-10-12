<div align="center">

# 🚕 Mobility DevOps

**Hyundai AutoEver Mobility SW School 4th · Taxi Dispatch Platform**

<br/>



</div>

---

## 📌 Overview

| 트랙 | 내용 |
|:---:|---|
| 🧑‍💻 **App** | 사용자·기사·차량·호출 CRUD, 호출 → 수락 → 도착 → 시작 → 완료/취소 상태 흐름 |
| 🔁 **CI** | Jenkins → SonarQube Cloud 품질 검사 → Trivy 이미지 스캔 → GHCR 푸시 |
| 🚀 **CD** | GitOps(Argo CD) + Argo Rollouts **Canary** 배포, prod 이상 시 자동 롤백 |
| 📈 **Ops** | Prometheus · Grafana · Loki 모니터링, Alertmanager → Slack 경보 |
| 🔐 **Security** | Tailscale, SSH 키 인증, fail2ban, Sealed Secrets, GitHub secret scanning |
| 🖥️ **Infra** | Private 온프레미스 — 호스트 PC + 노트북 서버, Vagrant VM 7대, Kubernetes 클러스터 |

## 🏗️ Architecture

<div align="center">
  <img src="https://raw.githubusercontent.com/mobility-devops/DevOps_Docs/main/architecture/images/architecture-simple.png" width="90%" alt="Architecture" />
</div>

<details>
<summary><b>🔎 배포 흐름 자세히 보기</b></summary>
<br/>

| 단계 | 하는 일 |
|---|---|
| **1. Push / PR** | GitHub webhook → Tailscale Funnel → Jenkins |
| **2. CI** | 테스트 → SonarQube Cloud → Docker 빌드 → Trivy → GHCR(digest) |
| **3. GitOps** | `DevOps_GitOps` 저장소의 이미지 digest 갱신 |
| **4. CD** | Argo CD 동기화 → Argo Rollouts Canary 단계 배포 |
| **5. 감시** | Prometheus 지표 분석 → 이상 시 자동 롤백 · Slack 알림 |

<div align="center">
  <img src="https://raw.githubusercontent.com/mobility-devops/DevOps_Docs/main/architecture/images/cd-simple.png" width="80%" alt="CD" />
  <br/><br/>
  <img src="https://raw.githubusercontent.com/mobility-devops/DevOps_Docs/main/architecture/images/monitoring-simple.png" width="80%" alt="Monitoring" />
</div>

</details>

## 📂 Repositories

| Repository | 역할 |
|---|---|
| [**DevOps_Backend**](https://github.com/mobility-devops/DevOps_Backend) | 🧩 앱 코드 · Dockerfile · Jenkinsfile |
| [**DevOps_GitOps**](https://github.com/mobility-devops/DevOps_GitOps) | 📦 배포 상태 (Kustomize, Argo CD) |
| [**DevOps_Infra**](https://github.com/mobility-devops/DevOps_Infra) | 🖥️ VM(Vagrant) · 서버 설정(Ansible) · 모니터링 |
| [**DevOps_Docs**](https://github.com/mobility-devops/DevOps_Docs) | 📚 아키텍처 · 가이드 · Runbook · ADR |

## 🛠️ Tech Stack

<div align="center">

**Application**<br/>
<img src="https://img.shields.io/badge/Java%2021-007396?style=for-the-badge&logo=openjdk&logoColor=white" />
<img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" />
<img src="https://img.shields.io/badge/MySQL%208.4-4479A1?style=for-the-badge&logo=mysql&logoColor=white" />
<img src="https://img.shields.io/badge/Flyway-CC0200?style=for-the-badge&logo=flyway&logoColor=white" />
<img src="https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white" />

**CI / CD**<br/>
<img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white" />
<img src="https://img.shields.io/badge/SonarQube%20Cloud-126ED3?style=for-the-badge&logo=sonarcloud&logoColor=white" />
<img src="https://img.shields.io/badge/Trivy-1904DA?style=for-the-badge&logo=aqua&logoColor=white" />
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/GHCR-181717?style=for-the-badge&logo=github&logoColor=white" />
<img src="https://img.shields.io/badge/Argo%20CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white" />
<img src="https://img.shields.io/badge/Argo%20Rollouts-EF7B4D?style=for-the-badge&logo=argo&logoColor=white" />

**Infrastructure**<br/>
<img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" />
<img src="https://img.shields.io/badge/Calico-FB8C00?style=for-the-badge&logo=projectcalico&logoColor=white" />
<img src="https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white" />
<img src="https://img.shields.io/badge/Vagrant-1868F2?style=for-the-badge&logo=vagrant&logoColor=white" />
<img src="https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white" />
<img src="https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white" />
<img src="https://img.shields.io/badge/Ubuntu%2024.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" />

**Observability & Security**<br/>
<img src="https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white" />
<img src="https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white" />
<img src="https://img.shields.io/badge/Loki-F2CC0C?style=for-the-badge&logo=grafana&logoColor=black" />
<img src="https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white" />
<img src="https://img.shields.io/badge/Tailscale-242424?style=for-the-badge&logo=tailscale&logoColor=white" />
<img src="https://img.shields.io/badge/Sealed%20Secrets-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" />

</div>

## 🖥️ Infrastructure at a Glance

| VM | 역할 | 머신 |
|---|---|---|
| `ci-01` | Jenkins, Docker | 호스트 PC |
| `k8s-master` | Control Plane | 호스트 PC |
| `k8s-worker1` · `k8s-worker2` | 앱, Gateway, 플랫폼 도구 | 호스트 PC |
| `k8s-worker3` | 앱, Gateway, 플랫폼 도구 | 노트북 서버 |
| `db-01` | MySQL 8.4 LTS | 호스트 PC |
| `mon-01` | Prometheus, Grafana, Loki | 호스트 PC |


## 👥 Team

| 이름 | 역할 |
|:---:|---|
| 김현서 | VM · Ansible · Backend |
| 손지원 · Lead  | Monitoring · Runbook |
| 임류경 | CD · GitOps |
| 방지우 | CI |

---

<div align="center">
  <sub>© 2026 Mobility DevOps · Hyundai AutoEver Mobility SW School 4th</sub>
</div>
