运行Docker时，在根目录下运行以下命令

```shell
sudo docker-compose up
```

这个Dockerfile里面包含初始化数据库的操作，所以后端程序在数据库初始化前可能会自动重启数次。

* **提醒：**已知使用当前的Docker设置初始化会导致后端程序无法连接，导致容器无限重连错误，错误提示中提示Mysql Exception:Connection Refused字段。手动解决方式是在**初始化完**关系型数据库容器后进行以下操作，执行后退出shell：

  ```
  sudo docker exec -it mysql-databases bash # 进入容器bash
  mysql -uroot -p #root账号登录mysql
  use mysql;
  update user set host="%" where user="root";
  flush privileges;
  ```

  > 这个bug出现的原因似乎是在docker-compose.yml里配置mysql的MYSQL_ROOT_HOST失效了。排查出的可能原因是导入的备份数据库里面包含了新的数据库信息。修复中。
  >
  > 又及，这个bug可能会导致初始密码无法设置为bupt624以外的密码。是否会出现此问题，待检测。

关闭Docker时，在根目录下运行以下命令（一般来说不要用这个，出错重启时直接up命令即可）

```shell
sudo docker-compose down
```
