# Kong Ingress Controller on Kubernetes
Gateway 도구로 Kong 을 사용하는 경우의 환경구성을 진행한다.

기본 Ingress 를 구성하고 Route Service 의 Network 장애 시의 Retry 정책 설정을 추가 적용한다.
### Retry 설정 정책
- `perTryTimeout` 3초
- `numRetries` 5회

# References
- [Kong Ingress on Minikube](https://docs.konghq.com/kubernetes-ingress-controller/2.12.x/deployment/minikube/)