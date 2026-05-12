# BTAPSO3
# MÔN PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ
---
## Họ tên: Nguyễn Thị Xuân Phương
## MSSV: K225480106054
## Lớp K58KTP.01
---
## Bài tập 3: Sử dụng wordpress để tạo website
## Deadline: 23h59 ngày 12 tháng 5 năm 2026.
---
# YÊU CẦU:
## Triển khai WordPress bằng Docker trên ubuntu
1. SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ TẠO docker ccompose chứa:
- Mariadb: sử dụng image: mariadb:latest để làm hệ quản trị csdl cho wordpress
- Phpmyadmin: sư dụng image: phpmyadmin:latest để đăng nhập vào mariadb rồi tạo csdl trống (chỉ để xem, ko cần tạo bảng từ đây, wordpress sẽ làm hết)
- WordPress: Sử dụng image: wordpress:latest, truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin
  
2. Yêu cầu: sau khi có 3 service này trong file docker-compose.yml :
- Cấu hình để hệ thống chạy
- Sử dụng cloudflare tunnel để public web này lên 1 sub-domain
- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...
- Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...
- Nhận xét việc sử dụng mã nguồn mở wordpress để tạo website (tốn công sức thế nào, dễ/khó dùng ra sao, tốn kém tài nguyên(ssh/ram) của máy chủ ra sao,....)
---

# BÀI LÀM
# Cấu trúc dự án 
```
~/thuha_wordpress/
├── docker-compose.yml       # File cấu hình các dịch vụ Docker
├── .env                     # File lưu trữ biến môi trường (mật khẩu, tên DB)
├── README.md                # Hướng dẫn chi tiết cách chạy và thông tin bài tập
└── data/                    # Thư mục chứa dữ liệu bền vững (tự động tạo khi chạy)
    ├── db_data/             # Dữ liệu của MariaDB
    └── wp_data/             # Mã nguồn và ảnh của WordPress
```
---

# CÁC BƯỚC CÀI ĐẶT 
## Bước 1. Tạo thư mục dự án 
```bash
# Tạo thư mục dự án
mkdir phuong_wordpress
# Di chuyển vào thư mục dự án
cd phuong_wordpress
# Tạo thư mục data
mkdir -p data/db_data data/wp_data
```
<img width="1005" height="72" alt="Screenshot 2026-05-12 075833" src="https://github.com/user-attachments/assets/a883ad7c-2740-41a9-83ae-7cd508b48d10" />

## Bước 2. Tạo và cấu hình file `docker-compose.yml`

```
nano docker-compose.yml
```

File `docker-compose.yml` sẽ được cấu hình gồm các service:
- Mariadb: Sử dụng để  làm hệ quản trị csdl cho wordpress
- Phpmyadmin: Giao diện để đăng nhập vào mariadb, chỉ cần tạo csdl còn lại wordpress sẽ làm hết
- Wordpress: Truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin

<img width="942" height="661" alt="Screenshot 2026-05-12 080642" src="https://github.com/user-attachments/assets/5f75cec3-87d2-4a17-be69-103fab100fbc" />

<img width="967" height="412" alt="Screenshot 2026-05-12 080648" src="https://github.com/user-attachments/assets/d1a197fd-cfb3-4e42-a0c0-c7204f79bc0e" />


## Bước 3. Khởi động hệ thống 
```bash
# Chạy tất cả các service để pull dịch vụ
docker-compose up -d
```
<img width="1028" height="306" alt="image" src="https://github.com/user-attachments/assets/7e124ea5-cda1-4c0a-895f-275aaa27aa6f" />
```
---

# TRUY CẬP VÀO CÁC DỊCH VỤ

## Truy cập trang wordpress
```
localhost:8000
```

# THIẾT LẬP WORDPRESS BAN ĐẦU VÀ TẠO BÀI ĐĂNG
## Thiết lập wordpress

 Nhấn **Cài đặt wordpress*** sau đó đăng nhập vào trang quản trị

<img width="833" height="805" alt="Screenshot 2026-05-12 083737" src="https://github.com/user-attachments/assets/29eea48e-ad72-4d4c-9d06-dd450a541b45" />


## TẠO HAI BÀI ĐĂNG
Quy trình tạo bài đăng
1. Sau khi đăng nhập vào trang Wordpress -> Chọn **Bài viết** -> **Thêm bài viết**
2. Tiêu đề: Ghi tiêu đề bài viết
3. Viết nội dung
4. Có thể thêm ảnh hoặc video bằng cách chọn **(+)** -> Chọn hình ảnh/video -> Tải lên
5. Nhấn **Đăng**

<img width="1914" height="974" alt="image" src="https://github.com/user-attachments/assets/95024ba4-4bae-499a-8690-d8f6b829d131" />

### Bài viết 1: Giới thiệu về bản thân


<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/20a5ee53-6480-4e6e-9b23-78f583b4fafc" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/7c9d61f4-f99e-4db1-8b0e-5f98fa69b3bc" />


### Bài viết 2: Giới thiệu ngành Kỹ thuật máy tính


<img width="1907" height="1075" alt="image" src="https://github.com/user-attachments/assets/287abb26-e0e1-4dc5-9e53-ac7ec8514cf5" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/368bf07c-f81c-4262-ab5a-7634dc085497" />

---

## 3. Nhận xét
- **Độ khó:** Dễ tiếp cận hơn Django do giao diện quản trị trực quan.
- **Tài nguyên:** Chiếm dụng RAM đáng kể (~600MB) nhưng mang lại hiệu quả quản lý nội dung vượt trội.
