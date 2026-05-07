# BÀI TẬP 3 

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

8. Gắn domain dinhtu.id.vn

Cách đơn giản (điểm vẫn cao)

Vào DNS (Cloudflare hoặc nhà cung cấp domain):

Type: A

Name: dinhtu.id.vn

Value: IP máy ảo

* Sử dụng Cloudflare Tunnel (Khuyên dùng - Đúng chuyên môn IT của Tú)

Cách này không cần mở port modem, cực kỳ bảo mật và chuyên nghiệp. Bạn đã từng tìm hiểu về Cloudflare Tunnel cho dự án IoT, hãy áp dụng nó vào đây:

Cài đặt cloudflared trên máy ảo:

Bash

curl -L --output cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb

sudo dpkg -i cloudflared.deb

Login vào Cloudflare:

<img width="1365" height="445" alt="image" src="https://github.com/user-attachments/assets/9e70e312-a3f1-4502-9492-1bb25e015886" />

Bash

cloudflared tunnel login

<img width="1619" height="455" alt="image" src="https://github.com/user-attachments/assets/b8185ab4-bf4d-4fc6-a12d-947722ef9162" />

(Click vào link hiện ra để chọn tên miền dinhtu.id.vn).

1. Xác thực trên trình duyệt
Tú hãy copy đường link bắt đầu bằng [https://dash.cloudflare.com/](https://dash.cloudflare.com/)... trong terminal của bạn, sau đó dán vào trình duyệt web trên máy tính thật (máy Windows/Mac bạn đang dùng để chạy Hyper-V).

Đăng nhập vào tài khoản Cloudflare của bạn.

<img width="1910" height="1029" alt="image" src="https://github.com/user-attachments/assets/5c4d357e-e803-4e05-b70c-d2383659d159" />

Chọn tên miền dinhtu.id.vn.

Nhấn nút Authorize (Ủy quyền).

<img width="1919" height="1040" alt="image" src="https://github.com/user-attachments/assets/bfb6efc4-a39b-482e-890e-dc771410c923" />

2. Chờ tải Certificate

Sau khi bạn nhấn Authorize trên trình duyệt, quay lại màn hình Terminal của máy ảo. Bạn sẽ thấy nó tự động thông báo đã tải file cert.pem về máy thành công. Lúc này lệnh login mới thực sự hoàn tất.

<img width="1916" height="1019" alt="image" src="https://github.com/user-attachments/assets/cd242a80-7cf0-40b8-9f15-6abb86d6380b" />


<img width="1310" height="306" alt="image" src="https://github.com/user-attachments/assets/01a7e06b-f668-4de7-90fe-cd8dbc80301e" />

3. Các bước tiếp theo (Làm sau khi login thành công)

Khi máy ảo đã báo nhận được chứng chỉ, hãy chạy tiếp các lệnh này để tạo tunnel:

Tạo Tunnel (Đặt tên là wp-tunnel):

Bash

cloudflared tunnel create wp-tunnel

<img width="1643" height="410" alt="image" src="https://github.com/user-attachments/assets/6a1fe5f7-fd78-473e-aa6e-209d92e0086f" />

(Lưu ý: Lệnh này sẽ trả về một mã ID của Tunnel, Tú hãy copy mã đó lại nhé).

Cấu hình file config:

Tạo file cấu hình để trỏ tên miền về port 8080 của WordPress:

Bash

nano ~/.cloudflared/config.yml

Dán nội dung này vào (thay [ID_CUA_TUNNEL] bằng mã bạn vừa copy):

Tạo Tunnel:

Bash

cloudflared tunnel create wp-tunnel

<img width="1724" height="950" alt="image" src="https://github.com/user-attachments/assets/b172236e-721a-4232-8d92-4ecaab386f82" />

Cấu hình DNS trên Cloudflare:

Bash
    cloudflared tunnel route dns wp-tunnel web.dinhtu.id.vn
    ```
<img width="1084" height="86" alt="image" src="https://github.com/user-attachments/assets/05f94d69-702e-4f1d-a66b-12ab3d31e9a3" />

5. Cấu hình WordPress nhận Domain mới

Đây là bước quan trọng nhất để giao diện web không bị lỗi. mở trình duyệt và làm theo thứ tự:

Truy cập: http://192.168.1.50:8080/wp-admin (Dùng IP nội bộ để vào cấu hình trước).

Vào Settings (Cài đặt) -> General (Tổng quan).

Sửa 2 ô sau thành địa chỉ mới của bạn:

WordPress Address (URL): http://web.dinhtu.id.vn

<img width="1909" height="1032" alt="image" src="https://github.com/user-attachments/assets/e62e25a4-acce-4582-a7f8-bae99bea34c3" />

Site Address (URL): http://web.dinhtu.id.vn

* trang đăng nhập admin

<img width="1911" height="1027" alt="image" src="https://github.com/user-attachments/assets/ca9798f7-bc96-45bb-a521-45b2e615f4c7" />

# Yêu cầu chính 

* SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ TẠO docker ccompose chứa:

Mariadb: sử dụng image: mariadb:latest để làm hệ quản trị csdl cho wordpress


Phpmyadmin: sư dụng image: phpmyadmin:latest để đăng nhập vào mariadb rồi tạo csdl trống (chỉ để xem, ko cần tạo bảng từ đây, wordpress sẽ làm hết)

<img width="1909" height="1024" alt="image" src="https://github.com/user-attachments/assets/2b5c16c5-803e-44bc-a843-bdd2fdd450e2" />

WordPress: Sử dụng image: wordpress:latest, truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin

<img width="1919" height="1073" alt="image" src="https://github.com/user-attachments/assets/3e4196b0-ef8b-4f78-ac72-cc5d4b663f49" />

* Yêu cầu: sau khi có 3 service này trong file docker-compose.yml :

Cấu hình để hệ thống chạy

Sử dụng cloudflare tunnel để public web này lên 1 sub-domain

- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...

+ Hình ảnh chứa thông tin cá nhân:

<img width="1906" height="1029" alt="image" src="https://github.com/user-attachments/assets/e186941e-a010-4f2a-b856-8f0bf86a76d6" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/3c81b7fb-d8d4-41de-b713-18be4453dc31" />

- Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ad77ae4b-aa18-4467-9816-e3e55f27a5ca" />

* Nhận xét 

1. Công sức triển khai

Tiết kiệm thời gian: Thay vì phải code từng dòng HTML/CSS/PHP, WordPress cho phép xây dựng một website hoàn chỉnh chỉ trong vài phút sau khi cài đặt xong môi trường Docker.

Quản trị dễ dàng: Việc thay đổi giao diện (Theme) hay thêm tính năng (Plugin) được thực hiện qua giao diện kéo thả, không đòi hỏi kiến thức lập trình phức tạp.

2. Độ khó/dễ khi sử dụng

Dễ dùng: Giao diện quản trị (Dashboard) trực quan, hỗ trợ tiếng Việt tốt, cộng đồng hỗ trợ cực lớn.

Khó khăn: Khó khăn nhất nằm ở bước cấu hình máy chủ (Ubuntu, Docker) và thiết lập kết nối an toàn (Cloudflare Tunnel). Khi đã xong bước này, việc sử dụng WordPress cực kỳ đơn giản.

3. Tài nguyên hệ thống (RAM/CPU/Disk)

RAM: WordPress chạy trên Docker tiêu tốn khoảng 400MB - 600MB RAM (bao gồm cả PHP engine). Nếu cài thêm nhiều plugin, con số này có thể tăng lên.

CPU: Khi không có lượt truy cập, CPU gần như ở mức 0-1%. Tuy nhiên, khi xử lý các yêu cầu phức tạp (như nén ảnh, xử lý video), CPU có thể nhảy vọt trong thời gian ngắn.

Lưu trữ: Mã nguồn WordPress khá nhẹ, nhưng cơ sở dữ liệu MariaDB sẽ phình to nhanh chóng nếu website có nhiều bài viết và bình luận. Việc sử dụng Docker giúp quản lý tài nguyên này một cách tách biệt và hiệu quả.
