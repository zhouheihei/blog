## trojan的配置使用

使用trojan大体分为三个部分，一是在服务器上搭建一个支持HTTPS的网站服务（这时这个服务器就是一个普普通通的网站），二是在服务器上配置trojan服务端，三是在客户机上配置trojan客户端。网站服务有很多种，根据自己喜好选择即可，如：nginx,caddy等（本文使用caddy）
***

### 环境

  * debian 10
***

### 准备
  1.域名
  2.服务器
  3.trojan
  4.caddy
  5.SwitchOmega
***

### 解析域名 
将域名解析到服务器IP
***

### Caddy 安装 配置
下载[Caddy](https://github.com/caddyserver/caddy/releases)
  
拷贝caddy到系统目录
`sudo mv caddy /usr/bin/`
  
添加组
`groupadd --system caddy`
  
添加用户
```bash
#    useradd --system \
	--gid caddy \
	--create-home \
	--home-dir /var/lib/caddy \
	--shell /usr/sbin/nologin \
	--comment "Caddy web server" \
	caddy 
```
下载caddy.service到系统目录
```bash
# cd /etc/systemd/system/
# wget https://github.com/caddyserver/dist/blob/master/init/caddy.service 
修改ExecStart and ExecReload 路径
```

创建Caddyfile文件
```bash
# mkdir /etc/caddy
# vi /etc/caddy/Caddyfile
```

添加以下内容到Caddyfile
```
domain.com //你的域名
respond "Hello, privacy!"
```

在/etc/caddy/下执行
```bash
# caddy run
之后会在/root/.local/share/caddy/certificates/acme-v02.api.letsencrypt.org-directory/domain.com下生成.crt 和.key文件，后面用。
```

注册服务,启动caddy服务
```bash
  	sudo systemctl daemon-reload
  	sudo systemctl enable caddy
```
