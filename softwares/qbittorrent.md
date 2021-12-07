# qBittorrent

* qBittorrent 서버 및 웹 클라이언트 구성

## 설치

```bash
sudo apt install qbittorrent-nox
```

## 구성

### 초기 설정

```bash
qbittorrent-nox --profile=/home/<user>/.config/
```

* 실행 후, 웹 클라이언트로 접속하여 포트, 사용자 비밀번호 등 수정

### 서비스

```bash
sudo nano /usr/lib/systemd/system/qbittorrent-nox.service
```

* 파일 내용

```
[Unit]
Description=qBittorrent Command Line Client
After=network.target

[Service]
ExecStart=qbittorrent-nox --profile=/home/<user>/.config/
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable qbittorrent-nox --now
```

