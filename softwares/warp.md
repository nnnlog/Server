# Warp 설치

## 설치

```bash
sudo apt install cloudflare-warp
```

## 등록

```bash
warp-cli register
```

## 연결

```bash
warp-cli connect
```

## 프록시

### 프록시 설정

```bash
warp-cli set-mode proxy
```

### 프록시 포트 변경

```bash
warp-cli set-proxy-port <PORT>
```

### 테스트

```bash
curl http://ip-api.com/json -x "socks5://127.0.0.1:<PORT>"
```

* 변경된 IP 확인

```bash
curl https://www.cloudflare.com/cdn-cgi/trace/ -x "socks5://127.0.0.1:<PORT>"
```

* `warp=on` 확인

