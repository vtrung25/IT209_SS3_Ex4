# Bài 4 — Nginx Virtual Hosts trên nhiều cổng

## Server blocks

- `nginx/beta-app.conf` lắng nghe TCP `8080`, phục vụ `/var/www/beta-app/html/`.
- `nginx/internal-app.conf` lắng nghe TCP `8090`, phục vụ `/var/www/internal-app/html/`.
- Mỗi thư mục `html/` chứa trang `index.html` riêng.

Chép hai cấu hình vào `/etc/nginx/sites-available/`, tạo symlink tương ứng trong `/etc/nginx/sites-enabled/`, sau đó chạy `sudo nginx -t` trước khi reload Nginx.

## Tường lửa

Trên Ubuntu, cho phép hai cổng:

```bash
sudo ufw allow 8080/tcp
sudo ufw allow 8090/tcp
sudo ufw status verbose
```

Trên DigitalOcean Cloud Firewall, thêm inbound TCP `8080` và TCP `8090` từ nguồn cần truy cập rồi gán firewall vào Droplet.

## Kiểm tra website

```bash
curl http://<IP_ADDRESS_DROPLET>:8080
curl http://<IP_ADDRESS_DROPLET>:8090
```

Cổng 8080 trả tiêu đề `Beta App`; cổng 8090 trả tiêu đề `Internal App`.
