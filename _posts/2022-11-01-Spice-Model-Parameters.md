---
layout:     post
title:      Spice Model Parameters
subtitle:   Spice Model解读
date:       2022-11-1
author:     Bohao
header-img: img/post-bg-ios9-web.jpg
catalog: true
original: true                    #是否原创申明
tags:
    - Analogue IC design
    - Circuit Simulation

---



# Spice Model Parameters

---

| Spice Name |    Symbol    |                    Model Parameter                    |   Units   | Default  |
| :--------: | :----------: | :---------------------------------------------------: | :-------: | :------: |
|   Level    |              |                      Model Type                       |           |    1     |
|            |              |                                                       |           |          |
|     KP     | $ \mu C_{OX} $ |             Transconductance coefficient              |  $A/V^2$  | 20$\mu$  |
|    VTO     |   $V_{t0}$   |              Zero-bias threshold voltage              |    $V$    |    0     |
|   LAMBDA   |  $\lambda$   |       Channel-length modulation <br />parameter       | $V^{-1}$  |    0     |
|   GAMMA    |   $\gamma$   |                 Body-effect parameter                 | $V^{1/2}$ |    0     |
|    PHI     |   $\phi_f$   |                   Surface Potential                   |    $V$    |   0.6    |
|     W      |     $W$      |                     Channel width                     |  Meters   | Defined  |
|     L      |     $L$      |                    Channel length                     |  Meters   | Defined  |
|     WD     |    $W_D$     |       Lateral diffusion width<br />横向扩散宽度       |  Meters   |    0     |
|     LD     |    $L_D$     |      Lateral diffusion length<br />横向扩散长度       |  Meters   |    0     |
|    TOX     |   $T_{ox}$   |                    Oxide thickness                    |  Meters   | $\infty$ |
|     UO     |   $\mu$      |                   Channel mobility                  | $cm^2/V/s$  |  350     |
|               |   |    |   |   |
|     RD     |    $R_d $    |                Drain ohmic resistance                 | $\Omega$  |    0     |
|     RS     |    $R_s$     |                Source ohmic resistance                | $\Omega$  |    0     |
|     RG     |    $R_g$     |                 Gate ohmic resistance                 | $\Omega$  |    0     |
|     RB     |    $R_b$     |                 Bulk ohmic resistance                 | $\Omega$  |    0     |
|    RDS     |   $R_{ds}$   |   Drain-source shunt resistance<br />漏-源旁路电阻    | $\Omega$  | $\infty$ |
|            |              |                                                       |           |          |
|    CGSO    |  $C_{GSO}$   | Gate-source overlap <br />capacitance / channel width |   $F/m$   |    0     |
|    CGDO    |  $C_{GDO}$   |  Gate-drain overlap <br />capacitance/channel width   |   $F/m$   |    0     |
|    CGBO    |  $C_{GBO}$   |   Gate-bulk overlap <br />capacitance/channel width   |   $F/m$   |    0     |
|     KF     |    $K_f$     |               Flicker noise coefficient               |           |    0     |
|     AF     |    $A_f$     |                Flicker noise exponent                 |           |    1     |
|            |              |                                                       |           |          |
|            |              |                                                       |           |          |

In addition to that, sometimes we need to guestimate the operating points of the transistors, so it's important to know the Transconductance coefficient. However, the PDK file may not show that directly, which means it need to be calculated. To get that, we need two coefficients: UO($\mu$) and TOX($T_{ox}$), and then it can be calculated:

$$
KP = UO \times \frac{8.85\times 10^{-14} \times 3.9 \ \ F/cm}{TOX}
$$

be careful with the units.



