# ansible命令

## 1,ansible

语法：

ansible -host 选项

ansible 

-e 添加变量 最高

-f  执行的时候并行主机默认是5个

-i 指定主机清单

-l 指定义主机清单后只运行那些主机

-m 指定模块名称  #在配置文件里也可以改

-p 异步轮训的时间，默认15秒

-B 异步运行多久超时

例子1		并发执行10个主机

```
ansible all -m shell -a 'hostname' -f 10
```

例子2        只执行10.0.0.1主机 -l 参数

```
ansible all -l 10.0.0.1 -m shell -a 'hostname' 
```

## 2,ansible-console

进入交互模式执行ansible

```
ansible-console
```

## 3,ansible-doc

查看模块帮助信息  

```
ansible-doc 模块名
```



## 4,ansible-galaxy

ansible共享模块

搜索关于tomcat模块

```
ansible-galaxy search tomcat
```

安装其他人的tomcat

```
ansible-galaxy install tomcatxxxxx
```

查看角色信息

```
ansible-galaxy info 角色名
```

创建一个role模板

```
ansible-galaxy init abc
```

## 5,ansible-playbook

检查语法

```
ansible-playbook test.yml --syntax-check
```

查看执行的剧本

```
ansible-playbook test.yml --list-tasks
```



## 6,ansible-pull

这个命令是用来执行**拉去远程的github或是gitlab**上的代码到**本地执行

[官网参考说明](https://docs.ansible.com/ansible/latest/cli/ansible-pull.html?highlight=pull)

语法

```
ansible-pull -U <repository> [options] [<playbook.yml>]
```

例子 -o 当远程有剧本时才运行  -C 是指定Master分支 -d 存放代码的目录 -i 指定运行的hosts文件 -U 指定url地址

```
ansible-pull -o -C master -d /tmp/test_pull -i /tmp/test_pull/hosts -U #github地址
```



## 7,ansible-config

查看ansible的配置

```
ansible-config view
```

查看变量

```
ansible-config dump
```

查看变量的描述信息

```
ansible-config list
```



## 8,ansible-inventory

ansible-inventory --vars --graph   #显示详细的图表信息



## 9,ansible-vauit

加密模块

例子  

1，给一个文件加密，输完密码以后就可以编辑

```
ansible-vauit create /tmp/123
```

xxxx password: 

xxxx password:

2，直接查看加密文件    

```
cat /tmp/123
```

ansible_vaulxx

xxxxxxxxxxxxxx

xxxxxxxxxxxxxx

xxxxxxxxxxxxxx

3，输入密码查看文件

```
ansible-vault view /tmp/123
```

password:     #输对密码

真实的内容

4，再次编辑文件

```
ansible-vault edit /tmp/123
```

password:   #输对密码

即可编辑文件

5，解密文件

```
ansible-vault docrypt /tmp/123
```

password:    #输对密码

6，对一个已经存在文件加密

```
ansible-vault encrypt /tmp/123 --ask-vault-pass
```

password:

password:

7，查看文件

```
ansible-vault view /tmp/123 --ask-vault-pass
```

例子 加密hosts文件

```
ansible-playbook test.yml --ask-vault-pass 
```

password:   #输入密码

指定密码文件

```
ansible-playbook test.yml --vault-password-file=/tmp/pass
```





############

学习到ansible patterns匹配       41分钟

https://www.bilibili.com/video/av25424954/?p=3  