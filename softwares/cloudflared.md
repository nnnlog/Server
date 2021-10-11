# Cloudflared 설치 및 구성

* Cloudflare Tunnel Client

## 설치

* [Cloudflare Package Repository](https://pkg.cloudflare.com/) 사용
* https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation#linux

## 로그인

```bash
cloudflared tunnel login
```

## 터널 생성

```bash
cloudflared tunnel create <name>
```

## 터널 설정

```bash
sudo nano /etc/cloudflared/config.yml
```

* SSH 터널링

```yaml
tunnel: <uuid>
credentials-file: /home/<user>/.cloudflared/<uuid>.json

ingress:
  - hostname: <hostname>
    service: ssh://localhost:22
  - service: http_status:404
```

* https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/configuration/configuration-file/ingress

## 터널 시작

```bash
cloudflared tunnel run <name or uuid>
```

## 서비스 생성

```bash
sudo cloudflared service install
```

## DNS 설정

https://developers.cloudflare.com/cloudflare-one/tutorials/ssh#route-to-the-tunnel

## 도메인으로 SSH 접근

https://developers.cloudflare.com/cloudflare-one/tutorials/ssh#connect-from-a-client-machine