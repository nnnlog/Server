# Shadowsocks 구성 및 사용

## 서버

### 설치

[https://github.com/Jigsaw-Code/outline-ss-server/releases](https://github.com/Jigsaw-Code/outline-ss-server/releases)에서 다운 후 `tar xvzf <file>` 명령어를 사용하여 압축 해제

### 구성

* `config.yml`

```yaml
keys:
  - id: <username>
    port: <port>
    cipher: chacha20-ietf-poly1305
    secret: <password>
```

### 실행

```bash
./outline-ss-server -config=config.yml
```

### 서비스

* `/usr/lib/systemd/system/shadowsocks.service` 파일 내용

```
[Unit]
Description=Shadowsocks
After=network.target

[Service]
WorkingDirectory=<path>
User=root
ExecStart=./outline-ss-server -config=config.yml
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

* `<path>`는 `outline-ss-server`과 `config.yml`이 있는 경로

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now shadowsocks
```



## 클라이언트

### Ubuntu (CLI)

```bash
sudo apt install shadowsocks-libev
```

#### 실행

```bash
ss-local -s <server_host> -p <server_port> -l <local_proxy_port> -k <password>
```

* `socks5://127.0.0.1:<local_proxy_port>`로 사용

#### 테스트

```bash
curl http://ip-api.com/json -x "socks5://127.0.0.1:<local_proxy_port>"
```

#### 서비스

* ` /usr/lib/systemd/system/ss-local.service` 파일 내용

```
[Unit]
Description=Shadowsocks client proxy
After=network-online.target

[Service]
Type=simple
User=ro
ExecStart=ss-local -s <server_host> -p <server_port> -l <local_proxy_port> -k <password>
Restart=on-failure
RestartSec=30

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now ss-local
```

### Android

https://play.google.com/store/apps/details?id=com.github.shadowsocks

### Windows

https://github.com/shadowsocks/shadowsocks-windows/releases

### Ubuntu (Desktop)

https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation