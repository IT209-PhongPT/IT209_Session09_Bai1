# IT209 - Session 09 - Bài tập 1: Kiểm tra cài đặt Docker Engine và chạy Container Hello-World

- **Sinh viên:** Phạm Thanh Phong
- **MSSV:** N24DTCN120
- **Học phần:** IT209 

---

## Danh mục tệp tin trong thư mục bài tập

| Tên tệp tin | Mô tả chức năng |
| :--- | :--- |
| [REPORT.md](./REPORT.md) | **Tệp tin báo cáo nộp bài chính thức:** Chứa đầy đủ kết quả đầu ra thực tế của Terminal theo yêu cầu đề bài |
| [IT209_Session09_BT1_PhamThanhPhong_N24DTCN120.md](./IT209_Session09_BT1_PhamThanhPhong_N24DTCN120.md) | Báo cáo chi tiết, phân tích kiến trúc, sơ đồ tuần tự và cơ chế phân quyền non-root socket |

---

## Tóm tắt các bước thực hiện nhanh

```bash
# 1. Thêm user vào group docker để không cần gõ sudo
sudo usermod -aG docker $USER
newgrp docker

# 2. Kiểm tra phiên bản Docker Client & Server
docker version

# 3. Kiểm tra thông tin cấu hình hệ thống Docker Daemon
docker info

# 4. Chạy container đầu tiên
docker run hello-world
```
