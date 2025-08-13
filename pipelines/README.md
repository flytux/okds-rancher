#### 1. 파이프라인 설치

```
# build , deploy 네임스페이스 생성
k create ns build
k create ns deploy

# build 네임스페이스에 파이프라인 생성
k create -f ./
```
#### 2. 파이프라인 credential 정보 설정

```
sa-kw-build.yml 에서 docker registry / argocd 인증 정보 확인 후 설정
```
