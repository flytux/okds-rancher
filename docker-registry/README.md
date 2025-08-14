### Docker registry 설치

#### 1. DNS 용 사설 인증서 생성
```
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes \
  -keyout docker.key -out docker.crt -subj '/CN=docker.local' \
  -addext 'subjectAltName=DNS:docker.local'
```

#### 2. 인증서 Secret 생성
```
kubectl create ns docker-registry
kubectl create secret tls docker-tls --key docker.key --cert docker.crt -n docker-registry
```

#### 3. 노드 (마스터/워커)에 ca 인증서에 추가 
```
cp docker.* /etc/pki/ca-trust/source/anchors/

update-ca-trust
```

#### 4. Docker Registry 설치
```
helm upgrade -i docker-registry -f values.yaml docker-registry-3.0.0.tgz --create-namespace -n docker-registry
```
#### 5. ContainerD 설정에 사설 레지스트리 추가
- Rke 방식
```

cat << EOF >> /etc/hosts
192.168.122.11 docker.local # Ingress IP
EOF

cat << EOF > /etc/rancher/rke2/registries.yaml
mirrors:
  docker.io:
    endpoint:
      - "https://docker.local"
configs:
  "docker.local":
    auth:
      username: admin # 레지스트리 ID
      password: vmsgX2!sm(Ts # 레지스트리 패스워드
    tls:
      cert_file: /etc/pki/ca-trust/source/anchors/docker.crt # Rocky Linux
      key_file: /etc/pki/ca-trust/source/anchors/doker.key
EOF

# rke2 서버 재기동
systemctl restart rke2-server
