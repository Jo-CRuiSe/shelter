---
title: Lumerical入门笔记
date: 2024-06-26 22:30:00 +0800
categories: [Notes]
tags: []
pin: false
author: jo
toc: true
commments: true
typora-root-url: ../../Jo-CRuiSe.github.io/
math: true
mermaid: false
---

# The FDTD(finite-difference time-domain) method（有限时域差分法）

- Time-domain simulation
  - E and H fields are solved using a time-stepping algorithm
- E and H fields are solved at discrete positions in space

## Advantages of the FDTD method

- 准确
- 普适
- 任意复杂形状
- 宽谱结果

## Simulation time and memory requirements

当器件在一个方向上为无限长时，可以使用x,y坐标进行仿真

|                     |               3D                |               2D                |
| :-----------------: | :-----------------------------: | :-----------------------------: |
| Memory Requirements | $$\sim V \cdot (\lambda/dx)^3$$ | $$\sim A \cdot (\lambda/dx)^2$$ |
|   Simulation Time   | $$\sim V \cdot (\lambda/dx)^4$$ | $$\sim A \cdot (\lambda/dx)^3$$ |

> $$V$$​：仿真体积
>
> $$A$$：仿真面积
>
> $$(\lambda/dx)^3$$：仿真密度

## Boundary conditions

PML

- Perfectly matched layer, absorbing boundary

Metal

- Perfectly reflecting boundary

Periodic

- Unit cell (structures and EM fields) contained in the simulation is repeated in the periodical direction (eg. source at normal incidence, along coordinate axes)

Bloch

- Periodic with a phase shift between each unit cell

Symmetric/ anti-symmetric

- Used to reduce the required stimulation volume when the structure and source have a plane of symmetry

## Sources

- Dispole 偶极子光源
- Gaussian 高斯或大数值孔径（矢量）
- Plane wave 平面波光源
- Total-field scattered-field 全场散射场光源：主要用于散射、吸收、削光界面
- Mode 波导模式光源
- Import 自输入光源

## Monitors

- Refractive index 折射率：用于查看器件设置是否正确
- Field time 时间：可以是点、线、面、立体的
- Movie 电影：可以查看相互作用
- Frequency-domain field profile/power 场分布/功率
- Mode expansion 模式分解

##  Running a simulation

一般情况下，进度表显示不超过95%结束可以得到准确的频域结果

正常结束运行有两种方法：

- 达到预先设置的Autoshutoff Min，强烈推荐
- 达到预先设置的仿真时间

## FDTD Solutions Workflow

1. 创建物理结构
2. 添加仿真区+边界
3. 添加光源
4. 添加监视器

## Using Eigen Solver

- 定义物理结构
- 定义仿真区域
- 频域分析

## Basic Scripting

simple mathematics: plot some simple functions

```matlab
> x = linspace(-10,10,500);
> y = sin(x);
> plot(x, y, "x", "y", "sin(x)");

> y = exp(-x^2/9)*sin(10*x);
> plot(x, y, "x", "y", "exp(-x^2/9)*sin(10*x)");

> ?size(x);
```

## Advanced Scripting

- 获得模式参数

```matlab
?getdata("mode1");
% 参数是 surface_normal dimension f neff loss TE polarization fraction waveguide TE/TM fraction x y z Ex Ey Ez Hx Hy Hz
```

- 获得频域曲线

```matlab
?getdata("frequencysweep");
% 参数是 neff loss vg D beta f f_vg f_D mode_number
```

例如

```matlab
f = getdata("frequencysweep", "f"); %得到频率
```

# 2.5D FDTD Propagator

## How the FDTD method works

E and H are discrete in time
$$
\vec{E}(t) \rightarrow \vec{E}^{n\Delta t},\space \vec{H}(t) \rightarrow \vec{H}^{(n + \frac{1}{2})\Delta t}
$$
The basic FDTD time-stepping relation:
$$
\vec{E}^{n+1} = \vec{E}^{n} + \alpha \vec{\nabla} \times \vec{H}^{n+\frac{1}{2}}
$$

$$
\vec{H}^{n+\frac{3}{2}} = \vec{H}^{n+\frac{1}{2}} + \beta \vec{\nabla} \times \vec{E}^{n+1}
$$

$$
\vec{H}^0 \rightarrow \vec{H}^\frac{1}{2} \rightarrow \vec{E}^1 \rightarrow \vec{H}^\frac{3}{2} \rightarrow ...
$$

> 不会产生人为的增益/衰减

## Using the time-domain propagator

- 定义物理结构
- 定义仿真区域
- 添加光源
- 添加监视器

## Dispersive Material

- 时域都是实数，频域是复数
- 频域关系：$$ \vec{D}(\omega) = \varepsilon(\omega)\vec{E}(\omega)$$
- 时域关系：$$ \vec{D}(t) = \varepsilon(t) \ast \vec{E}(t) = \int_0^t \vec{E}(t') \varepsilon(t - t')dt'$$

## Sources

The propagator has a variety of sources available:

- Dipole
- Slab Gaussian beam （标量）
- Slab plane wave
- Mode
- Total field/scattered field
- Large Na source （矢量）
- User-defined

## FDTD is  a time domain technique

$$
\vec{E}(\omega) = \int_0^{T_{Sim}} e^{i \omega t} \vec{E}(t) dt
$$

> 如果使用所谓“渐变”稳态场激励，就丧失了时域算法的优势

## Tips

- What mesh size should I use?
  - "Mesh accuracy" of 1 or 2 for initial setup (faster)
  - Use "meh accuracy" of 2-4 for final simulations
  - "Mesh accuracy" 5-8 is almost never necessary
- How long a simulation time should I use?
  - Start with long simulations times and let the "auto-shutoff" feature find out when you can stop the simulation
  - Check with point time monitors
- Avoid simulating homogeneous regions with no structure
- 与FDTD Solutions不同，光源的偏振特性不能在光源那里修改

# Solvers

## FDE Solver

Can be used for 1D(slab) or 2D structure cross sections

Look for solutions to Maxwell's equations of the form
$$
\vec{E}(x,y,z,\omega) = exp(i\beta_m z) \vec{E}_m(x,y,\omega)
$$

$$
\vec{H}(x,y,z,\omega) = exp(i\beta_m z) \vec{H}_m(x,y,\omega)
$$

可计算的物理特性：

模式分布、群折射率、色散、弯曲损耗、耦合长度、重叠积分

## varFDTD Solver

时域

Suitable for simulation of planar components including ring resonators, couplers, splitters, cross-overs, etc

3D planar waveguide geometry collapsed into 2D effective materials which capture material and waveguide dispersion.

应假设传播过程中在垂直方向几乎不改变

2D仿真速度但是接近3D仿真精度

## EME Solver

频域

严格求解麦克斯韦方程

一次仿真可以获得多个模式输入和多个模式输出的结果

将波导器件沿一个方向分段，每段就是一个cell

## When to use what solver

- 平面类波导
  - 垂直方向上有耦合：EME
  - 没有垂直方向上耦合
    - 传播是全方向的：varFDTD
    - 沿一个方向传播：EME
- 非平面类波导
  - 光栅类：EME
  - 光在垂直方向上有耦合的输入和输出：3D FDTD

## Typical workflow

1. 添加物理结构
2. 添加仿真区域（EME中需要分段）
3. 添加光源（EME中需要选输入输出端口、入射模式）
4. 添加监视器
5. 检查材料的拟合和内存需求
6. 进行仿真
7. 分析/输出
8. 更改结构参数直到达到预期效果

