<h1>MSA서비스 CICD 프로젝트</h1>
간단한 커뮤니티 서비스를 '게시글 서비스', '채팅 서비스'로 분리하여 MSA를 구현하고 Docker, Kubernetes, Git Action을 활용하여 CICD파이프라인을 구축합니다.
해당 레파지토리는 CD에 해당하는 레파지토리입니다.

<h2 id="technologies">🛠️ 기술</h2>

| Category | Stack |
| --- | --- |
| Language | Java |
| Framework | Spring Boot |
| Library | Spring Data JPA, Query DSL |
| Database | My SQL |
| Infra | Docker, Kubernetes, Argo CD, Helm, Git Action, AWS EKS, AWS Loadbalancer |
</br>
<h2>Deployment Architecture</h2>
<img alt="image" src="https://github.com/user-attachments/assets/547b26d9-795a-459e-ab56-fe724d58edf8" />

<h2>🛠️구현 사항</h2>

### 1. CICD 파이프라인 구축
<img alt="image" src="https://github.com/user-attachments/assets/8b367f98-0eb5-47bd-9cc3-f0ea4e6b9a18" />

- 오픈 그룹, 프라이빗 그룹 등 다양한 조건으로 그룹을 생성할 수 있습니다.
- 오픈 그룹을 입장하거나 프라이빗 그룹을 초대 받아 그룹을 입장할 수 있습니다.
- 그룹장은 그룹을 수정하거나 채널, 탭을 생성, 수정할 권한이 주어집니다.

### 2. 로드 밸런싱
- 친구 요청, 차단 등의 기능을 제공합니다.
- 1:1 채팅 기능을 제공합니다. 차단된 유저에게는 채팅을 전송할 수 없습니다.

### 3. 서비스 장애 복구
- 기존 GPT 채팅 서비스를 Connet에서 동일하게 사용할 수 있습니다.
</br>


