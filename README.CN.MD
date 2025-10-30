# vigie-waf 守望web防火墙

## 这是一个什么项目
这是一个由rust编写的，跨平台的，一站式web防御解决方案；
其特点是快如闪电和稳如老狗；

## 并发测试 1.2.3版本

以下是基于本机静态资源访问测试
防御架构为：

`vigie-waf` ===> `nginx` ===> `index.html`

### 200并发测试
![200并发](./assets/k6-test-200.png)

### 500并发测试
![200并发](./assets/k6-test-500.png)

## 项目架构
![架构图](./assets/core.png)

## 项目进展
- [x] 核心功能开发
- [x] 多进程架构
- [ ] 完善文档
- [ ] 全内存共享架构改造
- [ ] 其他功能迭代
- [ ] 开源代码


## 如何运行
### 直接下载
#### windows

1、下载[最新releases版本](https://github.com/pcloth/vigie-waf-rust-publish/releases)

2、在项目根目录直接运行./bin/vigie-waf-rust.exe

#### linux
1、下载[最新releases版本](https://github.com/pcloth/vigie-waf-rust-publish/releases)

2、在项目根目录直接运行./bin/vigie-waf-rust

### docker运行

由于vigie-waf是支持ota升级的，所以如果想使用ota升级，不要直接用容器内的项目运行。
推荐用宿主机映射代码目录的方式；

```sh
docker run -it -p 80:80 -p 443:443 \
  -v your_path:/app \
  pcloth/vigie-waf-rust:latest \
  -e ADMIN_USERNAME=admin \
  -e ADMIN_PASSWORD=admin123 \
  -e JWT_SECRET=298347sjfi#2212 \ 
  bash -c "export RUST_LOG=debug && /app/bin/vigie-waf-rust & while true; do echo hello world; sleep 60; done"
```
> 其中`& while true; do echo hello world; sleep 60; done`是为了让ota升级的时候容器不会停止而设立的，你如果想要手动升级，可以不需要这个
`ADMIN_USERNAME`、`ADMIN_PASSWORD`、`JWT_SECRET`三个参数一定要自己修改


## 如何配置

### 第一步

当运行好项目之后，直接在浏览器中访问http://localhost，会看到欢迎页面

![welcome](./assets/welcome.png)

### 第二步

点击进入后可以看到管理端登录页面
![login](./assets/login.png)

输入你之前在环境变量中配置的账号和密码

> 默认账号为`admin`，密码为`admin123`

### 第三步
修改你的语言：目前支持`中文`和`英文`
![changeLang](./assets/changeLang.png)

### 第四步
配置你的站点
![configSite](./assets/configSite.png)

### 完成





