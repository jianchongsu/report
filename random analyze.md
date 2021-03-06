第二章 抛掷硬币空间上的概率论
========================================================



2.1 有限概率空间
-------------------------
有限概率空间被用于随机试验的所有可能结果有限的建模中。上章中有限次抛掷硬币。如果抛掷三次，所有可能结果的集合为：

$\mathrm{\Omega= \left\{HHH,HHT,HTH,HTT,THH,THT,TTH,TTT \right\}}$     …………………… **(2.1.1)**

设每次抛掷出现正面的概率为**p**,出现背面的概率为__q=1-p__,假设投掷过程是**相互独立**的。

由此样本空间$\Omega$ 中每个元素$\omega$ (三次抛掷的结果序列)的概率都是可以出来；

### 我们称$\Omega$中的子集为__事件__

事件也经常用文字或符号来描述。
R中模拟投三次硬币：

```r
coin = c("T", "H")
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "TTT"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "HTH"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "HHT"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "HTT"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "HHH"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "TTT"
```

```r
paste(sample(coin, 1, replace = T), sample(coin, 1, replace = T), sample(coin, 
    1, replace = T), sep = "")
```

```
## [1] "THT"
```



### 定义2.1.1  有限概率空间包含样本空间$\Omega$ 和概率测度**P**：

样本空间是一个非空有限集合，概率测度**P**为一个函数，该函数将$\Omega$中每个元素对应到 [ 0, 1 ]之间的某个数，使得：

$\sum_{\omega} P(\omega)=1$ …………………… **(2.1.4)**

一个事件是$\Omega$中的一个子集，我们按如下方式定义事件**A**的概率：

$P(A)=\sum_{\omega} P(\omega)$ …………………… **(2.1.5)**

其中

$P(\Omega)=1$ …………………… **(2.1.6)**


2.2 随机变量、分布和期望
-------------------------

### 定义2.2.1：
设$（\Omega，P）$为有限概率空间，__随机变量__为定义为$\omega$上的一个实值函数


#### 下图为1.2.2
![plot of chunk graph1](figure/graph1.png) 

我们把$S_0,S_1,S_2,S_3$的自变量记为$\omega_1\omega_2\omega_3$,尽管有些随机变量并不依赖所有硬币抛掷过程。

$S_0$不是随机变量，因为不管硬币抛掷结果如何，它的值都是固定的。这样的随机变量称为**退化的随机变量**

### 分布：
随机变量的分布是对随机变量取不同值的概率的具体描述

> 随机变量不是分布，分布也不是随机变量
> 测度的变换将改变随机变量的分布，但是不会改变随机变量本身

### 定义2.2.4 期望的定义：

设X为定义在有限概率空间$(\Omega,P)$上的随机变量。X的**期望**定义为：

$EX=\sum_{\omega}X(\omega) P(\omega)$

当用风险中性测度$\tilde{P}$  计算期望时，我们采用记号：

$\tilde{E}X=\sum_{\omega}X(\omega) \tilde{P}(\omega)$



X的__方差__定义为：

$Var(X)=E(X-EX)^2$
> 期望满足线性性

#### 如果l(x)=ax+b是一个哑变量x的线性函数，则E[l(X)]=l(EX)。

### 定理2.2.5[詹森（Jensen）不等式]：
设X为定义在有限概率空间上的随机变量，$\varphi(x)$为哑变量 x 的凸函数（convex），则有：


$\varphi(EX) \le E[\varphi(X)]$

```r
x = seq(from = 0, to = 10, length = 100)
y = x^2
plot(x, y, type = "l", col = "blue", main = "凸函攼<U+3E36><U+393C><U+3E35>
abline(a = -25, b = 10, col = "red")
abline(a = -35, b = 10, col = "green")
abline(a = -18, b = 10, col = "green")
points(5, 25, pch = 19, col = "red", cex = 2)
```

![plot of chunk jensen](figure/jensen.png) 


由Jensen不等式，直接可得：
$(EX)^2 \le E[X^2]$

2.3 条件期望
-------------------------

第一章中二叉树定价模型中，由公式（1.1.8）选择风险中性概率$\tilde{p}$和$\tilde{q}$,即

$\tilde{p}=\cfrac{1+r-d}{u-d}$,  
$\tilde{q}=\cfrac{u-1-r}{u-d}$ …………………… **(2.3.1)**

容易验证上式满足：

$\cfrac{\tilde{p}u+\tilde{q}d}{1+r} =1$ …………………… **(2.3.2)**

因此，在每个时刻n对每个抛掷硬币结果的序列$\omega_1\cdot\cdot\cdot\omega_n$,我们有：

$S_n(\omega_1\cdot\cdot\cdot\omega_n)=\cfrac{1}{1+r} [\tilde{p}S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nH)+\tilde{q}S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nT)]$   …………………… **(2.3.3)**

(即股票在时刻n的价格为时刻n+1两种可能估价的加权平均贴现值，其中$\tilde{p},\tilde{q}$为平均权重)
为了简化记号，定义：

$\tilde{E_n}[S_{n+1}](\omega_1\cdot\cdot\cdot\omega_nH)=\tilde{p}S_{n+1}\omega_1\cdot\cdot\cdot\omega_nH)+\tilde{q}S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nT)$   …………………… **(2.3.4)**

这样就可以把公式（2.3.3）重写成：

$S_n=\cfrac{1}{1+r} \tilde{E_n}[S_{n+1}]$…………………… **(2.3.5)**

并称$\tilde{E_n}[S_{n+1}]$为基于时刻n信息的$S_{n+1}$的条件期望，该条件期望可以看作是基于前n次抛掷硬币的已知结果对$S_{n+1}$值的一个估计。


### 定义2.3.1
设n满足$1\le n\le N$,对于给定的（前n次抛掷硬币的结果）序列$\omega_1\cdot\cdot\cdot\omega_n$,存在$2^{N-n}$种可能的后续$\omega_{n+1}\cdot\cdot\cdot\omega_N$。用$\sharp H(\omega_{n+1}\cdot\cdot\cdot\omega_N)$表示后续$\omega_{n+1}\cdot\cdot\cdot\omega_N$中出现正面的次数，$\sharp T(\omega_{n+1}\cdot\cdot\cdot\omega_N)$为出现背面的次数，我们定义：


$\tilde{E_n}(\omega_1\cdot\cdot\cdot\omega_n)=\sum_{\omega_{n+1}\cdot\cdot\cdot\omega_N}\tilde{p}^\sharp H(\omega_{n+1}\cdot\cdot\cdot\omega_N){q}^\sharp T(\omega_{n+1}\cdot\cdot\cdot\omega_N)X(\omega_1\cdot\cdot\cdot\omega_n)$  …………………… **(2.3.6)**

并称**$\tilde{E_n}[X]$为基于时刻n信息的X的条件期望**。
或者写成：

$\tilde{E_n}(\omega_1\cdot\cdot\cdot\omega_n)=\sum_{\omega_{n+1}\cdot\cdot\cdot\omega_N}\tilde{p}^k{(1-\tilde{p})^(N-n-k)}X(\omega_1\cdot\cdot\cdot\omega_n)$  …………………… **(2.3.6.2)**


### 定义2.3.1（续）条件期望的两个极端情形分别是：
(1) $\tilde{E_0}[X]$————不依赖任何信息X的条件期望，定义为：

$\tilde{E_0}[X]=\tilde{E}[X]$…………………… **(2.3.7)**

(2) $\tilde{E_N}[X]$————基于所有N次抛掷硬币的信息X的条件期望，定义为：

$\tilde{E_N}[X]=X$…………………… **(2.3.8)**


### 定理2.3.2（条件期望的基本性质） 
设N为正整数，X和Y为依赖于钱N次抛掷硬币结果的随机变量。对于给定的$0\le n\le N$，以下性质成立。
#### （1）条件期望的线性性。
对于所有常数$c_1$和$c_2$，我们有：

$E_n[c_1X+c_2Y]=c_1E_n[X]+c_2E_n[Y]$

#### （2）提取已知量。
如果X实际上只依赖于前n次硬币抛掷，那么：

$E_n[XY]=XE_n[Y]$

#### （3）累计条件期望。
如果$0\le n\le m\le N$,那么：

$E_n[E_m[X]]=E_n[X]$

特别地，$E_n[E_m[X]]=E[X]$

#### （4）独立性。
如果X只依赖从第n+1次至第N次抛掷硬币的结果,那么：

$E_n[X]=E[X]$

#### （5）条件詹森不等式。

如果$\varphi(x)$为哑变量 x 的凸函数（convex），则有：


$\varphi(E_n[X]) \le E_n[\varphi(X)]$


2.4 鞅
-------------------------


如果我们将（2.3.5）两边除以$(1+r)^n$，得：

$\cfrac{S_n}{(1+r)^n} =\tilde{E_n}[\cfrac{S_{n+1}}{(1+r)^{n+1}}]$…………………… **(2.4.1)**

上式方程表明：在风险中性测度下，对不支付红利的股票，基于时刻n的信息对时刻n+1的股票价格贴现值的最好估计就是时刻n的股票价格贴现值。
满足这一条件的过程被称为__鞅__。

### 定义2.4.1 
考虑二叉树资产定价模型。
设$M_0,M_1,\cdot\cdot\cdot,M_N$为随机变量序列，每个$M_n$只依赖前n次抛掷硬币（$M_0$为常量）。这样的随机变量序列称为**适应随机过程**。

(1) 如果
$M_n=E_n[M_{n+1}],n=0,1,\cdot\cdot\cdot,N-1$…………………… **(2.4.2)**
则我们称这个过程为鞅
(2)如果
$M_n \le E_n[M_{n+1}],n=0,1,\cdot\cdot\cdot,N-1$
则我们称这个过程为下鞅（尽管它可能有递增趋势）。
(3)如果
$M_n \ge E_n[M_{n+1}],n=0,1,\cdot\cdot\cdot,N-1$
则我们称这个过程为上鞅（尽管它可能有递减趋势）。

我们可以得到：
$M_n=E_n[M_{m}],m=n,\cdot\cdot\cdot,N$…………………… **(2.4.3)**
上式可被称为“多步超前”形式的鞅性质。

### 定理2.4.4 
考虑一般的二叉树模型，其中0<d<1+r<u，设风险中性概率如下给出：
$\tilde{p}=\cfrac{1+r-d}{u-d}$,  
$\tilde{q}=\cfrac{u-1-r}{u-d}$
那么在风险中性测度下，贴现股票价格过程是一个鞅，即式（2.4.1）在每个时刻n对任意的抛掷硬币结果序列都成立。

> 真实概率下的平均增长率取决于投资者财富的平均增长率；
> 投资者财富在风险中性概率下的平均增站了，与投资者持有的组合过程无关，此时，股票的平均增长率等于利率
> 尽管在风险中性测度下，某些组合过程风险要更大些，但是它们的平均增长率还是一样的。

### 定理2.4.5 
考虑N时段的二叉树模型。设$\vartriangle_0,\vartriangle_1,\cdot\cdot\cdot,\vartriangle_{N-1}$为适应组合过程，$X_0$为实数，$X_0,X_1,\cdot\cdot\cdot,X_N$为由财富方程

$X_{n+1}=\vartriangle_nS_{n+1}+(1+r)(X_n-\vartriangle_nS_n),n=0,1,\cdot\cdot\cdot,N-1$
递归产生的财富过程，那么，贴现财富过程$\frac{X_n}{(1+r)^n},n=0,1,\cdot\cdot\cdot,N$为风险中性测度下的鞅，即：

$\cfrac{X_n}{(1+r)^n}=\tilde{E_n}\cfrac{X_n}{(1+r)^n},n=0,1,\cdot\cdot\cdot,N-1$…………………… **(2.4.7)**


> 贴现财富过程为风险中性测度下的鞅
#### 推论2.4.6.
在定理2.4.5的条件下，我们有：

$\tilde{E}\cfrac{X_n}{(1+r)^n}=X_0,n=0,1,\cdot\cdot\cdot,N$…………………… **(2.4.8)**

> 鞅的期望值不会随着时间改变
> 在二叉树模型中不存在套利

### 资产定价第一基本定理：
一般地，如果一个模型中存在一个风险中性测度，那么这个模型中就不存在套利。

定理2.4.5的另一个结果是下面的风险中性定价公式。设$V_N$是一个随机变量（衍生证券在时刻N的支付），它以来与前N次抛掷硬币的结果。由定理1.2.2（多时段二叉树模型中的复制）可知存在初始财富$X_0$和复制组合过程$\vartriangle_0,\vartriangle_1,\cdot\cdot\cdot,\vartriangle_{N-1}$，使得不论抛掷硬币的最终结果如何，相应的财富过程$X_0,X_1,\cdot\cdot\cdot,X_N$都满足
$X_N=V_N$。因为$\cfrac{X_n}{(1+r)^n}$是一个鞅，由“多步超前”的鞅性质表明：

$\cfrac{X_n}{(1+r)^n}=\tilde{E_n}\cfrac{X_N}{(1+r)^N}=\tilde{E_n}\cfrac{V_N}{(1+r)^N}$…………………… **(2.4.9)**

根据定义1.2.3，我们定义衍生证券在时刻n的价格$X_n=V_n$。因此，（2.4.9）又可以写成：


$\cfrac{V_n}{(1+r)^n}=\tilde{E_n}\cfrac{V_N}{(1+r)^N}$…………………… **(2.4.10)**


或者可以等价地写成：


$V_n=\tilde{E_n}[\cfrac{V_N}{(1+r)^{N-n}}]$…………………… **(2.4.11)**
我们将此总结为一个定理：

### 定理2.4.7（风险中性定价公式） 
考虑N时段二叉树资产定价模型，其中0<d<1+r<u,并且存在风险中性概率测度$\tilde{P}$。设$V_N$是一个随机变量，它依赖于抛掷硬币的结果。那么，对于0到N之间的n，衍生证券在时刻n的价格由风险中性定价公式（2.4.11）给出。进一步，在$\tilde{P}$之下，衍生证券的贴现价格是一个鞅，即：

$\cfrac{V_n}{(1+r)^n}=\tilde{E_n}\cfrac{V_{n+1}}{(1+r)^{n+1}}$…………………… **(2.4.12)**

由式（2.4.11）定义的随机变量$V_n$与定理1.2.2中定义的随机变量$V_n$是一致的。

> 衍生证券的贴现价格是一个鞅

到目前为止，我们只讨论了在某个单独日期支付的衍生证券。而许多衍生证券，如附息债券和利率互换等，会有一系列的支付。对于这样的证券，我们有以下的定价和对冲公式。

### 定理2.4.8（现金流定价）
考虑N时段二叉树资产定价模型，其中0<d<1+r<u,并且存在风险中性概率测度$\tilde{P}$。设$C_0,C_1,\cdot\cdot\cdot,C_N$为随机变量序列，其中$C_n$之依赖于$\omega_1\cdot\cdot\cdot\omega_n$。在时刻n,…,N,相应的支付分别为$C_n,\cdot\cdot\cdot,C_N$的衍生证券在时刻n的价格为：

$V_n=\tilde{E_n}[\sum_{k=n}^N\cfrac{C_k}{(1+r)^{k-n}}],n=0,1,\cdot\cdot\cdot,N$…………………… **(2.4.13)**
价格过程$V_n$，n=0,1,……,N满足：

$C_n(\omega_1\cdot\cdot\cdot\omega_n)=V_n(\omega_1\cdot\cdot\cdot\omega_n)-\frac{1}{1+r}[\tilde{p}S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nH)+\tilde{q}S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nT)]$…………………… **(2.4.14)**

定义：
$\vartriangle_n(\omega_1\cdot\cdot\cdot\omega_n)=\cfrac{V_{n+1}(\omega_1\cdot\cdot\cdot\omega_nH)-V_{n+1}(\omega_1\cdot\cdot\cdot\omega_nT)}{S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nH)-S_{n+1}(\omega_1\cdot\cdot\cdot\omega_nT}$…………………… **(2.4.15)**
其中n在0到N-1之间变化。如果我们令$X_0=V_0$，并按时间前向递归定义资产组合价值过程$X_1,X_2,1\cdot\cdot\cdot,X_N$如下：

$X_{n+1}=\vartriangle_nS_{n+1}+(1+r)(X_n-C_n-\vartriangle_nS_{n})$…………………… **(2.4.16)**

则对所有n和$\omega_1\cdot\cdot\cdot\omega_n$,我们有：

$X_n(\omega_1\cdot\cdot\cdot\omega_n)=V_n(\omega_1\cdot\cdot\cdot\omega_n)$…………………… **(2.4.17)**
其中$V_n$为支付序列$C_n,\cdot\cdot\cdot,C_N$在时刻n的所谓净现值。

2.5 马尔可夫过程
-------------------------
### 定义2.5.1  考虑二叉树资产定价模型。设$X_0,\cdot\cdot\cdot,X_N$为适应过程。如果对每个0到N-1之间的n以及每个函数f(x)，存在另一个函数g(x)(依赖于n和f)，使得：
$E_n[f(X_{n+1})]=g(X_n)$…………………… **(2.5.1)**

则称$X_0,\cdot\cdot\cdot,X_N$是一个马尔可夫（Markov）过程。

### 定理2.5.8 
设$X_0,\cdot\cdot\cdot,X_N$为二叉树模型中的风险中性概率测度$\tilde{P}$下的马尔可夫过程。设$\nu_N(x)$为一个哑变量x的函数，考虑一个在时刻N的支付为$\nu_N(X_N)$的衍生证券。那么，对于每个0到N之间的n，衍生证券的价格$V_n$为$X_n$的某个函数$\nu_n(x)$,即：
$V_n=\nu_n(X_n),n=0,1,\cdot\cdot\cdot,N$…………………… **(2.5.10)**
存在一个计算$\nu_n(x)$的递归算法，确切的公式依赖于基本的马尔可夫过程$X_0,\cdot\cdot\cdot,X_N$。对于多维马尔可夫过程，类似结果也成立

2.6 小结
-------------------------
### 样本空间
### 期望、分布、条件期望
### 鞅
### 马尔可夫过程

