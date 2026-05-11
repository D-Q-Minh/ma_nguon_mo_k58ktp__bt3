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
      MYSQL_USER: admin
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

volumes:
  db_data:
  wp_data:
```

