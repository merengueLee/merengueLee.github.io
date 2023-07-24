---
layout:     post
title:      Cadence Virtuoso Simulation Tips (Updating)
subtitle:   Cadence Virtuoso仿真提示（更新中）
date:       2023-07-19
author:     Bohao
header-img: img/post-bg-keybord.jpg
catalog: true
original: true                    #是否原创申明
tags:
    - Analogue IC design
    - Mixed Signal IC design
    

---





# Cadence Virtuoso Simulation Tips (Updating)



### Some parameter settings in Transient simulation

Reference: https://web.engr.oregonstate.edu/~moon/kaj/cadence.html#top

---

#### Accuracy

There are some parameters that are useful but confusing when I do Transient simulation, so I  did the research and figured out some of them. These settings can be found when you click the “**Option**” button and they will determine the behaviour of the simulation.

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230719202449.png" alt="screenshot 2023-07-19 at 20.24.42" style="zoom:40%;" />

Shown above, in the **INTEGRSTION PARAMETERS** column, it lists some methods which specifies the integration method, and it will also determine the accuracy and simulation speed. Also, the **ACCURACY PARAMETERS** column also lists some parameters which can affect the accuracy. 
Remember! Never set this things by yourself unless you want a unreliable results! What you need to so is set the “errpreset” at the beginning of Transient simulation setting page which concluded three options: liberal, moderate and conservative, and they will specifies the parameters related to the accuracy, shown as below.

![screenshot 2023-07-19 at 20.39.13](https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230719203918.png)

“liberal” is the most inaccurate one, while the “conservative” has the highest accuracy.

#### Convergence

> ```
> If the circuit you are simulating can have infinitely fast transitions (for example, a circuit that contains nodes with no capacitance), Spectre might have convergence problems. To avoid this, you must prevent the circuit from responding instantaneously.
> ```

In the **CONVERGENCE PARAMETERS** column, the parameter “cmin” which stands for the minimum capacitance to ground at each node can be set to a physically reasonable non-zero value to help converge the simulation. For example, in my simulation, I set it to $1 fF$.



#### Strobing

Strobing is a method to reduce the number of output data points, and it can also be used for sampling the ouput. Therefore, that’s why it’s useful in ADC verfication. 

<img src="https://raw.githubusercontent.com/merengueLee/my-gallery/master/imag/20230719204937.png" alt="screenshot 2023-07-19 at 20.49.31" style="zoom:40%;" />

There are parameters that you can set:
“**strobeperiod**” : sets the interval between points that you want to save.
“**strobedelay**” : sets the offset within the period relative to ‘skipstart’.
“**skipcount**” : If this is set to N, then only every N'th point is saved.
Normally, I set the strobeperiod to sampling time of ADC I’m testing.