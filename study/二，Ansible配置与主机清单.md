# Ansible配置与主机清单

## 配置

配置文件存在不同的位置，但只有一个可用

ansible从上往下依次检查，检查到哪个可用就用哪个

1，   ansible_config 环境变量，可以定义配置文件的位置

2，  ./ansible.cfg存在于当前工作目录

3，   ~/.ansible.cfg存在于当前用户家目录

4，    /etc/ansible/ansible.cfg 默认目录

配置文件中需要打开

#是否检查远端主机有秘钥  一般是取消注释打开状态

host_key_checking = False

打开这个需要后面增加参数可以让循环语法一次性执行  **很有用建议打开提供脚本运行效率**

#squash_actions = apk,apt,dnf,homebrew,pacman,pkgng,yum,zypper



循环写法

https://blog.csdn.net/sfdst/article/details/81236114

## 主机清单

### 主机IP地址

[webservers]   #[]方括号是组名

host:9999         #指定主机连接端口

host http_port=80 max=808 #定义主机变量

www[1:30].example.com   #定义1到30范围内的主机

www-[a:f].example.com    #定义a到f范围内的主机

### 变量

all  所有主机

ungrouped 包含没有组的主机

不会出现group_names之类的组列表中

变量合并

优先顺序，all最低，host最高

all group

parent group

child group

host

可以使用ansible_group_priority调整优先级，默认为1 数值越大优先越高

例子  可以输入密码执行远程命令

```
ansible 主机 -a '命令' -k
SSH password: #输入主机密码
ansible '主机' -a '命令' -K
SUDO password: #提取权限密码
```

例子 可以在配置文件中写入主机密码  定义了一个变量test

```
/etc/ansible/hosts
[node]
10.0.0.1 ansible_ssh_pass=123456 test=134
```

```
ansible node -m debug -a "msg{{test}}"
xxxx
msg: 134
xxxx
```

lnventory变量参数列表

主机连接：

ansible_connection   # local

所有连接：

ansible_host #远程主机名

ansible_port  #ssh端口号，

ansible_user   #默认ssh用户名

ssh连接参数

ansible_ssh_passssh 密码 不建议使用 一般使用--ask-pass或是ssh密钥

权限提升参数

ansible_become 开启提权

ansible_become_method 提权方式

ansible_become_user 提权用户

ansible_become_pass 提权密码

ansible_become_flags 提权命令参数

远程主机环境参数

ansible_shell_type 默认是sh 也可以指定其它

ansible_python_interpreter 指定对应的Python环境

动态主机清单

