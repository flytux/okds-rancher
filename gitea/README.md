#### 1. Gitea 설치 - single / sqllite 

```
k apply -f gitea-install.yaml

# ingress 접속 후 최초 설정 화면에서 server URL 설정 - 인그레스 주소
```

#### 2. 사용자 생성

```
argo / 12345678 로 사용자 생성 > Tekton 파이프라인 sa-kw-build.yml에서 참조
```
