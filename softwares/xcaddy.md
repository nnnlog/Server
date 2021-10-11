# xcaddy 설치

https://github.com/caddyserver/xcaddy#install

## SSL 인증서 자동 발급 설정

* https://caddy.community/t/how-to-use-dns-provider-modules-in-caddy-2/8148

```bash
xcaddy build --with github.com/caddy-dns/cloudflare
```

* Caddyfile 상단에 전역 설정 추가

```
{
	acme_dns cloudflare <token>
}
```

## 서비스 등록

* `/usr/lib/systemd/system/caddy.service`

```
[Unit]
Description=caddy
After=network.target

[Service]
WorkingDirectory=/home/<user>/caddy/
Environment=
Type=simple
User=root
ExecStart=/home/<user>/caddy/caddy run
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

* 자동 시작 및 활성화

```bash
sudo systemctl daemon-reload
sudo systemctl enable caddy --now
```

