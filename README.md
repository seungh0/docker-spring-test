# Nginx Reverse Proxy Server

### Forward Proxy Server vs Reverse Proxy Sever

### - Forward Proxy
* 내부망 PC or 서버들이 외부망에 접속할때, 먼저 Proxy Server를 거쳐서 외부망에 연결되는 방식

1. 보안: Proxy Server 에서 In/Out bound 패킷에 대한 보안 정책(Content filtering 등)을 적용할 수 있음.
2. 성능: Proxy Server는 내부에 Cache를 유지하며 이미 한번 통신한 외부 서버의 이미지, 파일 등을 저장할 수 있음. 내부 사용자가 외부 서버에 접속시, Cache에 데이터가 있으면, Proxy 서버가 데이터를 제공하여 빠른 통신을 지원한다.

### - Reverse Proxy
* 외부에서 내부 서버가 제공하는 서비스 접근 시, Proxy 서버를 먼저 거쳐서 내부 서버로 들어오는 방식.
1. 보안: 외부 사용자는 실제 내부망에 있는 서버의 존재를 모른다. 모든 접속은 Reverse Proxy 서버에게 들어오며, Reverse Proxy는 요청에 매핑되는 내부 서버의 정보를 알고 요청을 넘겨준다.
따라서 내부 서버의 정보를 외부로부터 숨길 수 있다.
2. 로드 밸런싱: Proxy 서버가 내부 서버의 정보를 알고 있으므로, 로드 밸런싱을 통해 부하 여부에 따라 요청을 분배 할 수 있다.

### Nginx Install & Setup Reverse Proxy

Install Nginx
```
sudo apt-get update
sudo apt-get install nginx
sudo unlink /etc/nginx/sitese-enabled/default
cd /etc/nginx/sites-available
vim reverse-proxy.conf
```

#### revese-proxy.conf
```
server {
        listen 80;
        listen [::]:80;

        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;

        location / {
                    proxy_pass http://127.0.0.1:8080;
  }
}
```

#### 설정 Nginx에 적용 후 Nginx 재시작
```
sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf 
nginx -t
sudo systemctl restart nginx
```

---
* [개인 블로그]

[개인 블로그]: https://willseungh0.tistory.com/7?category=833680