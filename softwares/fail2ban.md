# Fail2Ban 설치 및 구성

## 설치

```bash
sudo apt install fail2ban -y
```

## 구성

`/etc/fail2ban/jail.conf`에서 내용 수정

```
ignoreip = 127.0.0.1/8 ::1  192.168.0.0/24
bantime = -1
findtime = 60m
maxretry = 3
```
