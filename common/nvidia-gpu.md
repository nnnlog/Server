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

