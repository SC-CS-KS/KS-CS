# OP

## bin
* [rabbitmqctl](bin/rabbitmqctl.md)


## install
* [Download](http://www.rabbitmq.com/releases/rabbitmq-server)
```sh
$ make
$ make DESTDIR=/home/star/deploy/rabbitmq install
``` 

* Start
```sh
$ nohup ./sbin/rabbitmq-server start &
$ lsof -i:15672
```

* Test


### RabbitMQWeb 管理插件
```sh 
$ sh rabbitmq-plugins enable rabbitmq_management
# 新增一个用户
$ rabbitmqctl  add_user  Username  Password
$ rabbitmqctl  set_user_tags star monitoring
```
```md
http://server-name:15672
```



