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



### 1. Some parameter settings in Transient simulation

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



### 2. The difference between Harmonic Balance & Shooting in PSS simulation

Reference: https://community.cadence.com/cadence_blogs_8/b/rf/posts/tip-of-the-week-when-to-use-harmonic-balance-engine-vs-shooting-newton-engine

---

They are two simulation engines in the PSS setting, and an inappropriate setting can lead to the “no convergence” issue of simulation.

Based on Tawna’s(author of the reference) description: 

> The **Shooting** Newton algorithm uses an adaptive time step control, which is particularly effective for <u>sharp transitions</u>. Convergence is robust and not as sensitive to <u>model imperfections</u>.

> **Harmonic balance** (HB) is much faster for mildly nonlinear circuits.

##### Conclusion: 

These two engines have different algorithms, and if your circuit is mildly nonlinear, **HB** is more recommended because it’s <u>faster</u> than **Shooting**. 
It looks like the **Shotting** is <u>easier to get convergence</u> because normally non-convergence is caused by non-linearity. 
The results should be similar if the simulation parameter setting is properly.



Tawna also listed some cases that are suitable for each engine(I just copy them):

**For Harmonics Balance**: 

+ High dynamic range, weakly-nonlinear systems
  + RF front-ends (LNA, Mixer) 
  + IQ modulators
+ Mildly nonlinear oscillators with resonators, such as
  - LC oscillators 
  - Crystal oscillators 
  - Negative-gain oscillators 
+ Circuits with distributed components
  - Transmission lines 
  - S-parameter models

**For Shooting Newton:** 

+ Circuits where input signals have sharp transitions 

+ Strongly nonlinear circuits

  - Frequency dividers 

  - Strongly-nonlinear resonatorless **oscillators**, such as
    - Ring oscillators, 
    - Relaxation oscillators,
    - Oscillators containing digital control components,
    - Oscillators with dividers.



