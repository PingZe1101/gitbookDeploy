DevTools.md

# 本地启动服务打开页面
## http-server
1. npm install http-server -g
2. 在目标目录打开命令行 执行 "http-server -p 自定义端口号"

# npm源管理器 && node版本管理

## npm源管理器：nrm
安装:sudo npm install -g nrm  
查看是否安装成功:nrm --version
```
❯ nrm --version
    1.2.3
```
列出可选择的源:nrm ls  
前面带 * 号的表示正在使用的源
```
❯ nrm ls

    npm ---------- https://registry.npmjs.org/
    yarn --------- https://registry.yarnpkg.com/
    *tencent ------ https://mirrors.cloud.tencent.com/npm/
    cnpm --------- https://r.cnpmjs.org/
    taobao ------- https://registry.nlark.com/
    npmMirror ---- https://skimdb.npmjs.com/registry/
```
切换使用的源:nrm use npm
```
❯ nrm use cnpm
    Registry has been set to: https://r.cnpmjs.org/
```
删除一个源:nrm del \<registry>
```
❯ nrm del xdf

    delete registry xdf success
```
添加一个源:nrm add \<registry> \<url>
```
❯ nrm add xdf http://npm.koolearn.com/

    add registry xdf success
```
测试源速度:nrm test  
测试一个源的响应时间：nrm test \<registry>
```
❯ nrm test npm

    npm ------ 1612ms
```
测试所有源的速度：nrm test
```
❯ nrm test

    npm ------ 1317ms
    yarn ----- 866ms
    tencent -- 316ms
    * cnpm ----- 572ms
    taobao --- 404ms
    npmMirror - 3440ms
    xdf ------ 957ms
```
访问源的主页：nrm home \<registry>

# node版本管理工具n
安装：sudo npm install -g n
查看是否安装成功:n --version
```
❯ n --version
    v7.4.1
```
安装或使用一个node版本：sudo n node-version,  
如果本地已存在这个node-version，则切换到这个node-version;  
如果本地不存在这个node-version，则下载安装并切换
```
❯ sudo n 8.12.0
  installing : node-v8.12.0
       mkdir : /usr/local/n/versions/node/8.12.0
       fetch : https://nodejs.org/dist/v8.12.0/node-v8.12.0-darwin-x64.tar.xz
   installed : v8.12.0 (with npm 6.4.1
```
查看所有已经安装的node版本：n  
使用或安装稳定的官方发布：sudo n stable
```
❯ sudo n stable
  installing : node-v14.18.1
       mkdir : /usr/local/n/versions/node/14.18.1
       fetch : https://nodejs.org/dist/v14.18.1/node-v14.18.1-darwin-x64.tar.xz
   installed : v14.18.1 (with npm 6.14.15)
```
删除一个node版本：n rm node-version  


