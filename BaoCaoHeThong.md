# Báo Cáo Hệ Thống ArcherySec
Báo Cáo Hệ Thống ArcherySec
==============

- Tổng quan về Archerysec
#### Archery là một công cụ quản lý và đánh giá lỗ hổng mã nguồn mở, giúp các nhà phát triển và người tiêu dùng thực hiện quét và quản lý các lỗ hổng. Archery sử dụng các công cụ nguồn mở phổ biến để thực hiện quét toàn diện cho ứng dụng web và mạng. Nó cũng thực hiện quét xác thực động ứng dụng web và bao gồm toàn bộ ứng dụng bằng cách sử dụng selen. Các nhà phát triển cũng có thể sử dụng công cụ để triển khai môi trường DevOps CI / CD của họ.

- Cài đặt hệ thống Archerysec
  - Thiết lập hệ thống
  - Triển khai bằng Vagrant và Ansible
  - Cài đặt Archerysec làm Docker Container

- Cài đặt và tích hợp OWASP ZAP vào Archerysec
- Demo scan trang web với OWASP ZAP

# 1. Cài đặt hệ thống Archerysec
## 1.1. Thực hiện chạy các dòng lệnh để thiết lập hệ thống
### Cài đặt
```
$ git clone https://github.com/archerysec/archerysec.git
$ cd archerysec
$ NAME=user EMAIL=admin@user.com PASSWORD=admin@123A bash setup.sh
$ bash run.sh
```
### Các biến môi trường
#### `DB_PASSWORD` <!-- omit in toc -->

Database password for the postgres db server

#### `DB_USER` <!-- omit in toc -->

Database user for the postgres db server

#### `DB_NAME` <!-- omit in toc -->

Database name for the postgres db server

#### `DJANGO_SETTINGS_MODULE` <!-- omit in toc -->

Django setting to use. currently this can be set to `archerysecurity.settings.development` or `archerysecurity.settings.production` depending on your needs

#### `DJANGO_SECRET_KEY` <!-- omit in toc -->

Always generate and set a secret key for you project. Tools like [this one](https://www.miniwebtool.com/django-secret-key-generator/) can be used for this purpose

#### `DJANGO_DEBUG` <!-- omit in toc -->

Set this variable to `1` if debug should be enabled

#### `ARCHERY_WORKER` <!-- omit in toc -->

This variable is used to tell the container it has to behave as a worker to process tasks
and not as a web server running on port 8000. Set it to `True` if you want to run on
this mode.

#### `EMAIL_HOST`

`export EMAIL_HOST='smtp.xxxxx.com'`

#### `EMAIL_USE_TLS`

`export EMAIL_USE_TLS=True`

Set this variable to `True` or `False`

#### `EMAIL_PORT`

`export EMAIL_PORT=587`

Set this variable to SMTP port.

#### `EMAIL_HOST_PASSWORD`

`export EMAIL_HOST_PASSWORD='password'`

Set this variable to SMTP Password.

#### `EMAIL_HOST_USER`

`export EMAIL_HOST_USER='xxxxxxxxxxxxx@gmail.com'`

Set this variable to SMTP Email.

### Đăng nhập hệ thống ArcherySec
- `Truy cập địa chỉ http://0.0.0.0:8000`
- `Đăng nhập vào hệ thống với Username: admin@user.com, Password: admin@123A`

## 1.2. Triển khai bằng Vagrant và Ansible
### Triển khai
#### Chạy các lệnh sau để thiết lập
```
$ git clone https://github.com/archerysec/archerysec-vagrant-ansible.git
$ cd archerysec-vagrant-ansible
$ vagrant up --provision
```

## 1.3. Cài đặt Archerysec làm Docker Container
### Cài đặt
```
$ docker pull archerysec/archerysec
$ docker run \
    -e NAME=user \
    -e EMAIL=user@user.com \
    -e PASSWORD=admin@123A  \
    -it -p 8000:8000 archerysec/archerysec:latest
```
### Sử dụng Archerysec thông qua Docker
```
$ git clone https://github.com/archerysec/archerysec.git
$ cd archerysec
$ docker-compose up -d
``` 

# 2. Cài đặt và tích hợp OWASP ZAP vào Archerysec
- Tải OWASP ZAP tại trang chủ OWASP ZAP
- Tiến hành cài đặt bằng dòng lệnh
`$ ./ZAP 2.11.1.unix.sh`
- Ở tại ứng dụng OWASP ZAP
 - Tools > Options > API > Copy API Key
 - Tools > Options > Local Proxies > Copy Address và Port
- Tại hệ thống Archerysec
 - Settings > Enable API > Paste ZAP API Key > Paste ZAP API Host > Paste ZAP API Port
- Save
 # 3. Demo scan trang web với OWASP ZAP
 - Tại hệ thống Archerysec 
  - Create New > Domain Scans
  - URL's: nhập URL muốn scan (ví dụ:https://www.facebook.com/)
  - Chọn Project
  - Enable ZAP Scanner
  - Lauch
 - Tại cửa sổ Terminal sẽ thấy được quá trình Scan
## Như vậy là đã demo thành công Scan khi tích hợp OWASP ZAP và Archerysec.
