# sshkey
懒人免登陆脚本

vim sshkey.sh

复制以下内容粘贴到新建的sshkey脚本中

#!/usr/bin/bash
#check root
if [ `whoami` = "root" ];then
        echo -e "\033[32m Success! \033[0m"
else
        echo -e "\033[31m Permission Denied! \033[0m"
        exit
fi
#Local key
ssh-keygen -t rsa
#create
cd /root/.ssh && cat id_rsa.pub > authorized_keys
#Public key upload to remote server
echo "Please input your Ip address:"
read Ip
echo "Your IP Address is $Ip"
echo "Please input your Port:"
read Port
echo "Your Port Address is $Port"
echo "Please input your Username:"
read Username
echo "Your Username Address is $Username"
ssh-copy-id -p $Port $Username@$Ip

chmod +x sshkey.sh

第一次手动输入ip,端口,密码 把公匙传到服务端之后就省去了频繁登录需要输入密码的情况
