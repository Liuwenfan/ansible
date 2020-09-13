# mysql主从搭建剧本
> create by liuwenfan  
> create at 2020-09-13

## 剧本介绍
> 本ansible剧本用来搭建mysql主从节点  
> 并且使用mysql-router作为主从集群的代理节点


## 使用前提
- 1.需要搭建一个私有的或者共有的mysql5.7的yum源和mysql-router的yum源
自建或已存在的mysql源的baseurl格式必须为【http://you_repo_server/mysql】

- 2.在roles/vars/main.yaml里面设置各个参数
```
root_new_password: #填写你想设置的mysql的root密码

# mysql router information
mysql_router_ip: # 设置mysql-router设备的ip
mysql_router_write_port: # 设置mysql-router接受读写请求的端口
mysql_router_read_port: # 设置mysql-router接受读请求的端口

# mysql master information
mysql_master_ip: # 设置mysql主节点设备的ip
mysql_master_port: # 设置mysql主节点设备的port

# mysql slave information
mysql_slave_ip: # 设置mysql从节点设备的ip
mysql_slave_port: # 设置mysql从节点设备的port

# yum repo information
yum_repo_server: # 设置mysql的yum源的地址

# mysql user information
rsync_user_username: # 设置mysql主从之间同步的用户
rsync_user_password: # 设置mysql同步用户的密码
```

- 3.搭建ansible服务
找一个设备作为ansible的主控端,安装ansible服务,被控制端需要设置ansible的ssh用户免密登录
相关指令ssh-keygen,ssh-copy-id
