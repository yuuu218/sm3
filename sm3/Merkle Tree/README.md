# 项目 ：Merkle Tree

## Hash

Hash是一个把任意长度的数据映射成固定长度数据的函数。

例如，对于数据完整性校验，最简单的方法是对整个数据做Hash运算得到固定长度的Hash值，然后把得到的Hash值公布在网上。

这样用户下载到数据之后，对数据再次进行Hash运算，比较运算结果和网上公布的Hash值进行比较，如果两个Hash值相等，说明下载的数据没有损坏。

可以这样做是因为输入数据的稍微改变就会引起Hash运算结果的面目全非，而且根据Hash值反推原始输入数据的特征是困难的。

如果从一个稳定的服务器进行下载，采用单一Hash是可取的。但如果数据源不稳定，一旦数据损坏，就需要重新下载，这种下载的效率是很低的。

## Hash List 

在点对点网络中作数据传输的时候，会同时从多个机器上下载数据，而且很多机器可以认为是不稳定或者不可信的。

为了校验数据的完整性，更好的办法是把大的文件分割成小的数据块（例如，把分割成2K为单位的数据块）。

这样的好处是，如果小块数据在传输过程中损坏了，那么只要重新下载这一快数据就行了，不用重新下载整个文件。

怎么确定小的数据块没有损坏哪？只需要为每个数据块做Hash。

BT下载的时候，在下载到真正数据之前，我们会先下载一个Hash列表。

那么问题又来了，怎么确定这个Hash列表本身是正确的呢？答案是把每个小块数据的Hash值拼到一起，然后对这个长字符串在作一次Hash运算，这样就得到Hash列表的根Hash(Top Hash or Root Hash)。

下载数据的时候，首先从可信的数据源得到正确的根Hash，就可以用它来校验Hash列表了，然后通过校验后的Hash列表校验数据块。



## Merkle Tree

Merkle Tree可以看做Hash List的泛化（Hash List可以看作一种特殊的Merkle Tree，即树高为2的多叉Merkle Tree）。

在最底层，和哈希列表一样，我们把数据分成小的数据块，有相应地哈希和它对应。

但是往上走，并不是直接去运算根哈希，而是把相邻的两个哈希合并成一个字符串，然后运算这个字符串的哈希，这样每两个哈希就结婚生子，得到了一个”子哈希“。

如果最底层的哈希总数是单数，那到最后必然出现一个单身哈希，这种情况就直接对它进行哈希运算，所以也能得到它的子哈希。

于是往上推，依然是一样的方式，可以得到数目更少的新一级哈希，最终必然形成一棵倒挂的树，到了树根的这个位置，这一代就剩下一个根哈希了，我们把它叫做 Merkle Root。

在p2p网络下载数据之前，先从可信的源获得文件的Merkle Tree树根。一旦获得了树根，就可以从其他不可信的源获取Merkle tree。通过可信的树根来检查接受到的Merkle Tree。如果Merkle Tree是损坏的或者虚假的，就从其他源获得另一个Merkle Tree，直到获得一个与可信树根匹配的Merkle Tree。

Merkle Tree和Hash List的主要区别是，可以直接下载并立即验证Merkle Tree的一个分支。因为可以将文件切分成小的数据块，这样如果有一块数据损坏，仅仅重新下载这个数据块就行了。

如果文件非常大，Merkle Tree可以一次下载一个分支，然后立即验证这个分支，如果分支验证通过，就可以下载其它数据了。而Hash List只有下载整个Hash List才能验证。

![](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/m1.png?raw=true)

## 运行指导

直接在C++编译器上运行

## 运行结果

### sha256

![](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/m4.png?raw=true)

### md5

![](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/m3.png?raw=true)

### sm3

![](https://github.com/yuuu218/Innovation-pioneering/blob/main/image/m2.png?raw=true)

## 完成人

于晓畅

## 参考文献

[Merkle Tree - 默克尔树](https://blog.csdn.net/a159393/article/details/101707564?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165899092116781647522722%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=165899092116781647522722&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-101707564-null-null.142^v35^pc_rank_34,185^v2^control&utm_term=%20merkletree&spm=1018.2226.3001.4187)
