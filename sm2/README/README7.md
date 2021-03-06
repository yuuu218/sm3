### 一、名称：实现SM2 2P签名及验证  
### 二、简介：  
门限密码算法通常用 (n， k）形式表示，n 表示参与者的个数， k 表示门限值（也被称为阈值），表示要完成秘密运算时最少需要的参与者个数。在攻击者能够攻破或完全控制的参与者个数少于
k 个的前提下，门限密码算法依然能够保持其安全性。  
   接下来介绍一下这种 SM2 门限密码方案的原理：它是一种（2，2）门限密码方案，即需要两个参与方，才能完成用到私钥的密码运算（如签名、解密）。  
公钥及私钥份额生成算法：当需要生成 SM2 非对称密钥时，由两个参与方各自独立生成一个私钥份额（或称为私钥片段、私钥分量），双方通过交互通信、传输一些辅助计算数据，由其中一方合并辅助数据生成 SM2 公钥。只要这两个参与方不串通，就没有办法恢复出完整的 SM2 私钥。在攻击者至多只能攻破其中一个参与方的情况下，攻击者也没有办法恢复出完整的 SM2 私钥。
门限签名算法：当需要对消息进行 SM2 签名时，两个参与方分别使用各自持有的签名私钥片段，计算生成签名片段，然后双方交互传输签名片段等辅助计算数据，由其中一方对收到的数据进
行合并计算，生成 SM2 签名。  
如下图所示：  
 ![image](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/sm2_13.png)  
### 三、完成人：于晓畅、李金源    
### 四、项目代码说明  
本项目的基础是实现SM2签名算法，在此基础上实现两部分签名，故我利用了项目二实现的随机生成k时的SM2签名及验证算法，再定义了两部分签名函数def twoP_sign()。  
为实现椭圆曲线的运算，需要一些基本的函数，如素数检测、字节和int的转换、求最大公约数、求乘法逆元等，本代码的前面部分实现了这些基础函数。其后定义了椭圆曲线密码类，
用以实现一般的ECC运算：加法、乘法、求反等。再然后定义了SM2类继承ECC，实现SM2算法的签名、验签等。最后是与本项目直接相关的两部分签名函数，利用了项目说明里的过程，代码实现之。  
### 五、运行指导：利用PyCharm在安装了所需模块的前提下直接run .py文件即可  
### 六、运行截图  
![image](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/sm2_14.png)  
### 七、具体贡献说明  
于晓畅：完成代码  
李金源：搜集资料 
