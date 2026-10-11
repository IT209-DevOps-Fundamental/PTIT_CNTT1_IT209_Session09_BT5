# Bài Tập 5: Khởi Chạy Dịch Vụ Đơn Giản Với Docker Compose

## 1. Mục tiêu
- Sử dụng Docker Compose CLI v2 để quản lý vòng đời của dịch vụ web thông qua cấu hình khai báo (declarative config).
- Khởi chạy dịch vụ ở chế độ chạy ngầm (`-d`), ánh xạ cổng `8082:80`, kiểm tra phản hồi và hạ dịch vụ an toàn.

---

## 2. Cấu hình Docker Compose
Nội dung tệp `docker-compose.yml`:
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8082:80"
```

---

## 3. Các bước thực thi và Kết quả Terminal

### Bước 1: Khởi chạy dịch vụ ở chế độ chạy ngầm
Lệnh thực thi:
```bash
docker compose up -d
```

Kết quả Terminal:
```text
[+] Running 2/2
 ✔ Network bt5_default  Created                                            0.1s 
 ✔ Container bt5-web-1  Started                                            0.5s 
```

---

### Bước 2: Kiểm tra trạng thái dịch vụ đang chạy
Lệnh thực thi:
```bash
docker compose ps
```

Kết quả Terminal:
```text
NAME        IMAGE          COMMAND                  SERVICE   CREATED         STATUS         PORTS
bt5-web-1   nginx:alpine   "/docker-entrypoint.…"   web       6 seconds ago   Up 5 seconds   0.0.0.0:8082->80/tcp
```
> **Đánh giá**: Dịch vụ `web` (container `bt5-web-1`) đang chạy bình thường (`Up 5 seconds`), cổng container `80/tcp` được ánh xạ chuẩn ra cổng host `8082`.

---

### Bước 3: Kiểm tra phản hồi qua lệnh curl
Lệnh thực thi:
```bash
curl http://localhost:8082
```

Kết quả Terminal:
```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

---

### Bước 4: Hạ và dọn dẹp dịch vụ
Lệnh thực thi:
```bash
docker compose down
```

Kết quả Terminal:
```text
[+] Running 2/2
 ✔ Container bt5-web-1  Removed                                            0.3s 
 ✔ Network bt5_default  Removed                                            0.1s 
```

---

## 4. Kết luận
- Quản lý dịch vụ thành công bằng Docker Compose v2 với tệp cấu hình `docker-compose.yml`.
- Lệnh `docker compose ps` hiển thị rõ service web đang chạy và lắng nghe trên port `8082`.
- Lệnh `curl http://localhost:8082` trả về trang chào mừng của Nginx ("Welcome to nginx!").
- Lệnh `docker compose down` dọn dẹp hoàn toàn container và network đã tạo.
