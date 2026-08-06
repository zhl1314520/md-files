## charles 工具栏

![charles 工具栏介绍](D:\charles\charles 工具栏介绍.png)





## 对于 Django 项目启动 charles 却抓不到 http 请求

### 解决 (3 步)

- ### 原来的启动

> ### python manage.py runserver

改为

> ### python manage.py runserver 0.0.0.0:8000

- ### ipconfig	(powershell)

  - 使用的是：热点，即无线局域网适配器 WLAN-----> ipv4-----> 如：192.168.248.xx
  - 使用的是：插线，即以太网适配器-----> ipv4

- ### 浏览器访问

> ### http://192.168.31.xx:8000