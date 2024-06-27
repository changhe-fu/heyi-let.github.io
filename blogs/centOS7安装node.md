# linux centOS7 安装node

进任意目录，或推荐放在： /***/server/node

1. 下载nodejs: (如果下载不了，官网 https://nodejs.org/en/download/复制LINUX最新版本的链接过来)

```
wget https://nodejs.org/dist/v12.18.3/node-v12.18.3-linux-x64.tar.xz
```

2. 然后解压： 

```
tar -xvf node-v12.18.3-linux-x64.tar.xz
```

4. 让它全局能访问

```
ln -s /***/server/node/node-v12.18.3-linux-x64/bin/node /usr/local/bin/node
ln -s /***/server/node/node-v12.18.3-linux-x64/bin/npm /usr/local/bin/npm
```

5. 全局测试，在任意目录 

```
node -v
npm -v
```

6. nodejs/npm 版本更新

```
首先安装n模块：

npm install -g n

第二步：

升级node.js到最新稳定版

n stable

n后面也可以跟随版本号比如：

n v0.10.26
检查 node -v     npm -v
```





