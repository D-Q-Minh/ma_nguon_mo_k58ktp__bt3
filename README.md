# Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
### Họ tên: Dương Quang Minh
### MSSV: K225480106047
### Lớp: K58KTP

### Bài 3: SỬ DỤNG WORDPRESS ĐỂ TẠO WEB SITE
### 1. tạo 
file docker-compose.yml:
```
services:
  db:
    image: mariadb:latest
    container_name: mariadb_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 123456
      MYSQL_DATABASE: wordpress_db
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: 123456
    volumes:
      - db_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin_ui
    restart: always
    ports:
      - "8080:80"
    environment:
      PMA_HOST: db
    depends_on:
      - db

  wordpress:
    image: wordpress:latest
    container_name: wordpress_app
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: 123456
      WORDPRESS_DB_NAME: wordpress_db
    depends_on:
      - db
    volumes:
      - wp_data:/var/www/html

  tunnel:
    image: cloudflare/cloudflared:latest
    container_name: cloudflare_tunnel
    restart: always
    command: tunnel --no-autoupdate run
    environment:
      - TUNNEL_TOKEN=eyJhIjoiMzljZDJiMmQyNDNhZDU3MzA2ZjFjMGY0OTA5ZTZlYWIiLCJ0IjoiNmY0M2Q4NjktNzBhYy00NjY1LWI2OWYtOTlkYjUwNjI4ODkwIiwicyI6IlpXSTFNbVV4TkRjdFptTTNOeTAwTURJeExUZzFObUl0WWpaak9EUTVOVFU0T0RnMiJ9
    depends_on:
      - wordpress

volumes:
  db_data:
  wp_data:
```
###### tạo tunnel ở cloudflare
<img width="818" height="68" alt="image" src="https://github.com/user-attachments/assets/3473a54b-dfc4-489c-82b3-bae3f57cf445" />
<img width="1050" height="67" alt="image" src="https://github.com/user-attachments/assets/0aa34d08-b8e5-4440-9dd7-747380c02a87" />

###### chạy docker compose up -d
<img width="517" height="118" alt="image" src="https://github.com/user-attachments/assets/dc4b917e-d82c-4474-b09a-5e381fa407fc" />

###### 
