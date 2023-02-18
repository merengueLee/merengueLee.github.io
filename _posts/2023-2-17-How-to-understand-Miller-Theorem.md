---
layout:     post
title:      How to understand Miller Theorem
subtitle:   深入理解密勒定理
date:       2023-2-17
author:     Bohao
header-img: img/post-bg-ios9-web.jpg
catalog: true
original: true                    #是否原创申明
tags:
    - Analogue IC design
    

---



# How to understand MILLER'S Theorem

---

## Miller’s theorem

To begin with, a brief introduction to Miller’s theorem is necessary.

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230217170004.png" alt="screenshot 2023-02-17 at 16.59.57" style="zoom:50%;" />

In short, according to the diagram above, in order to make the current flow in/out of those two nods (X & Y) unchanged. the equations can be get:

$$
Z_1 = \frac{Z}{1-\frac{V_Y}{V_X}} \\
Z_2 = \frac{Z}{1-\frac{V_X}{V_Y}}
$$

which is Miller’s Theorem.



## Understanding 

### How to measure the input impedance

From above, we could say that Miller’s Theorem inverts a “floating” impedance to the input impedance of nodes X and Y, so how do we usually measure the input impedance? Usually, we choose this way below.

+ Input a step voltage ($\Delta V$) into the testing node.
+ Measure the charge offered by this voltage source [$\Delta Q = \Delta V \cdot C$], and then the input impedance of this node can be get.



### In this case (a capacitive impedance)

This diagram shows a very common scenario that a capacitor is connected between the input and output of an amplifier.

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230217220152.png" alt="screenshot 2023-02-17 at 22.01.45" style="zoom:33%;" />

<u>Node X:</u> $\Delta V$;    
<u>Node Y:</u> $- A \cdot \Delta V$.
$\Delta Q$ on $C_F$ : $(1+A) \cdot \Delta V \cdot C_F$, and that applies to the input capacitance: 
$$
C_{in} = (1+A) \cdot C_F
$$



### Something Interesting

If we look back to the introduction to Miller’s Theorem, there is something that can be found: $Z_1 + Z_2 = Z$. 
If we think that not in a mathematical way, it looks like we “cut” the impedance into two pieces ($Z_1$ & $Z_2$ ) and at that “cutting point”, the voltage drops to **0**, like a “virtual ground” (of course, **small signal voltage**, not the real voltage).

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230218233324.png" alt="screenshot 2023-02-18 at 23.33.16" style="zoom:40%;" />

> Similarly, recall the case above. $V_X$ and $V_Y$ have different polarities, and there will have a point in $C_F $whose voltage must be 0.



---
### BTW: 

The measurement of **input impedance** also reminds me of how we measure the resistor or “equivalent resistor” in a circuit. And before we talk about it, let’s first define what is a resistor.

#### what does a resistor do

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230217223001.png" alt="screenshot 2023-02-17 at 22.29.53" style="zoom:30%;" />

The resistor is something that impedes, and slows down, the movement of charge. When we think about a resistor below, it’s quite easy to conclude that the current across the resistor is: $I = (V_1 - V_2) / R$.

Therefore in a given time, $ t$, a charge of $Q = (V_1 - V_2) t /R$  transfers from X to Y.

> **Wait, what? What a commonsense! Do I need you to tell me that?**

Yes, it is a commonsense, but if we think that carefully, and if we can arrange this in some other way, we can have a resistor-substitute that is quite different from the resistor we considered before. A very classic example of this is switched capacitor (shown below), and after applying this theory, we can know the **equivalent resistor** of this  circuit is:

$$
R_{eq} = \frac{1}{C_1 \cdot F_{CLK}} 
$$

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230217225306.png" alt="screenshot 2023-02-17 at 22.53.01" style="zoom:30%;" />



### Reference

[1] Razavi B. Design of analog CMOS integrated circuits[M].





















