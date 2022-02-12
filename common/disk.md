# 디스크

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
