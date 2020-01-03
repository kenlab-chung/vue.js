# 工程说明
node.js版本:v13.5.0
npm版本：6.13.4
cnpm版本：6.1.1
vue-cli版本：@vue/cli 4.1.2

# 工具安装方法
```
sudo apt update  //更新软件资源列表
```
## node.js 安装方法
安装：
```
sudo apt-get install -y nodejs
```
查看版本：
```
node -v
```
## npm 安装方法
```
sudo apt-get install npm //安装
sudo npm config set registry https://registry.npm.taobao.org/ //设镜像地址为淘宝npm镜像地址
```
## cnpm 安装方法（可选）
```
sudo npm install -g cnpm --registry=https://registry.npm.taobao.org
sudo cnpm -v //查看版本号
```
## n 安装方法
```
sudo npm install -g n
```
## node.js模块管理
```
sudo n stable                //安装稳定版本
sudo n latest                //安装最新版本
sudo n rm 0.10.1             //删除某个版本
sudo n use 0.10.21 some.js   //以制定的版本执行脚本
```
## vue-cli 4.0安装
```
sudo npm uninstall vue-cli -g //如果以前安装过老版本vue-cli则需要卸载之
sudo npm install @vue/cli -g //安装vue-cli 4.0
sudo vue -V  // 查看版本号
```
## 创建项目
```
vue create ucwebapp //ucwebapp为项目名称，建议不要用中文，不要用驼峰方式命名，用中划线或下划线
```