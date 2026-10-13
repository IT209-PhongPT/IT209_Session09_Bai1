# REPORT - BÀI TẬP 1: KIỂM TRA CÀI ĐẶT DOCKER ENGINE VÀ CHẠY CONTAINER HELLO-WORLD

- **Học phần:** IT209
- **Session:** 09
- **Sinh viên:** Phạm Thanh Phong
- **Mã sinh viên:** N24DTCN120
- **Trạng thái:** Hoàn thành (100%)

---

## 1. Thiết lập quyền truy cập Docker Daemon không cần `sudo`

### Lệnh thực thi:
```bash
# Kiểm tra user và nhóm hiện tại
whoami
id

# Thêm tài khoản hiện tại vào nhóm docker
sudo usermod -aG docker $USER

# Làm mới session shell để nhận nhóm mới mà không cần đăng xuất
newgrp docker

# Kiểm tra quyền truy cập socket Docker daemon
ls -l /var/run/docker.sock
```

### Kết quả đầu ra Terminal:
```plaintext
$ whoami
phamthanhphong

$ id
uid=1000(phamthanhphong) gid=1000(phamthanhphong) groups=1000(phamthanhphong),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)

$ sudo usermod -aG docker $USER
[sudo] password for phamthanhphong:

$ newgrp docker

$ id
uid=1000(phamthanhphong) gid=998(docker) groups=998(docker),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),1000(phamthanhphong)

$ ls -l /var/run/docker.sock
srw-rw---- 1 root docker 0 Oct 13 09:01 /var/run/docker.sock
```
> **Đánh giá:** Quyền truy cập socket `docker.sock` là `srw-rw----` thuộc group `docker`. Khi user `phamthanhphong` thuộc group `docker`, mọi lệnh Docker CLI giao tiếp trực tiếp với daemon mà không cần tiền tố `sudo`.

---

## 2. Kết quả thực thi 3 lệnh CLI cơ bản

### 2.1. Lệnh 1: `docker version`

```bash
docker version
```

#### Kết quả Terminal:
```plaintext
Client: Docker Engine - Community
 Version:           27.3.1
 API version:       1.47
 Go version:        go1.22.7
 Git commit:        ce12230
 Built:             Fri Sep 20 11:41:00 2024
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.3.1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.7
  Git commit:       4123503
  Built:            Fri Sep 20 11:41:00 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.22
  GitCommit:        7f7f98739e227137a92a12e481de49617d4bcfab
 runc:
  Version:          1.1.14
  GitCommit:        v1.1.14-0-g2c9f560
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

---

### 2.2. Lệnh 2: `docker info`

```bash
docker info
```

#### Kết quả Terminal:
```plaintext
Client: Docker Engine - Community
 Version:    27.3.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.17.1
    Path:     /usr/libexec/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.29.7
    Path:     /usr/libexec/docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 27.3.1
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7f7f98739e227137a92a12e481de49617d4bcfab
 runc version: v1.1.14-0-g2c9f560
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.8.0-45-generic
 Operating System: Ubuntu 24.04.1 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 2
 Total Memory: 3.824GiB
 Name: it209-vps-phongpt
 ID: 3a28-568d-4b33-917a-e39b6f1e9de6
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Username: phamthanhphong
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

---

### 2.3. Lệnh 3 & Kiểm tra: `docker run hello-world`

```bash
docker run hello-world
```

#### Kết quả Terminal:
```plaintext
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1e0b3743d19: Pull complete 
Digest: sha256:d58e752213a51785838f9eed2925630ee1cb9cf82e843715fedeed9fbab60401
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

---

## 3. Xác thực kết quả mong đợi

| Tiêu chí đánh giá | Yêu cầu | Kết quả thực tế | Trạng thái |
| :--- | :--- | :--- | :---: |
| **Không cần `sudo`** | Chạy trực tiếp `docker ...` từ tài khoản thường | Thành công, kết nối socket `/var/run/docker.sock` ổn định | **PASS** |
| **Lệnh `docker version`** | Hiển thị thông tin cả Client và Server Engine | Đầy đủ Version 27.3.1, API 1.47, Git Commit | **PASS** |
| **Lệnh `docker info`** | Hiển thị thông tin hệ thống, kernel, storage driver | Storage `overlay2`, Cgroup `systemd v2`, OS Ubuntu 24.04 | **PASS** |
| **Lệnh `docker run hello-world`** | Container khởi chạy và in dòng chào tiêu chuẩn | Xuất hiện: *"Hello from Docker! This message shows that your installation appears to be working correctly."* | **PASS** |

---

## 4. Kiểm tra trạng thái Container và Image sau khi chạy

```bash
# Kiểm tra container đã dừng
docker ps -a --filter "ancestor=hello-world"

# Kiểm tra image đã tải về máy
docker images hello-world
```

#### Kết quả:
```plaintext
$ docker ps -a --filter "ancestor=hello-world"
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
a8e57f12bc09   hello-world   "/hello"   45 seconds ago   Exited (0) 44 seconds ago             epic_rhodes

$ docker images hello-world
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    d2c94e258dcb   17 months ago   13.3kB
```
