### 一、名称：实现SM2 2P解密  
### 二、简介：  
门限解密算法：当需要对 SM2 密文进行解密时，两个参与方分别使用各自持有的解密私钥片段，计算生成明文片段，然后双方交互传输明文片段等辅助计算数据，由其中一方对收到的数据进行
合并计算，生成解密后的明文。  
如下图所示：  
 ![image](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/sm2_15.png)  
### 三、完成人：于晓畅、张琴心、王婧涵、李金源  
### 四、项目代码说明  
本项目的基础是实现SM2加密算法，在此基础上实现两部分解密，故我们先实现了SM2加密算法，再定义了两部分解密函数def twoP_decrypt()。  
为实现椭圆曲线的运算，需要一些基本的函数，如素数检测、字节和int的转换、求最大公约数、求乘法逆元等，本代码的前面部分实现了这些基础函数。其后定义了椭圆曲线密码类，用以实现一般
的ECC运算：加法、乘法、求反等。再然后定义了SM2类继承ECC，实现SM2算法的签名、验签等。最后是与本项目直接相关的两部分解密函数，利用了项目说明里的过程，代码实现之。
### 五、运行指导：利用PyCharm在安装了所需模块的前提下直接run .py文件即可  
### 六、运行截图  
 ![image](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/sm2_16.png)  

### 七、具体贡献说明  
王婧涵：实现椭圆曲线密码类（实现一般的ECC运算）  
张琴心：实现SM2类继承ECC  
于晓畅：实现两部分解密函数，整合代码  
李金源：实现素数检测、字节和int的转换、求最大公约数、求乘法逆元等基础函数  


