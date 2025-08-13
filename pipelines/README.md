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
sa-kw-build.yml 에서 docker registry / gitea 인증 정보 확인 후 설정
```

#### 3. PipelineRun으로 테스트
```

# Git repo 주소, branch 명 등 확인 후

k create -f pr-kw-build.yml -n build
```
