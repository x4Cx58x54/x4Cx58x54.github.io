# B超影像分析总结 | B-scan Ultrasonography Analysis Review

## C#

#### MessageBox
```C#
MessageBox.Show(string text, string caption, MessageBoxButtons buttons, MessageBoxIcon icon);
```
返回`DialogResult`类型。仅有的触发方法。

#### 静态类
静态类只包含静态成员并且不可实例化。

#### try-catch
```C#
try
{
    STATEMENTS;
}
catch (Exception ex)
{
    STATEMENTS;
}
```
截获的异常赋值给 `ex`，以进一步处理。可用 `ex.ToString()` 查看异常信息。

#### 反射动态链接库

## CentOS

### 配置网络
检测网络
```
ping www.github.com 
```
更改配置
```
cd /etc/sysconfig/network-scripts/
vi ifcfg-ens0p3
```
将 `ONBOOT=no` 改成 `ONBOOT=yes`

```
service network restart
```

### 安装 wget
```
yum -y install wget
```

### 更改 yum 源
```
cd /etc/yum.repos.d
mv ./CentOS-Base.repo ./CentOS-Base.repo.bak
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
mv CentOS7-Base-163.repo CentOS-Base.repo
```

## Node.js 服务器搭建

### 启动 TCP

```js
var net = require('net');

var server = net.createServer(function (client){
        console.log('Client connected.');
        client.on('end', function(){
                console.log('Client disconnected.');
        });
        client.write('Roger, roger.');
        client.pipe(client);
});

server.listen(9527, function(){
        console.log('Server started on port 9527.');
});
```