---
title: linux下安装nginx
date: 2016-09-08 17:16:31
tags: "nginx"
---

yum install -y gcc

yum install -y gcc-c++

wget http://nginx.org/download/nginx-1.10.0.tar.gz

yum install -y pcre pcre-devel

yum install -y zlib zlib-devel

yum install -y openssl openssl-devel

tar zxvf nginx-1.10.0.tar.gz

cd nginx-1.10.0

./configure

make && make install

cd /usr/local/nginx
