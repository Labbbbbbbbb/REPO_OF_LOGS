## Typora_Download_in_Linux

官网：https://typoraio.cn/#linux

![image-20240413105237032](/home/zyt/.config/Typora/typora-user-images/image-20240413105237032.png)

点击`binary file(x64)`，安装二进制文件压缩包，然后`cd`到其所在的目录

```
tar xzvf Typora-linux-x64.tar.gz 
cd bin
sudo cp -ar Typora-linux-x64 /opt
cd /opt/Typora-linux-x64/
#启动
./Typora
```

至此如果要启动Typora只能在`/opt/Typora-linux-x64/`目录下，为了在任意位置启动，还需要配置环境变量

```
sudp gedit ~/.bashrc
```



打开`.bashrc`配置文件添加：

```cpp
#Typora环境变量
export PATH=$PATH:/opt/Typora-linux-x64
```

source,让配置生效

```bash
source ~/.bashrc
```

然后在任何目录都可以直接输入`Typora`启动啦