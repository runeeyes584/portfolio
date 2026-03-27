# Docker Setup Guide

## Files Created

- **Dockerfile**: Định nghĩa Docker image với Nginx
- **nginx.conf**: Cấu hình Nginx server
- **.dockerignore**: File/folder loại trừ khỏi Docker build
- **docker-compose.yml**: Cấu hình để test locally

---

## 1. Build Docker Image Locally

```bash
docker build -t kaleidoscope428/portfolio:latest .
```

## 2. Test Locally với Docker

### Option A: Sử dụng docker run
```bash
docker run -p 8080:80 kaleidoscope428/portfolio:latest
```
Sau đó mở http://localhost:8080

### Option B: Sử dụng docker-compose
```bash
docker-compose up -d
```
Mở http://localhost:8080

---

## 3. Push lên Docker Hub

### Bước 1: Login Docker Hub
```bash
docker login
```
Nhập Docker Hub username và password (hoặc access token)

### Bước 2: Push image
```bash
docker push kaleidoscope428/portfolio:latest
```

### Bước 3: Tag version khác (optional)
```bash
docker tag kaleidoscope428/portfolio:latest kaleidoscope428/portfolio:1.0
docker push kaleidoscope428/portfolio:1.0
```

---

## 4. Sử dụng Image từ Docker Hub

### Chạy từ Docker Hub (sau khi push)
```bash
docker run -p 8080:80 kaleidoscope428/portfolio:latest
```

### Hoặc với docker-compose
```bash
# Sửa docker-compose.yml
# Thay: build: .
# Thành: image: kaleidoscope428/portfolio:latest

docker-compose up -d
```

---

## 5. Kiểm tra Status

```bash
# Danh sách images
docker images

# Danh sách containers đang chạy
docker ps

# Logs
docker logs <container_id>

# Stop container
docker stop <container_id>
```

---

## Notes

- Image size: ~30MB (Nginx Alpine)
- Port mặc định: 80 (trong container) -> 8080 (localhost)
- Tự động gzip compression cho static files
- Security headers đã được cấu hình

---

## Troubleshooting

**Docker daemon not running?**
- Mở Docker Desktop

**Permission denied?** (Linux/Mac)
- Thêm `sudo` trước lệnh docker

**Port 8080 đã sử dụng?**
- Thay đổi port: `docker run -p 9090:80 kaleidoscope428/portfolio:latest`
