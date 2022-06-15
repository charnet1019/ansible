# ansible 2.12.6
常用角色

# 安装依赖包  
  ```
  dnf install sshpass -y
  ```

# 初始化角色  
  ```
  ansible-galaxy role init --offline <ROLE_NAME>
  ```

# 查看已安装的collection
  ```
  ansible-galaxy collection list
  ```

# 语法检查  
  ```
  ansible-playbook --syntax-check test.yml
  ```

# 用户提权字段释义  
  - become          是否进行提权操作。如果需要，设置为yes; 必需  
  - become_user     设置为具有所需特权的用户-您想要成为的用户，而不是您登录时使用的用户; 非必需; 默认为root  
  - become_method   权限工具，如sudo，su，pfexec; 非必需; 默认为sudo  
  - become_flags    play或task级别上，允许为任务或角色使用特定的标志。一种常见的用法是，当shell设置为no login时，将用户更改为nobody; 非必需  

  - remote_user     用于在远程主机上执行任务的用户

# 查看远程服务器的元数据信息  
  ```
  ansible demo -i hosts -m setup
  ```


---
# SSH相关配置  
## authorized_key模块key_options取值如下:
  - command                 # 使用此密钥进行身份验证时执行的命令  
  - environment             # 使用此密钥时要添加到环境中的变量，以 NAME=value 形式  
  - from                    # 可以使用此密钥连接远程主机(发起方IP)的逗号分隔列表  
  - no_agent_forwarding     # 使用此密钥时禁止身份验证代理转发  
  - no_port_forwarding      # 使用此密钥时禁止TCP转发  
  - no_X11_forwarding       # 使用此密钥时禁止X11转发  


# 手工生成用户密码  
## CentOS 6  
*md5格式*  
```
openssl passwd -1 -salt 'yousalt' 'secret'
```
*sha512格式*  
```
grub-crypt --sha-512
```

## CentOS 7  
*sha512格式*  
```
python -c 'import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm: ")) else exit())'
```

# 查看用户账户过期详细信息  
```
[root@localhost home]# chage -l tim
Last password change					: Jun 13, 2022
Password expires					: never
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
```




---
# 常见问题  
## Platform linux on host -.-.-.- is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could change this.  
```
/etc/ansible/ansible.cfg
[defaults]
interpreter_python = auto_legacy_silent
```
