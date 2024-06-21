# Tugas Besar Sistem Terdistribusi
# Kelompok 12:
- 1203210013 - Enrico Sulfriando Sinaga
- 1203210145 - Aditya Aulia Rohman

1. Buat 10 Linux container, 6 container menggunakan template ubuntu 20.04 dan 3 menggunakan template debian 10
```sh
# LXC UBUNTU 20.04
sudo lxc-create -n LXC_PHP7_1 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP7_2 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP7_3 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP7_4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP7_5 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP7_6 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --server images.linuxcontainers.org

# LXC DEBIAN 10 
sudo lxc-create -n LXC_PHP5_1 -t download -- --dist debian --release buster --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_PHP5_2 -t download -- --dist debian --release buster --arch amd64 --force-cache --server images.linuxcontainers.org
sudo lxc-create -n LXC_DB_SERVER -t download -- --dist debian --release buster --arch amd64 --force-cache --server images.linuxcontainers.org
```

2. Setting IP setiap LXC dan set LXC menjadi auto start
IMAGE
3. Install dan setting SSH buat menjadi itu Permitlogin yes
rssaauthentication yes
```
cd /etc/ssh
sudo nano sshd_config
```
IMAGE
4. Restart ssh service
```
sudo service sshd restart
```
5. lalu setting password
```
passwd
```
6. Install Ansible
```
sudo apt install ansible sshpass
```
7. Buat folder baru untuk mengerjakan configure ansible 
```
cd ~/ansible
sudo mkdir -p TUBES
cd TUBES
```
8. Buat file hosts yang berisi:
```
[Laravel]
lxc_php7_1 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php7_2 ansible_host=lxc_php7_3.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php7_3 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php7_4 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become_pass=123

[Wordpress]
lxc_php_1 ansible_host=lxc_php7_1.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php_3 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=123
lxc_php_4 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become_pass=123

[database]
lxc_mariadb  ansible_host=lxc_mariadb.dev ansible_ssh_user=root ansible_become_pass=123

[yii]
yii_1 ansible_host=lxc_php7_1.dev ansible_ssh_user=root ansible_become_pass=123
yii_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=123
yii_3 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=123
yii_4 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become_pass=123
yii_5 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become_pass=123

[ci]
ci_1 ansible_host=lxc_php5_1.dev ansible_ssh_user=root ansible_become_pass=123
ci_2 ansible_host=lxc_php5_2.dev ansible_ssh_user=root ansible_become_pass=123
```
9. Membuat install-mariadb.yml, yang berisi
```
- hosts: database
  vars:
    username: 'admin'
    password: '123'
    domain: 'lxc_mariadb.dev'
  roles:
    - db
    - pma
```
10. membuat install-Laravel.yml yg berisi 
```
---
- hosts: Laravel
  vars:
    username: 'admin'
    password: '123'
    domain: 'lxc_php7_2.dev'
  roles:
    - php
    - lv
```
IMAGE
11. Membuat install-yii.yml yang berisi
```
---
- hosts: yii
  vars:
    username: 'admin'
    password: '123'
    domain: 'lxc_php7_6.dev'
  roles:
    - yii
```
IMAGE
12. Membuat install-ci.yml yang berisi
```
- hosts: ci
  vars:
    git_url: 'https://github.com/aldonesia/sas-ci'
    destdir: '/var/www/html/ci'
    domain: 'lxc_php5_1.dev
  roles:
    - app
```
