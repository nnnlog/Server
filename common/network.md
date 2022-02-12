# 네트워크

#### 고정 아이피 할당

- `/etc/netplan/*.yaml`

```
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp4s0:
      addresses:
      - 192.168.123.200/24
      gateway4: 192.168.123.1
      nameservers:
        addresses:
        - 1.1.1.1
        - 1.0.0.1
        search: []
  version: 2
```

> 또는 공유기에서 고정 할당

#### Wake on LAN (WOL) 활성화

* WOL은 네트워크를 통해 컴퓨터를 부팅하는 기능이다.
* WOL을 사용하려면, 바이오스에서 네트워크를 통해서 부팅하는 것을 **먼저** 활성화해야 한다.
* ifconfig와 ethtool이 설치되어 있지 않으면, `net-tools`와 `ethtool`을 설치하면 된다.

```bash
ifconfig
```

네트워크 인터페이스의 이름을 확인한다. (ex. `enp4s0`, ``)

```bash
sudo ethtool <name>
```

_ex. `sudo ethtool enp4s0`_

`Supports Wake-on`에 `g`가 포함되어 있으면서 `d`가 없으면, WOL을 사용할 수 있다.

```bash
sudo ethtool -s <name> wol g
```

_ex. `sudo ethtool -s enp4s0 wol g`_

WOL을 활성화한다.

컴퓨터가 재부팅될 때마다 위 명령어를 다시 쳐주어야 하기 때문에, 위 명령어를 부팅 때마다 실행하는 서비스를 만든다.

```bash
sudo nano /usr/lib/systemd/system/wol.service
```

```
[Unit]
Description=Enable Wake On Lan

[Service]
Type=oneshot
ExecStart=ethtool -s <n wol g

[Install]
WantedBy=basic.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now wol
```

