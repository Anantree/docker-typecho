# docker-typecho
you can use it quickly build your typecho blog

项目包含(mysql、redis、php、nginx)版本均为docker默认。
默认开启80、443、3306端口。
数据库地址：mysql
数据库root默认密码：123456
数据库登录默认密码：123456
默认账号及数据库：typecho
更改数据库请参考docker-compose.yml文件

使用方法：

1. 安装docker，拉取本项目

   ```git
   git clone https://github.com/Anantree/docker-typecho.git
   ```

2. 按照自己的需求修改docker-compose.yml文件

3. 拉取最新的typecho代码

   ```git
   cd docker-typecho
   git clone https://github.com/typecho/typecho web
   ```

   - 这一步可省略，web中有typecho的1.2.2版本。如需最新版本将web文件夹全部删除，执行上面的语句

4. 启动服务

   ```git
   docker-compose up -d
   ```

   
