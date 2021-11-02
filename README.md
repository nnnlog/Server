# 서버 설치 자료

* 서버 재설치를 위한 자료 정리

## 네트워크

#### 고정 아이피 할당

* `/etc/netplan/*.yaml`

```yaml
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

> or 공유기에서 고정 할당

## 디스크

* [`ubuntu--vg-ubuntu--lv` 크기 변경](https://askubuntu.com/questions/1106795/ubuntu-server-18-04-lvm-out-of-space-with-improper-default-partitioning)

#### NTFS 디스크 잡기

```bash
sudo apt-get install -y ntfs-3g
sudo mkdir /media/D
sudo mount -t ntfs-3g /dev/sdb1 /media/D/
```

재부팅 후에도 로딩하려면 `/etc/fstab`에 다음 내용을 추가

```
/dev/sdb1 /media/D ntfs-3g exec,permissions,auto 0 0
```

마운트된 폴더 소유자 변경

```bash
sudo chown $USER:$USER /media/D
```

## 그래픽 카드 드라이버 설치 오류 해결

* gcc, g++ 설치

1. 그래픽 관련 프로세스 정지 확인 (gdm, sddm 등)
2. https://unix.stackexchange.com/questions/440840/how-to-unload-kernel-module-nvidia-drm/441811#441811
3. https://linuxconfig.org/how-to-disable-nouveau-nvidia-driver-on-ubuntu-18-04-bionic-beaver-linux

## CUDA 설치

1. Offline (Runfile) 선택해 다운로드
2. 그래픽 드라이버 설치 옵션은 해제

* 환경 변수 등록은 `/etc/profile`에 다음 내용을 추가

```
# CUDA Install
export PATH=$PATH:/usr/local/cuda-11.4/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.4/lib64
```

* 현재 세션에서 바로 환경 변수를 갱신하려면, `source /etc/profile`을 입력

## 절전 모드 비활성화

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

## 소프트웨어

* [softwares/](./softwares/) 참조

