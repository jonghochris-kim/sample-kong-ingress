# Kong Ingress Controller on Kubernetes
Gateway 도구로 Kong 을 사용하는 경우의 환경구성을 진행한다.

기본 Ingress 를 구성하고 Route Service 의 Network 장애 시의 Retry 정책 설정을 추가 적용한다.
### Retry 설정 정책
- `perTryTimeout` 3초
- `numRetries` 5회

## Kong Ingress Test
임의의 포트 번호(54000) 로 Port-forward 를 설정한다. 
```shell
# Port-forward 설정
$ kubectl port-forward service/kong-proxy -n kong 54000:80
```
별도의 터미널 세션에서 접속 테스트를 진행한다.
```shell
# 접속 테스트
$ curl -i -H 'Host:kong.example' http://localhost:54000/echo

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Content-Length: 135
Connection: keep-alive
Date: Fri, 27 Oct 2023 09:33:36 GMT
X-Kong-Upstream-Latency: 4
X-Kong-Proxy-Latency: 10
Via: kong/3.4.2

Welcome, you are connected to node minikube.
```

## Kong Retry 설정
echo 서비스가 `503` 인 경우의 Retry 정책이 정상작동하는지 살펴본다.

우선 서비스의 상태를 503 상태로 만들기 위해 echo 서비스의 http port number 를 변경한다.
```yaml
# 1027 에서 1028 로 변경
    - port: 1028
      name: http
      protocol: TCP
      targetPort: 1028
```



# References
- [Kong Ingress on Minikube](https://docs.konghq.com/kubernetes-ingress-controller/2.12.x/deployment/minikube/)