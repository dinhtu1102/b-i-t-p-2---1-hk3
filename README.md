<img width="1918" height="1073" alt="image" src="https://github.com/user-attachments/assets/deb95030-b1f7-4d8c-b317-841c0ff95254" /># bài tập 2 - đề 1 

# Họ tên : Nguyễn Đình Tú

# Mã số dinh viên : K225480106067

# ĐỀ 1 : Mariadb + Wordpress => website + play in

# BÀI LÀM 

1 Sờ đồ cấu trúc bài :

Internet → Domain (dinhtu.id.vn)
                ↓
            Nginx (optional)
                ↓
          WordPress (Docker)
                ↓
           MariaDB (Docker)

2. Chuẩn bị máy ảo Hyper-V

Trong Hyper-V:

Cài Ubuntu Server (khuyến nghị 20.04 hoặc 22.04)
RAM: 2GB+
Network: External Switch (để có IP thật)

Sau khi cài xong:

sudo apt update && sudo apt upgrade -y

* cài đặt máy ảo

<img width="913" height="684" alt="image" src="https://github.com/user-attachments/assets/08c88896-0b8b-454b-892f-f8dc7cef8afe" />

<img width="1030" height="897" alt="image" src="https://github.com/user-attachments/assets/fe19302a-0e38-421d-a11f-8b44762bed28" />

<img width="1024" height="870" alt="image" src="https://github.com/user-attachments/assets/b0289e73-9537-482d-a1ca-008b4828cf6a" />

3. Cài Docker + Docker Compose

sudo apt install docker.io -y

sudo systemctl enable docker

sudo systemctl start docker

sudo apt install docker-compose -y

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/9951115a-1788-45b5-858e-be07e4cbefe8" />

Kiểm tra:

docker --version

docker-compose --version

<img width="1919" height="227" alt="image" src="https://github.com/user-attachments/assets/8fb64562-7c4a-4aa1-9402-cf1c79101c5c" />

4. Tạo project

mkdir wordpress-mariadb

cd wordpress-mariadb

<img width="515" height="103" alt="image" src="https://github.com/user-attachments/assets/718af5e5-3e55-42c1-a053-92c2aa251e6e" />

5. Tạo file docker-compose.yml

Tạo file:

nano docker-compose.yml

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/4449e7ab-b7df-4ae0-9fb0-267c70a01d78" />

* Nội dung chuẩn bài:

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/66eb6250-ba4d-49ee-9748-d6df7bdaa044" />

6. Chạy hệ thống

docker-compose up -d

<img width="1557" height="201" alt="image" src="https://github.com/user-attachments/assets/1896750b-1362-48a6-bdac-87dd9b00102d" />

Kiểm tra:

docker ps

<img width="1919" height="438" alt="image" src="https://github.com/user-attachments/assets/a9f84fca-263a-40ad-8d12-838cf876a26e" />

7. Truy cập WordPress

Mở trình duyệt:

http://http://172.18.158.11:8080/wp-admin/install.php

<img width="1919" height="1043" alt="image" src="https://github.com/user-attachments/assets/4a159233-5793-42f3-aaaf-085284124d49" />

👉 Làm bước cài đặt:

Site name

Username

Password

Email

<img width="1918" height="1073" alt="image" src="https://github.com/user-attachments/assets/8b3ec68c-4f1c-4bee-8ebe-3a3ec9b53025" />

*truy cập đừng dẫn vào trang admin: http://172.18.158.11:8080/wp-admin/

<img width="1915" height="1033" alt="image" src="https://github.com/user-attachments/assets/257d5a99-1364-49a9-9822-4540c1dd5b69" />


