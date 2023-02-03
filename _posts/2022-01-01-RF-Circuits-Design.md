---
layout:     post
title:      RF Circuit Design
subtitle:   Basic Theory
date:       2022-01-01
author:     Bohao
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - RF Circuit Design
    - Blog

---



# 射频电路设计(RF Circuit Design)

### I. 传输线理论(Transmission Line Analysis)

**啥是传输线？**  

> 传输线是电子工程中的专用电缆或者其他结构，用于传输无线电频率的交变电流 ( 就电线么 )

**给几个例子：**  

+ <font color = grey>**双线传输线  Two-Wire Lines**(就两根线)：</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232833.png" alt="image-20211217203041101" style="zoom:67%;" />

+ <font color = grey>**同轴传输线  Coaxial Line：**</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232837.png" alt="image-20211217203143383" style="zoom:67%;" />

+ <font color = grey>**微带传输线  Microstrip Lines**(PCB板上的导带可以看作是微带线，也有专门做出来当作元件的)：</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232904.png" alt="image-20211217203322800" style="zoom:67%;" />



<div style="page-break-after:always"></div>

​		<u>三明治结构</u> Sandwich structure：

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232901.png" alt="image-20211217203540000" style="zoom:67%;" />

​		<u>平行板结构</u> Geometric representation：

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232910.png" alt="image-20211217203612505" style="zoom:75%;" />





#### 0️⃣ 传输线理论的实质 <font size = 3> <font color = grey>(这玩意干嘛的？) </font></font>

<font color = grey>**传输线理论的目的：针对于高频电路，当电路<u>特征尺寸</u>可用于电磁波波长相比拟时(1/10)，电压和电流将随<u>空间位置</u>不同而变化，传统的电路理论不适用，需要有一个全新的理论来辅助电路设计。**  </font>  

> **特征尺寸**：通常指集成电路中半导体器件的<u>最小尺寸</u>( Eg. MOS的沟道长度 )  

+ <font color = grey>**由于电压和电流在电路中不同空间位置的大小不同，针对于正弦波，考虑以一个函数来衡量其在电路中的大小，该函数应当将<u>空间</u>和<u>时间</u>结合在一起。因此，针对于电压波(电压波沿着==z轴==正方向传播)：**</font>  ()

$$
V(z,t)=V_0sin(\omega t-\beta z)
$$

+ <font color = grey>**针对于该式，沿z轴的波长$\lambda$描述其==空间特征==，用沿着时间轴的周期 $T=1/f $描述==时间特性==，即相对于时间的空间变化 ---> 运动速度，射频电路中用==相速度$v_p$==来描述：**</font>

$$
v_p=\omega/\beta=\lambda f=\frac{1}{\sqrt{\epsilon \mu}}= \frac{c}{\sqrt{\epsilon_r \mu_r}}
$$

> **相速度**，是指波的相速度或相位速度，或简称相速，相速度的定义是电磁波的恒定相位点的推进速度。

> 理论上用示波器测出来应该这种样子(两个波形有**相位差**，所以上面那个叫**相速度**，帮助理解下)  
> <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232917.png" alt="image-20211217204159190" style="zoom:67%;" />



#### 1️⃣ 等效电路模型 <font size = 3> <font color = grey>(使定量分析传输线成为可能)</font></font>

**<font color = grey>电压电流随空间位置变化的特性使得`基尔霍夫电压电流定律`对于较长导线不再适用，这对于电路设计时<u>计算的精确度</u>来说是一场灾难。</font>  **

**<font color = grey>幸运的是，将较长的导线分割为==微小线段==，并引入==分布参数==(the distributed parameter)的可以在一定程度上能有效应对这一挑战(类似于微分)，因为在被分割后的单一线段上，基尔霍夫老爷子的定律<u>仍然行得通</u>。</font>  
<font color = grey>而对于微小线段的分析，利用分布参数可以建立数学模型(以双线传输线为例，其他同理): </font>**

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232922.png" alt="image-20211217201801505" style="zoom:75%;" />

> **R**、**L**：寄生的电阻、电感  
> **C**：导线间电荷分离导致的电容效应  
> **G**：介质损耗(非理想绝缘体)  
>
> > R L C G 均表示的是==单位长度==的值





<font color = grey>**等效电路的==一般形式==(为了方便分析)：**</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232926.png" alt="image-20211217202259770" style="zoom:90%;" />

**事实上，等效电路中的参数是可以通过麦克斯韦定律计算而出的，针对不同的传输线，其对应参数的表达式不同，且可以通过查表得到，例如下表：**

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232931.png" alt="image-20211219195728010" style="zoom:80%;" />

> 表达式中 $\delta$ 为趋肤深度





#### 2️⃣ 传输线方程 <font size = 3> <font color = grey>(理论分析的基础)</font></font>

**传输线方程是什么？** <font color = grey>**是一个微分方程组[用来描述电路中的电路电压关系]，解出来以后可以得到传输线中某一点的具体<u>电流电压</u>值**(事实上并不完全精确)</font>  

**怎么来的？** <font color = grey>(两条路线：**1.** 利用等效电路模型以及基尔霍夫电流电压定律，推导而出；**2.** 麦克斯韦方程组)</font>  
 <font color = grey>**具体推导不再赘述，通过==等效电路模型==推导的方式似乎更加容易理解；**</font>  

<font color = grey>**<u>大概思路</u>就是，因为等效电路模型已经是将传输线进行==分割==后得到的模型( 因为长度非常短，就可以利用基尔霍夫电流电压定律得到这一微小单元里面的电流电压关系 )，很容易联想到这其实和==微分==殊途同归；**</font>

<font color = grey>**因此将这一微小单元的电流电压关系利用微分进行替代，就能得到该种传输线的传输线方程，对其进行求解就能得到传输线上具体节点的电路电压，下面列出双线传输线的传输线方程，以作参考比较：**</font>

**针对等效电路模型，利用基尔霍夫电压定律得到：**

$$
(R+j\omega L)I(z)\Delta z+V(z+ \Delta z)=V(z) \\
\Rightarrow lim_{ { \Delta z } \to 0} \bigg(- \frac{V(z+ \Delta z)-V(z)}{ \Delta z} \bigg)=- \frac{dV(z)}{dz}=(R+j \omega L) I(z)
$$


**电流同理，因此得到双线传输线的==传输线方程==为：**
$$
-\frac{dV(z)}{dz}=(R+j\omega L)I(z)\ ,\\
\frac{dI(z)}{dz}=-(G+j\omega C)V(z)
$$

---------

<font color = maroon>**求解过程(简单几句提一下)：**</font>  
**将传输线方程简单处理(**求导)**并互相带入：**
$$
\frac{d^2V(z)}{dz^2}-\gamma ^2V(z)=0\ ,\\
\frac{d^2I(z)}{dz^2}-\gamma ^2I(z)=0\ ,\\
\gamma = \alpha+j\beta=\sqrt{(R+j\omega L)(G+j\omega C)}
$$

> 式中，**$\gamma$**为==复传播常数==，$\alpha$代表**衰减系数**，$\beta$代表**相位常数**



**通解为**(第一项均代表向+z方向传播的波，第二项为-z方向)**：**
$$
V(z)=V^+ e^{-\gamma z}+V^- e^{+\gamma z}\ ， \\
I(z)=I^+ e^{-\gamma z}+I^- e^{+\gamma z}
$$

> 由上式及复传播系数可以得到，波沿着==+z==方向传播的波的**幅度**将<u>逐渐减小</u>，vice versa.



**将(6)式回代入(4)式中得到：**(反正就是疯狂回代)
$$
I(z)=\frac{\gamma}{R+j\omega L}(V^+ e^{-\gamma z} - V^- e^{+\gamma z})
$$
 <font color = grey>**看到这个式子似乎豁然开朗了，电流和电压通过东西一联系起来了，电压？电导？**</font>  
 <font color = grey>**至此，引入一个非常重要的概念：**</font>**==特性阻抗== (Characteristic Impedance)**  

> **特性阻抗**<u>并非常规电路意义上的阻抗</u>，它的定义基于**正向和反向行进的电压波和电流波**

$$
Z_0= \frac{R+j\omega L}{\gamma}=\sqrt{\frac{R+j\omega L}{G+j\omega C}}=\frac{V^+}{I^+}=-\frac{V^-}{I^-}
$$

进一步，电流波和电压波可以表示为：
$$
V(z)=V^+ e^{-\gamma z}+V^- e^{+\gamma z}\ ， \\
I(z)=\frac{1}{Z_0}(V^+ e^{-\gamma z} - V^- e^{+\gamma z})
$$


-------

 <font color = grey>**通过上面的推导，我们除了解出电压波和电流波的表达式外，还得到了一个非常重要的物理量**</font>——**特征阻抗**  <font color = grey>**，这几个东西几乎会出现在以后所有的射频电路分析中，望谨记。**</font>



#### 3️⃣ 终端加载的无损耗传输线模型 <font size = 3> <font color = grey>(最基础的模型)</font></font>

**1. 这是啥东西？** <font color = grey>射频电路都可以看做为**有限长线段**与各种**分立的有源无源器件**的组合；其中最<u>简单</u>的就是==只连接了负载的传输线线段==，而这个传输线又是**无损耗**的，这个最简单的模型就是该部分要讨论的模型，如下：</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232938.png" alt="image-20211219194750675" style="zoom:65%;" />

**什么是==无损耗传输线==？类似于真空中的球形鸡？** <font color = grey>**通常，(8)式所定义的特性阻抗，是考虑了==损耗==的 (实部)；然而事实上，对于==较短的线段==(也是射频和微波电路中最常见的情况)，忽略损耗所带来的误差是完全可以接受的，因此这样的假设完全是具有实际意义的；**</font>  
 <font color = grey>**也就是说$R=G=0$ ，所以<u>(8)式</u>可以进一步简化为：**</font>
$$
Z_0 = \sqrt{L/C}
$$
 <font color = grey>而**复传播常数**变为：</font>
$$
\gamma = j\beta = j\omega \sqrt{LC}
$$

<font color = grey>**将前文所提到表格中对于等效电路参数的计算公式带入，可以得到不同传输线的特性阻抗，若经过计算，会发现，表中所列传输线的特性阻抗都有$ \sqrt{\frac{\mu}{\epsilon}}$ 这一项，以平行板传输线为例：**</font>
$$
Z_0= \sqrt{\frac{\mu}{\epsilon}} \frac{d}{w}
$$

> 式中$ \sqrt{\frac{\mu}{\epsilon}}$ 为**波阻抗**，在自由空间中，该值约为377$\Omega$ ，代表着天线向着**自由空间**发射电磁能量时的阻抗；  
> 与在自由空间中传播不同，波在传输线中传输时要受到约束，由平行板传输线结构中的$w$与$d$来表达。



**2. 衍生概念**  

- **电压反射系数 (Reflection coefficient)**

  <font color = grey>**针对于终端加载的无损耗传输线模型，通过观察(6)式，可知：在==z < 0== (就是负载左边，看上面那张图) 的区间，终端负载阻抗产生了==反射==。为了衡量反射的程度，引入一个指标：==<u>电压反射系数</u>$\Gamma_0$==，代表**</font><font color = firebrick>**在负载端(z = 0)处反射电压波与入射电压波的比值**</font><font color = grey>**，利用终端条件$Z(0) = Z_L$，可以得到负载端反射系数具有可行性的计算方法：**</font>
  $$
  \Gamma_0 = \frac{V^-}{V^+} = \frac{Z_L - Z_0}{Z_L + Z_0}
  $$
  <font color = grey>**由此式很容易推得，表示在不同负载条件下，电压反射系数的大小，或者说有多少电压被反射了，比如：**</font>  
  
  > 开路传输线($Z_L \rightarrow \infty$)：$\Gamma_0 = 1$，意味着反射电压波与入射电压波**同相位**；  
  > 短路传输线($Z_L = 0$)：$\Gamma_0 = -1$，意味着反射电压波与入射电压波**反相位**；  
  > 阻抗匹配时($Z_0 = Z_L$)：$\Gamma_0 = 0$，没有反射，被负载全部吸收，相当于接了一条无限长且特性阻抗相同的传输线。
  >
  > 这里需要明确的一个关于电路基础的且很多人对此模糊的概念是：<u>开路</u>相当于负载无限小，<u>短路</u>相当于负载无限大，阻抗匹配就是相当于在这二者取了一个中间的合适的值
  
  <font color = grey>**根据反射系数的定义，<u>电压波</u>和<u>电流波</u>用==负载处的反射系数==可以表示为：**</font>	
  $$
  V(z)=V^+ (e^{-\gamma z} + \Gamma_0 e^{+\gamma z})\ ， \\
  I(z)=\frac{V^+}{Z_0}( e^{-\gamma z} - \Gamma_0 e^{+\gamma z})
  $$
  
  > <font color = firebrick>**Warining：**</font>上面所定义的==反射系数$\Gamma_0$==事实上只是**负载处的反射系数** (负载反射系数)，而**真正的反射系数**是传输线上任意一点反射电压波与入射电压波幅值的比值，而这个系数似乎**并不等于**负载处的反射系数$\Gamma_0$ ，而是随着**测量点**的不同而变化 (越靠近负载，$\Gamma_0$越大)。(很多书会在这里把这两个概念混淆，很头大 ......)
  
  
  
  <font color = grey>**我们不妨探讨一下这个“ 真正的反射系数 ”是怎样的。(事实上，下面要讨论的就是<u>反射系数</u>，$\Gamma_0$只是==特殊情况==罢了)** </font> 
  <font color = grey>**为了方便，我们用<u>距离负载</u>的距离 $d$ 来描述反射系数，并建立==新的坐标系== (注意<u>正方向</u>)，讨论的模型如下(当然因为是借的图，这是一个分析负载短路的图，能说明问题就行)：**</font>
  
  <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232943.png" alt="image-20211223171526510" style="zoom:80%;" />
  
  <font color = grey>**所以==电压波==和==电流波==的表达式变成：**</font>
  $$
  V(d) = V^+ e^{+j\beta d} (1+\Gamma_0 e^{-j2\beta d}) = A(d)[1+ \Gamma(d)] \ , \\
  I(d) = \frac{V^+}{Z_0} e^{-j2\beta d}(1- \Gamma_0 e^{-j2\beta d}) = \frac{A(d)}{Z_0}[1- \Gamma(d)]\ ,\\
  \Gamma(d) = \Gamma_0 e^{-j2\beta d}
  $$
  <font color = grey>**上式中的$\Gamma(d)$即为反射系数，定义如上，可以看出他和测量点距离负载的距离 $d$ 有着指数关系。**</font>
  
  
  
  
  
  <font color = grey>**笔记写到这，还是不太清楚==反射到底是什么东西==？看看QA Stack上大佬怎么说的吧(自己翻译的)**</font>
  
  > 一条传输线同时包含**分布电容**和**分布电感**，二者的存在形成了传输线的特性阻抗$Z_0$。假设我们有一个**阶跃电压信号源**$V_S$，且其内阻$Z_S$与特性阻抗$Z_0$相匹配。在<u>t=0</u>之前，传输线上所有分布器件电压电流均为0。
  >
  > 在阶跃发生的那一刻，来自信号源的电压在 $Z_S$ 和 $Z_0$ 上**均分**，因此线路末端的电压为 $V_S/2$。所发生的第一件事是，第一个分立单元的电容需要被充电到$V_S/2$，而这需要电流流过该单元的电感。 但这会立即导致下一单元的电容通过下一单元的电感充电，依此类推。 电压波沿线路向下**传播**，伴随着电流在其后面流动，而不在前。(**个人理解：把传播理解成电压在无穷多个前文所述的等效电路中依次传播就非常说的通了**)
  >
  > 但是，假设线路的远端(负载端)是==开路==的。当电压波到达那里时，在它后面流动的电流就无处可去，因此电荷**“堆积”**在最后一单元的电容，直到电压达到可以**遏止该单元的电感的电流**的大小。能够执行此操作所需的电压恰好是到达该单元电压的**两倍**，这会在最后一单元的电感产生**反向电压**，该电压与最初在该单元中启动电流的电压一致。但是，我们现在在线路的末端有 $V_S$，而大部分线路仅充电到 $V_S/2$。这会导致电压波以**相反**的方向传播，并且随着它的传播，仍在电压波的*前面*流动的**正向传播电流**在电压波后面减少到零，使波后面的线路充电到 $V_S$。（另一种思考方式是反射产生了一个<u>反向电流</u>，正好**抵消**了原来的正向电流。）当这个反射的电压波到达**源头**时，$Z_S$ 两端的**电压**突然下降到**零**，因此**电流**也下降到**零**。同样，现在一切都处于<u>稳定状态</u>。**(个人理解：这块相当于把负载端的<u>开路状态</u>传递到了信号源)**
  >
  > 现在，如果当入射波到达传输线的负载端是那里==短路==（而不是开路），我们有一个不同的**限制条件**：电压实际上不能上升，电流只是流入短路。 但是现在我们遇到了另一种**不稳定**的情况：线路靠近负载那一端是 **0V**，但线路的其余部分仍充电到$ V_S/2$。因此，**附加电流**流入短路电路，该电流等于 $V_S/2$ 除以 $Z_0$（恰好等于流入传输线的**原始电流**）。一个电压波（从 $V_S/2$ 下降到 0V）反向传播，这个波后面的电流是它前面的原始电流的**两倍**。 （同样，可以将其视为抵消原始正波的负电压波。）当电压波到达源时，传输线靠近信号源的那一端的电压被拉到 0V，整个源电压加到$ Z_S$ 上，通过 $ Z_S$ 的电流等于 现在在线路中流动的电流。**一切再次稳定** **(个人理解：这块相当于把终端的短路状态传递到了信号源)**
  
  
  
  
  
- **传播常数和相速度**

  <font color = grey>**对于无损耗传输线，其==相位常数==$\beta =\omega \sqrt{LC}$，因为没有衰减，==传播常数==$\gamma = j \omega \sqrt{LC}$ ，而==相速度==$v_p = \frac{1}{\sqrt{LC}}$ ， 由此可以得出相位常数与相速度的关系：**</font>
  $$
  \beta = \frac{\omega}{v_p}
  $$

  > **BTW：**等效电路参数中的**L**和**C**事实上与频率无关(参见前文所述表格)，也就是说**相速度$v_p$与频率无关**，这一结论意味着不同频率的信号在传输线中会以相同的速度传播，即**波形的形状**不会发生变化，这一现象称为**==无色散==(dispersion-free)传输**。(当然是理想情况下)

  

- **驻波 (Standing wave)**

  **1. 什么是驻波？** <font color = grey>**駐波為兩個==波長==、==頻率==和==波速==皆相同的正弦波相向行進<u>干涉</u>而成的合成波。與行波不同，駐波的波形無法前進，因此==無法傳播能量==。**</font>
  
  <font color = grey>**如前所述，信号在传输线中传输可能会产生反射，而正向传输的波和反射波频率相同、波速相同，因此理论上他们干涉后也可能产生驻波；事实上的确如此，当传输线的负载端==短路==或者==开路==时，传输线中会<u>形成驻波</u>。这两种情况下==反射系数==为1或-1，相当于没有向负载传输能量，入射波被全部反射了回来，也正验证了上面那段定义所说的驻波无法传输能量这一点。**</font>
  
  <font color = grey>**那么当正向波和反射波的==振幅==不一样呢，这也是传输线中最常见的情况，根据叠加定理，事实上这时两个信号叠加后的信号已经<u>不是驻波</u>了，而是一个在<u>移动的==“ 驻波 ”==</u> (它的波结并不固定)，这个“ 驻波 ”的振幅、波速等参数都和入射波和反射波的振幅大小有关，甚至更进一步，和电压反射系数有关。**</font>
  
  <font color = grey>**也就是说我们不妨用这个==“ 驻波 “ 的波峰和波谷的相对大小==来衡量一下有多大程度的入射波被反射了回来，或者说传输线和负载的匹配程度，由此，引入一个新的物理量——<u>驻波比</u>。**</font>
  
  <div style="page-break-after:always"></div>
  
  **2. 驻波比 (Standing wave ratio, SWR)**
  
  <font color = grey>**当传输线与负载不匹配时，会产生反射波，入射波与反射波经过叠加后，会产生一种类似于“ 驻波 ”的合成波 (当然短路和开路时形成的是驻波) ，这个驻波的振幅等参数与反射波与入射波的振幅大小有关，为了==量化不匹配的程度==，不妨用传输线上电压最大幅度(或电流)与电压最大幅度(或电流)的比值来衡量，即==驻波比==，利用数学运算也可以知道其与<u>负载处的反射系数</u>$|\Gamma_0|$的关系：**</font>
  $$
  SWR = \frac{|V_{max}|}{|V_{min}|} = \frac{|I_{max}|}{|I_{min}|} = \frac{1 + |\Gamma_0|}{1 - |\Gamma_0|}
  $$
  <font color = grey> **$SWR$随着电路不匹配程度 (反射系数) 的加深而增大，最小值为1，最大值趋向于$ { +\infty} $ .**</font>
  
  <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232949.png" alt="image-20211223164758731" style="zoom:60%;" />



**3. 典型的终端条件：**不同负载条件下传输线的输入阻抗

+ **终端加载的无损传输线的输入阻抗**

  <font color = grey>**我们已经得到了电压波和电流波的表达式，也就是说可以得到任意一点看向负载端的传输线的==输入阻抗==，例如在距离<u>负载</u>$d$处，==输入阻抗==为 (省略了中间的推导步骤)：**</font>
  $$
  Z_{in} (d) = \frac{V(d)}{I(d)} = Z_0 \frac{1+\Gamma(d)}{1-\Gamma(d)} = Z_0 \frac{Z_L + jZ_0 tan(\beta d)}{Z_0 + jZ_L tan(\beta d)}
  $$
  <font color = grey>**其中的$\beta = (2\pi f)/v_p = 2\pi / \lambda $，是前面提到的相位常数，容易得知，这是一个与==频率==相关的量。**</font>

  

+ **三种典型的终端条件**

  + **终端短路传输线**

    <font color = grey>**前置条件：**</font>$Z_L = 0 \ ,\  \Gamma_0=-1$  
    <font color = grey>**输入阻抗：**</font>
    $$
    Z_{in} (d) = jZ_0 tan(\beta d)
    $$
    <div style="page-break-after:always"></div>
  
    <font color = grey>**电压波：**</font>
    $$
    V(d) = V^+ [e^{+j\beta d} - e^{-j\beta d}] = 2jV^+sin(\beta d)
    $$
    <font color = grey>**电流波：**</font>
    $$
    I(d) = \frac{V^+}{Z_0}cos(\beta d)
    $$
    

    

    <font color = grey>**为了可视化，将以上参数按照两个不同的维度画出来：**</font>
  
    <font color = grey>**频率一定时，距离$d$变化：**</font>
  
    <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203232956.png" alt="image-20211223235531052" style="zoom:70%;" />
  
    > 从图中可以看出，随着测量点倒负载的**距离**增加，输入阻抗表现出==周期性==。  
    > 个别点甚至阻抗为0，或者为 $\infty$ ；既有呈<u>感性</u>的点也有呈<u>容性</u>的点。

    <div style="page-break-after:always"></div>

    <font color = grey>**距离固定，频率$f$发射变化：**  </font>
  
    <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203233004.png" alt="image-20211223235555528" style="zoom:70%;" />
  
    > 随着**频率**改变，输入阻抗呈现==周期性==；周期性的开路、短路。
  
    
  
    
  
    
  
  + **终端开路传输线**
  
    <font color = grey>**前置条件：**</font>$Z_L = \infty \ ,\  \Gamma_0= +1 $  
    <font color = grey>**输入阻抗：**</font>
    $$
    Z_{in} (d) = - jZ_0 \frac{1}{tan(\beta d)}
    $$
    <font color = grey>**电压波：**</font>
    $$
    V(d) = V^+ [e^{+j\beta d} + e^{-j\beta d}] = 2V^+cos(\beta d)
    $$
    <font color = grey>**电流波：**</font>
    $$
    I(d) =  \frac{2j V^+}{Z_0}sin(\beta d)
    $$
    <div style="page-break-after:always"></div>
  
    <font color = grey>**频率一定时，距离$d$变化：**</font>
  
    <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203233011.png" alt="image-20211224162617897" style="zoom:60%;" />
  
    <font color = grey>**距离固定，频率$f$发射变化：**  </font>
  
    <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203233014.png" alt="image-20211224162752165" style="zoom:67%;" />
  
    
  
    
  
  + **终端阻抗匹配 **
  
    <font color = grey>**此时，$Z_L = Z_0 \ ,\  \Gamma(d)= 0 $，因此，根据输入阻抗的计算公式(18)，$Z_{in}(d) = Z_0$，输入阻抗与传输线长度无关。**</font>
  
  
  
  
  <div style="page-break-after:always"></div>
  
  + **1/4波长阻抗变换器（窄带匹配电路）**
  
    <font color = grey>**回看输入阻抗的计算公式(18)，分子分母那一坨三角函数很难受，能不能想办法把他们干掉呢？Sure！下面来看几个特殊情况。**</font> 
  
      
  
    + **长度为1/2波长 $d=m(\lambda/2), \ m=1,2,3,...$**
  
      <font color = grey>**将前置条件带入式(18)，发现==输入阻抗$Z_{in}(d=\lambda/2) = Z_L $==，也就是说，此时输入阻抗为负载阻抗，与传输线特性阻抗无关。**</font>
  
      > 我们其实也可以因此<u>合理外推</u>，当传输线长度为**1/2波长**时，传输线会把负载的状态“ **搬运** ”到<u>测量点</u>处；通过观察上述的负载端**开路**和**短路**时，输入电阻随长度变化的曲线，发现这一推论似乎并无问题。
  
    
  
    + **长度为1/4波长 $d=\lambda / 4+m(\lambda/2), \ m=1,2,3,...$**
  
      <font color = grey>**当传输线的长度为==1/4波长==时，将前置条件带入式(18)，我们惊奇的发现输入阻抗变为：**</font>
      $$
      Z_{in}(d=\lambda/4) = \frac{Z_0^2}{Z_L}
      $$
      <font color = grey>**看到这一堆式子似乎没有受到啥启发啊，不过事实上，这个式子用一个简单的关系把输入阻抗、特性阻抗、负载阻抗联系在一起：==几何平均值==。**</font>
  
      <font color = grey>**而它是有实际用途的，如果我们能适当调节特性阻抗，不就能将负载阻抗和前级匹配起来了吗！而事实上在实际的工程中，输入阻抗$Z_{in}$和负载阻抗$Z_L$，我们是==已知==的，特定特性阻抗$Z_0 $是可以通过调整==物理参数==得到的，如此，便能实现==阻抗匹配==。**</font>  
      <font color = grey>**==特性阻抗==：**</font>
      $$
      Z_0 = \sqrt{Z_L Z_{in}}
      $$
      <img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203233019.png" alt="image-20211224170127402" style="zoom:70%;" />
  
      <font color = grey>当然，这种阻抗匹配方法只能在**特定频点**下适用，毕竟长度取决于波长，当由于成本低等原因，依然应用广泛。</font>
  
      <div style="page-break-after:always"></div>
  
      **计算1/4波长阻抗变换器参数的过程：**
  
       ```flow
       st=>start: 已知工作频率，传输线前后级电阻，介质厚度d，材料相对介电常数
       ed=>end: 结束
       op1=>operation: 根据式(26)，得出传输线特性阻抗
       op2=>operation: 根据式(10)及平行板传输线的等效电路的参数，计算出传输线宽度
       op3=>operation: 由介电常数，计算相速度
       op4=>operation: 根据相速度和工作频率，得到波长，进一步得到该传输线的长度
       con=>condition: 分别计算该传输线的长度和宽度
       
       st->con(yes)->op1->op2->ed
       con(no)->op3(right)->op4->ed
       ```
  
      
  
      

<div style="page-break-after:always"></div>

#### :four:连接波源、负载的传输线 <font size = 3> <font color = grey>(完整的传输系统)</font></font>

<font color = grey>**前文的分析只是针对于简单的传输线及负载，实际的传输模型中，波源是一个不可忽视的存在，因为波源由于源阻抗 (简单认为是内阻吧，但这种说法不全面) 的存在，波源也有可能会和传输线失配。**</font>

<font color = grey>**事实上，笔者认为，波源只是特殊情况下的负载，不必有所顾虑，之前对于负载分析的诸多理论，仍可以套用。**</font>



##### :a: 包含波源的传输线模型

<font color = grey>**当加入了波源后，传输线模型变为：(注意不同的反射系数观察的方向不同，这里的$\Gamma_L$就是之前讨论的反射系数)**</font>

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230203233026.png" alt="image-20211225204413041" style="zoom:67%;" />

> 这里的观察方向简而言之就是，把除了方向以外的电路全部忽略掉，只分析方向上的电路

下面列出不同的反射系数的表达式

**输入反射系数：**(套用前面的公式15)  
$$
\Gamma_{in} = \Gamma(d=l) = \frac{Z_{in} - Z_0}{Z_{in} + Z_0} = \Gamma_0 r^{-2j\beta l}
$$
**波源反射系数：**(类比前面的公式13) 
$$
\Gamma_S = \frac{Z_G - Z_0}{Z_G + Z_0}
$$
**输出反射系数：**(类比下公式27，只是方向反了)
$$
\Gamma_{out} = \Gamma_S r^{-2j\beta l}
$$

**输入阻抗：**(根据式18)
$$
Z_{in} = Z_0 \frac{1 + \Gamma_{in}}{1 - \Gamma_{in}}
$$




##### :b: 关于功率

事实上，我们所设计的电路本质上都是要将信号的功率逐级传输下去，因此要研究传输线中的功率问题就十分有必要。

+ 传输线的输入功率

  传输线的输入功率其实就是波源的输出功率，而要计算功率，就需要知道电压和电流的大小；并且，由于反射电压的存在，功率事实上也可看作正向传输和反向传输的波。

  首先需要明确传输线的输入电压 / 波源的输出电压 (分压) ：
  $$
  V_{in} = V_{in}^+ + V_{in}^- = V_{in}^+(1 + \Gamma_{in}) = V_G (\frac{Z_{in}}{Z_{in}+ Z_G})
  $$
  经过一系列运算，可以得到输入功率 (无损耗) 的表达式，由于无损耗，输入功率也等于传输到负载的功率：
  $$
  P_{in} =P_L= \frac{1}{8} \frac{|V_G|^2}{Z_0} \frac{|1-\Gamma_S|^2}{|1-\Gamma_S \Gamma_0 e^{-2j\beta l}|^2} (1-|\Gamma_0|^2)
  $$
  当传输线完全匹配时 ($\Gamma_S = 0 \ ,\Gamma_0 = 0 $ )，波源达到了最大输出功率 (最大资用功率)：
  $$
  P_{in} = \frac{1}{8} \frac{|V_G|^2}{Z_0} = \frac{1}{8} \frac{|V_G|^2}{Z_G}
  $$
  当波源和传输线不匹配时 ($ \Gamma_S \neq 0 \ ,\Gamma_0 = 0 $)
  $$
  P_{in} = \frac{1}{8} \frac{|V_G|^2}{Z_0} |1 - \Gamma_S|^2
  $$

  > 功率表示时常用单位是$dBm$：
  > $$
  > P[dBm] = 10 log\frac{P}{1mW}
  > $$

  在该系统中，要实现最佳阻抗匹配，需要满足的条件是：  
  输入端：(传输线的输入电阻和波源阻抗的复数共轭匹配)
  $$
  Z_{in} = Z_G^*
  $$
  输出端：(传输线的输出电阻和负载阻抗的复数共轭匹配)
  $$
  Z_{out} = Z_L^*
  $$
  
  
  
+ 负载吸收功率

  通常，我们所讨论的传输线系统在传输时都是无损耗的，此时输入传输线的功率等于负载吸收的功率，然而，当传输线中有损耗时，容易想到，这俩功率将不相同。

  考虑损耗时，传播常数将包含衰减系数$\alpha $，新的负载吸收规律表示如下(可以和式32进行对比)：
  $$
  P_L = \frac{|V_L^+|^2}{2Z_0} (1-|\Gamma_0|^2) = \frac{1}{8}\frac{|V_G|^2}{Z_0} \frac{|1-\Gamma_S|^2}{|1-\Gamma_S \Gamma_{in} |^2}e^{-2\alpha l} (1-|\Gamma_0|^2) \ ,\\
  |V_L^+|= |V_{in}^+ e^{-\alpha l}| \ ,\\
  \Gamma_{in} = \Gamma_0 e^{-2\gamma l}
  $$
  
+ 衍生概念

  + 反射损耗 (return loss, RL)

    当波源与传输线不匹配时，会有部分能量返射回波源，即传输线输入功率达不到最大资用功率，造成能量的浪费，为了衡量这一损耗，引入反射损耗RL，它的定义是用反射功率与输入功率相比：
    $$
    RL[dB] = -10log(\frac{P_{in}^-}{P_{in}^+}) = -10log(\frac{P_r}{P_i})=-10log|\Gamma_{in}|^2= -20log|\Gamma_{in}| \ ，\\
    RL[Np] = -ln|\Gamma{in}|
    $$
    若传输线是匹配的，$\Gamma_{in} \rightarrow 0 \ , \ RL \rightarrow \infty  $，直接反映了传输线与波源之间的阻抗失配程度

    

  + 插入损耗 (insertion loss, IL)

    前面定义的反射损耗总感觉怪怪的，当RL趋近于无穷大时是最好的，然而这和损耗给人的映像是截然相反的，；众所周知，在物理或者工科中，损耗这东西似乎是越小越好，因而引入一个新的物理量——插入损耗，它的定义是传输功率与输入功率之比。
    $$
    IL[dB] = -10log(\frac{P_t}{P_i})=-10log(\frac{P_i - P_r}{P_i})=-10log(1-|\Gamma_{in}|^2)
    $$
    若波源与传输线不匹配 (例如开路或者短路)，插入损耗最大 ($IL \rightarrow \infty $)

    若波源与传输线匹配，插入损耗最大 ($IL \rightarrow 0 $)
















