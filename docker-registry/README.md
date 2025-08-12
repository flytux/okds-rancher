openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes \
  -keyout docker.key -out docker.crt -subj '/CN=docker.local' \
  -addext 'subjectAltName=DNS:docker.local'

kubectl create secret tls docker-tls --key docker.key --cert docker.crt -n docker-registry

cp docker.* /etc/pki/ca-trust/source/anchors/

update-ca-trust

