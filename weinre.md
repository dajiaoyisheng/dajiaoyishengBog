### 使用 weinre 微信页面远程调试移动端
#### 安装
```
npm -g install weinre
```
#### 启动服务端
```
weinre --boundHost 0.0.0.0 --httpPort 8081
```
### 本地可跑起来的项目(172.16.x.xxx我本机IP)
```
http://172.16.x.xxx:1789/lbm/recom.html
```
#### 在待调试的页面中注入 weinre 代码
> 在页面中引入一个脚本就可以了，本例中是:
```
<script src="http://127.0.0.1:1790//target/target-script-min.js#anonymous"></script>
```
#### 浏览器远程调试
打开 ```http://127.0.0.1:1790/client/#anonymous``` 在这个页面进行调试:
#### 关闭防火墙专用网络
#### 微信页面打开
```
http://172.16.x.xxx:1789/lbm/recom.html
```

### 再次没成功的总结
### 使用 weinre 远程调试页面
#### 遇到的坑

[网上教程](https://mozillazg.com/2015/11/how-to-debug-wechat-web-page-with-weinre.html)
- 链接同一wifi
- 代码放服务器上：比如本地打开
```
http://recomlist.com:9089/recom/default/recom.html
```
- 手机打开得是：
```
http://本机ip:9089/recom/default/recom.html
```
- 防火墙？
#### 关于获取本机ip
要用cmd