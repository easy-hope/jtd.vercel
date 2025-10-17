---
title: gitlab私有化部署
layout: default
---

# gitlab私有化部署
## 宝塔面板docker部署
宝塔面板万能安装脚本
```bash
if [ -f /usr/bin/curl ];then curl -sSO https://download.bt.cn/install/install_panel.sh;else wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh;fi;bash install_panel.sh ed8484bec
```
登录宝塔面板→docker→gitlab-ce
## 把 omnibus gitlab 私有化部署到 Ubuntu 20.04 LTS
先手动将“软件和更新”的源改为阿里云
```纯文本
wget https://omnibus.gitlab.cn/ubuntu/focal/gitlab-jh_14.9.0-jh.0_amd64.deb &
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
sudo apt-get install -y postfix
# 在安装 Postfix 的过程中可能会出现一个配置界面，在该界面中选择“Internet Site”并按下回车。把“mail name”设置为 apsonic-moto.cn
export EXTERNAL_URL=https://gitlab.apsonic-auto.com
sudo dpkg -i gitlab-jh_14.9.0-jh.0_amd64.deb
sudo vi /etc/gitlab/gitlab.rb
# external_url 'http://gitlab.apsonic-auto.com:4888' # 如果运营商禁止使用默认的80端口，需在此用冒号自定义端口才能顺利使用lfs
# gitlab_rails['initial_root_password'] = 'password'
# gitlab_rails['manage_backup_path'] = true
# gitlab_rails['backup_path'] = "/mnt/挂载点"
# gitlab_rails['backup_keep_time'] = 604800
sudo gitlab-ctl reconfigure
```
最后手动登录root账户并修改密码，偏好设置->本地化->语言->中文
### 备份
```bash
 while true
 do
   sudo cp '/etc/gitlab/gitlab.rb' /mnt/挂载点
   sleep 250000
   sudo gitlab-rake gitlab:backup:create
 done &
```
### 恢复
```bash
sudo su
#停止相关数据连接服务
gitlab-ctl stop unicorn
gitlab-ctl stop sidekiq
# 修改权限，如果是从本服务器恢复可以不修改
chmod 777 /var/opt/gitlab/backups/1530156812_2018_06_28_10.8.4_jh_gitlab_backup.tar
# 从1530156812_2018_06_28_10.8.4_jh编号备份中恢复
gitlab-rake gitlab:backup:restore BACKUP=1530156812_2018_06_28_10.8.4_jh    
# 按照提示输入两次yes并回车

gitlab-ctl start                #启动gitlab
```
浏览器访问新服务器的地址进行查看，迁移成功

在实际情况中访问gitlab可能是用域名访问，我们可以修改gitlab配置文件中的url再进行备份，这样就不会影响迁移过程，恢复完成后需要进行的只是修改域名对应的dns解析ip地址

由于备份的时候不会处理gitlab.rb和gitlab-secrets.json，所以目标服务器依然需要改一下gitlab.rb，最少`external_url`需要改一下

