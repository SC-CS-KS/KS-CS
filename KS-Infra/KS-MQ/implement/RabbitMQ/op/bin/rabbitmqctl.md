# rabbitmqctl
```md
由于账号guest具有所有的操作权限，并且又是默认账号，出于安全因素的考虑，guest用户只能通过 localhost登陆使用，
并建议修改 guest用户的密码以及新建其他账号管理使用 rabbitmq (该功能是在3.3.0版本引入的)。
```
```md
虽然可以将 ebin 目录下 rabbit.app 中 loopback_users 里的<<"guest">>删除， 
并重启 rabbitmq，可通过任意 IP 使用guest账号登陆管理控制台，但始终是违背了设计者的初衷。
```
## 用户管理
```md
(1) 新增一个用户
rabbitmqctl  add_user  Username  Password
(2) 删除一个用户
rabbitmqctl  delete_user  Username
(3) 修改用户的密码
rabbitmqctl  change_password  Username  Newpassword
(4) 查看当前用户列表
rabbitmqctl  list_users
```
## 用户角色
```md
1. 超级管理员(administrator)
    可登陆管理控制台(启用management plugin的情况下)，
    可查看所有的信息，并且可以对用户，策略(policy)进行操作。
2. 监控者(monitoring)
    可登陆管理控制台(启用management plugin的情况下)，
    同时可以查看 rabbitmq 节点的相关信息(进程数，内存使用情况，磁盘使用情况等)
3. 策略制定者(policymaker)
    可登陆管理控制台(启用management plugin的情况下), 
    同时可以对 policy 进行管理。但无法查看节点的相关信息(上图红框标识的部分)。
    与administrator的对比，administrator能看到这些内容
4. 普通管理者(management)
    仅可登陆管理控制台(启用management plugin的情况下)，无法看到节点信息，也无法对策略进行管理。
5. 其他
    无法登陆管理控制台，通常就是普通的生产者和消费者。
```
```md
rabbitmqctl  set_user_tags  User  Tag
User为用户名， Tag为角色名(对应于上面的administrator，monitoring，policymaker，management，或其他自定义名称)。

也可以给同一用户设置多个角色，例如
rabbitmqctl  set_user_tags  hncscwc  monitoring  policymaker
```
## 用户权限
```md
指的是用户对exchange，queue的操作权限，包括配置权限，读写权限。
配置权限会影响到exchange，queue的声明和删除。
读写权限影响到从queue里取消息，向 exchange 发送消息以及 queue 和 exchange 的绑定(bind)操作。
```
```md
(1) 设置用户权限
rabbitmqctl  set_permissions  -p  VHostPath  User  ConfP  WriteP  ReadP

(2) 查看(指定 hostpath )所有用户的权限信息
rabbitmqctl  list_permissions  [-p  VHostPath]

(3) 查看指定用户的权限信息
rabbitmqctl  list_user_permissions  User

(4)  清除用户的权限信息
rabbitmqctl  clear_permissions  [-p VHostPath]  User
```