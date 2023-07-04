# CertD

CertD 是一个免费全自动申请和部署SSL证书的工具。       
后缀D取自linux守护进程的命名风格，意为证书守护进程。    

## 一、特性
本项目不仅支持证书申请过程自动化，还可以自动化部署证书，让你的证书永不过期。     

* 全自动申请证书（支持阿里云、腾讯云、华为云注册的域名）
* 全自动部署证书（目前支持服务器上传部署、部署到阿里云、腾讯云等）
* 支持通配符域名
* 支持多个域名打到一个证书上
* 邮件通知
* 证书自动更新


## 二、在线体验

官方Demo地址，自助注册后体验    

https://certd.handsfree.work/

> 注意数据将不定期清理，生产使用请自行部署    
> 包含敏感信息，务必自己本地部署进行生产使用

## 三、使用教程
本案例演示，如何配置自动申请证书，并部署到阿里云CDN，然后快要到期前自动更新证书并重新部署     

![演示](./doc/images/5-view.png)

↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓      
-------> [点我查看详细使用步骤演示](./step.md)   <--------      
↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑     

## 四、本地docker部署

### 1. 安装docker、docker-compose

1.1 安装docker    
https://docs.docker.com/engine/install/

1.2 安装docker-compose     
https://docs.docker.com/compose/install/linux/

### 2. 下载docker-compose.yaml文件
```bash
mdkir -p certd
cd certd
wget https://github.com/certd/certd/blob/v2/docker/run/docker-compose.yaml

# 根据需要修改里面的配置
# 1.修改镜像版本号
# 2.配置数据保存路径
# 3.配置certd_auth_jwt_secret
vi docker-compose.yaml


```
> 镜像版本号与release版本号同步：    
https://github.com/certd/certd/releases


### 3. 运行
```bash
# 如果docker compose是插件化安装
docker compose up -d

#如果docker compose是独立安装
docker-compose up -d

```
### 4. 访问

http://your_server_ip:7001


## 五、一些说明
### 1. 免费证书申请
* 本项目ssl证书提供商为letencrypt
* 申请过程遵循acme协议
* 需要验证域名所有权，一般有两种方式（目前本项目仅支持dns-01）
  * http-01： 在网站根目录下放置一份txt文件
  * dns-01： 需要给域名添加txt解析记录，泛域名只能用这种方式
* 证书续期：
  * 实际上acme并没有续期概念。
  * 我们所说的续期，其实就是按照全套流程重新申请一份新证书。
* 免费证书过期时间90天，以后可能还会缩短，所以自动化部署必不可少

### 2. 证书续期
实际上没有证书续期的概念，只有重新生成一份新的证书，然后重新部署证书    
所以每天定时运行即可，当证书过期日前20天时，会重新申请新的证书，然后自动执行部署任务。


## 六、联系作者
如有疑问，欢迎加入群聊（请备注certd）   
* QQ群：141236433   
* 微信群：   
![](https://ai.handsfree.work/images/exchange_wxqroup.png)
