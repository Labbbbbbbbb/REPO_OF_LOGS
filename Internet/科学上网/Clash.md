
## 下载

clash官网：https://www.clash.la/releases/

![1708925903673](image/Clash/1708925903673.png)

选择倒数第三个linux版（是的它的名字叫Clash for Windows Linux版)

下载之后解压

进入解压后的文件（注意要进到里面那一层，该位置ls的结果如下)

![1708926108499](image/Clash/1708926108499.png)

然后在该工作目录下运行命令  `./cfw` 即可打开clash

![1708925791325](image/Clash/1708925791325.png)

接下来配置环境变量让clash可以在全局打开：

为防止命名格式不合理，先把里面那一层文件夹改名为`Clash-for-linux`

```
sudo cp -ar Clash-for-linux /opt
sudo geidt ~/.bashrc
```

在`.bashrc`中添加

```
#Clash Env
export PATH=$PATH:/opt/Clash-for-linux
```

然后保存退出

```
source ~/.bashrc
```

以后直接输入`cfw`即可打开Clash啦




## 配置

点开右上角的设置，配置代理

![1708947944761](image/Clash/1708947944761.png)

7890是本机的clash默认端口

然后配置好url，点击General中的start with linux就好啦
