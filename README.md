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
CI와 CD는 프로세스와 목적이 다르기 때문에 CI레파지토리와 CD레파지토리를 분리하였습니다.
<img alt="image" src="https://github.com/user-attachments/assets/8b367f98-0eb5-47bd-9cc3-f0ea4e6b9a18" />
CI레파지토리
- main브랜치에 코드 변화가 감지되면 Git Action이 트리거됩니다.
- 레파지토리의 코드를 jar 파일로 빌드합니다.
- Dockerfile을 통해 도커 이미지를 빌드합니다.
- Docker hub에 빌드된 이미지를 푸시합니다.
CD레파지토리
- 배포할 도커 이미지의 태그, 배포 전략과 관련된 설정 파일을 관리합니다.
- main 브랜치에 배포 설정 변경이 감지되면 Argo CD에서 이를 감지합니다.
- 마스터 노드에서 실행되는 Argo CD가 CD레파지토리의 배포 설정대로 워커 노드를 동기화합니다.

### 2. 로드 밸런싱
- 친구 요청, 차단 등의 기능을 제공합니다.
- 1:1 채팅 기능을 제공합니다. 차단된 유저에게는 채팅을 전송할 수 없습니다.

### 3. 서비스 장애 복구
- 기존 GPT 채팅 서비스를 Connet에서 동일하게 사용할 수 있습니다.
</br>


