### 一、名称：签名攻击-泄露k导致泄露d   
### 二、简介：  
#### 1、ECDSA  
s=k^(-1)(e+dr)  
kG=(x,y)  
r=x mod n  
#### 2、Schnorr  
d=(s-k)Hash(m||R)^(-1)  
R=eG=x,y  
#### 3、SM2  
d=(k-s)(s+r)^(-1)  
r=(e+x)  
kG=(x,y)  
### 三、完成人：于晓畅  
### 四、项目代码说明  
    本项目的基础是实现SM2签名算法，在此基础上将得到的签名利用已知的k得到d，故我利用了项目二实现的随机生成k时的SM2签名及验证算法，再定义了一个利用生成的签名和k得到d的函数def leaking_k()。  
    为实现椭圆曲线的运算，需要一些基本的函数，如素数检测、字节和int的转换、求最大公约数、求乘法逆元等，本代码的前面部分实现了这些基础函数。其后定义了椭圆曲线密码类，用以实现一般的ECC运算:
加法、乘法、求反等。再然后定义了SM2类继承ECC，实现SM2算法的签名、验签等。最后是与本项目直接相关的利用生成的签名和k得到d的函数，利用了项目说明里的过程，代码实现之。  
### 五、运行指导：利用PyCharm在安装了所需模块的前提下直接run .py文件即可  
### 六、运行截图  
![image](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/sm2_9.png)  
