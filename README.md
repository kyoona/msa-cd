<h1>MSA서비스 CICD 프로젝트</h1>
해당 레파지토리는 CD에 해당하는 레파지토리입니다.<br/>
간단한 커뮤니티 서비스를 '게시글 서비스', '채팅 서비스'로 분리하여 MSA를 구현하고 Docker, Kubernetes, Git Action을 활용하여 CICD파이프라인을 구축합니다.
프로젝트 목적은 다음과 같습니다.

### 1. CICD 파이프라인 구축
CI와 CD는 프로세스와 목적이 다르기 때문에 CI레파지토리와 CD레파지토리를 분리하였습니다.
<img alt="image" src="https://github.com/user-attachments/assets/8b367f98-0eb5-47bd-9cc3-f0ea4e6b9a18" />
<br/>
CI 프로세스
- CI레파지토리는 서비스의 코드를 관리합니다.
- CI레파지토리의 main브랜치에 코드 변화가 감지되면 Git Action이 트리거됩니다.
- 레파지토리의 코드를 jar 파일로 빌드합니다.
- Dockerfile을 통해 도커 이미지를 빌드합니다.
- Docker hub에 빌드된 이미지를 푸시합니다.

CD 프로세스
- CD레파지토리는 배포할 도커 이미지의 태그, 배포 전략과 관련된 설정 파일을 관리합니다.
- CD레파지토리의 main 브랜치에 배포 설정 변경이 감지되면 Argo CD에서 이를 감지합니다.
- 마스터 노드에서 실행되는 Argo CD가 CD레파지토리의 배포 설정대로 워커 노드를 동기화합니다.
<br/>

### 2. 로드 밸런싱
AWS ALB를 사용하여 클라이언트 요청을 적절한 워커 노드의 Kubernetes Ingress로 전달하여 MSA 서비스 간 부하를 분산합니다.
<br/>

### 3. 서비스 장애 복구
ReplicaSet을 사용하여 항상 지정된 개수의 Pod를 유지될 수 있도록합니다. 특정 Pod가 장애로 종료되면, 자동으로 새로운 Pod를 생성합니다.
<br/>

### 4. 사용량에 따른 오토스케일링
HPA Controller를 통해 CPU 및 메모리 사용량을 실시간 모니터링 하며, 설정된 임계치를 초과하면 자동으로 Pod를 확장, 감소하면 Pod 수를 줄여 불필요한 리소스 사용을 방지합니다.
<br/>

<h2 id="technologies">🛠️ 기술</h2>

| Category | Stack |
| --- | --- |
| Language | Java |
| Framework | Spring Boot |
| Library | Spring Data JPA, Query DSL |
| Database | My SQL |
| Infra | Docker, Kubernetes, Argo CD, Helm, Git Action, AWS EKS, AWS Loadbalancer |
</br>
<h2>아키텍처</h2>
<img alt="image" src="https://github.com/user-attachments/assets/547b26d9-795a-459e-ab56-fe724d58edf8" />
Control plane에 해당하는 마스터 노드와 2개의 워커 노드로 쿠버네티스 클러스터가 구성되어 있습니다. <br/>
각 워커 노드의 pod에는 라우팅을 위한 Gateway역할을 하는 서비스, 게시판 서비스, 채팅 서비스가 컨테이너로 실행됩니다.
쿠버네티스 클러스터는 AWS의 EKS를 통해 배포되었습니다.
<img width="2026" alt="k8s-deault" src="https://github.com/user-attachments/assets/df71c9e2-47c5-42dc-9ed8-e45b1b974054" />



