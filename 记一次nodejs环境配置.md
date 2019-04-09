## 记一次nodejs环境配置

nodejs基本环境



nodejs nodejs

npm  包管理工具

pm2  项目管理工具



1. 下载安装nodejs 可以通过wget 下载安装包 也可以下载好安装包上传到linux服务器上

2. 稍微高一点版本的nodejs都会包含npm包在node/bin/下

3. 建立软连接   ln -s /node/bin/node /usr/local/bin/node

   ​    		    ln -s /node/bin/npm /usr/local/bin/npm

   node -v

   npm -v 

   查看版本

4. 下载pm2管理工具 在联网环境下 npm install -g pm2

    pm2 -v

   查看版本

   离线环境下

   找到一台可以联网的机器下载安装pm2

   npm config get prefix 

   如果显示/usr/local/node 则在/node/lib/node_modules 下找到pm2打包放到离线服务器的/node/lib/node_modules下

   tar -cvzf pm2.tar.gz pm2  打包

   tar -xvzf pm2.tar.gz  解压

   npm build pm2 -g 重新编译

   建立软连接 ln -s /node/bin/pm2 /usr/local/bin/pm2

   pm2 -v 查看pm2版本

5. 运行项目

   进入到项目文件夹下

   执行pm2 bin/www 启动项目

   pm2 list   查看项目列表

![1544449095086](assets/1544449095086.png)

pm2 stop 1 关闭id =1 的服务

pm2 start 1 开启id=1的服务

pm2 delete 1 删除id=1的服务



PS：其他操作可执行Google



