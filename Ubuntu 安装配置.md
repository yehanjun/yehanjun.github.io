Ubuntu 安装配置
安装 nvm

curl -x http://192.168.0.16:7890 https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

安装 oh-my-zsh

手动下载https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh
执行命令 sh install.sh 进行安装
拉取 git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
拉取 git clone https://github.com/zsh-users/zsh-history-substring-search ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-history-substring-search
拉取 git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
拉取 git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
修改 .zshrc 文件，把上述4个插件添加进去，然后执行 source ~/.zshrc 使插件生效

ssh 免密登录
确保服务器已经安装sshd服务，可在终端执行命令 sudo service sshd status
查看当前用户是否已生成密钥对 ls ~/.ssh/id_rsa.pub
执行如下命令生成新的密钥对 ssh-keygen -t rsa
公钥拷贝 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
重启ssh sudo service sshd restart
npm 使用阿里云加速

npm config set registry https://registry.npmmirror.com

pypi 镜像使用清华源
临时使用
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
注意，simple 不能少, 是 https 而不是 http
设为默认
升级 pip 到最新的版本 (>=10.0.0) 后进行配置：
python -m pip install --upgrade pip
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
如果您到 pip 默认源的网络连接较差，临时使用本镜像站来升级 pip：
python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --upgrade pip
修改hosts文件

sudo vi /etc/hosts

修改静态路由表

sudo ip route add 10.129.0.0/16 via 10.0.2.1 dev enp0s8
sudo ip route add 10.130.0.0/16 via 10.0.2.1 dev enp0s8
sudo ip route add 10.132.0.0/16 via 10.0.2.1 dev enp0s8
重启网络生效 sudo netplan apply



