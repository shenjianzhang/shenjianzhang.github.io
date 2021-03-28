---
layout: post
mathjax: true
title:  "考虑自转和自引力效应的运动方程(Equations of Motion)"
date:   2021-01-26 20:25:00 +0800
categories: seismology
---

这篇笔记整理了求解考虑自转(rotating)和自引力(self-gravitating)的地球模型中，一定力(源)所引起的全球的位移分布时所采用的运动方程及其边界条件的形式。

#### 本文主要参考的资料为：
- Wang, R. (1997). Tidal response of the solid Earth. In: Wilhelm H., Zürn W., Wenzel HG. (eds) Tidal Phenomena. Lecture Notes in Earth Sciences, vol 66. Springer, Berlin, Heidelberg. DOI: <https://doi.org/10.1007/BFb0011456>.
- Dahlen, F., & Tromp, J. (1998). Theoretical global seismology. Princeton University Press.

## 初始状态
在这里，我们将地球设为一个具有自引力的弹性分层模型，并且其以角速度$\boldsymbol{\Omega}$绕固定的轴自转，同时设在以地球质心为原点的球坐标系中$\theta=0$所对应的方向为$\boldsymbol{\Omega}$的方向。在未受到任何扰动时，介质处于稳定状态(steady-state)，即在地球本身的旋转参考系(rotation reference system)中位移为零，数学表示为
\\[ \begin{equation}\begin{cases}
& \rho_0(\mathbf{x}) \nabla \phi_0(\mathbf{x}) + \nabla \cdot \mathbf{T_0} - \rho_0 (\mathbf{x}) \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{x}) = 0 \\\\\
& \nabla^2 \phi_0(\mathbf{x}) = -4\pi G \rho_0(\mathbf{x})
\end{cases}
\end{equation} \\]
其中$\rho_0(\mathbf{x})$为初始稳定状态下的密度分布，$\phi_0(\mathbf{x})$为相应的引力势分布，$G$为万有引力常数，$\mathbf{T_0}$为二阶应力张量，可以进一步分解为应力球张量(静水压应力，hydtodtatic pressure)和应力偏张量
\\[ \begin{equation}
\mathbf{T_0} = -P \mathbf{I} + \boldsymbol{\sigma_0}
\end{equation} \\]
即
\\[ \begin{equation}
\nabla \cdot \mathbf{T_0} = -\nabla P + \nabla \cdot \boldsymbol{\sigma_0}
\end{equation} \\]
其中$P=-\frac{1}{3} \mathrm{tr}(\mathbf{T_0})$为静水压大小.

回到公式(1)，我们可以看出第一个方程为牛顿第二定律在非惯性系中的表达，其左侧三项分别是引力的作用，应力的反馈，以及非惯性系中的惯性力——离心力的作用，其右侧表示在旋转参考系中，介质在三者的共同作用下达到平衡。公式(1)的第二个方程则是引力的Poisson方程，给出了引力(势)和密度分布之间的关系。

## 扰动状态
### 扰动量的线性化
在初始状态的基础上，我们假设地球模型受到一个扰动，为了方便，这里我们用力$\mathbf{f}$来表示这一扰动。在这一力的作用下，地球介质也将发生扰动，在$t$时刻，$\mathbf{x}$处的介质将经过位移$\mathbf{u}(\mathbf{x},t)$到达新的位置$\mathbf{r}$，即
\\[ \begin{equation}
\mathbf{r} = \mathbf{x} + \mathbf{u}(\mathbf{x},t)
\end{equation} \\]
同时介质的密度和引力势也会发生相应扰动
\\[ \begin{equation}
\rho = \rho_0 + \rho'
\end{equation} \\]
\\[ \begin{equation}
\phi = \phi_0 + \phi'
\end{equation} \\]
应力场扰动表示为
\\[ \begin{equation}
\mathbf{T} = \mathbf{T_0}  + \boldsymbol{\sigma'} = -P \mathbf{I} + \boldsymbol{\sigma_0} + \boldsymbol{\sigma'}
\end{equation} \\]
这里需要注意的是，在弹性力学或连续介质力学中，我们可以采取两种不同的描述来表达介质的运动状态，即 **Lagrangian描述** 和 **Eulerian描述**。**Lagrangian描述** 关注的是单独的质点微元(material-fixed)，用质点的初始坐标来描述质点的性质和行为，这里的初始坐标(例如下面公式中的$\mathbf{x}$)更像是一个“标签”，表示描述的是初始状态下的哪个质点。**Lagrangian描述** 下的位移可以表达为
\\[ \begin{equation}
\mathbf{u_L}(\mathbf{x},t) = \mathbf{r}(\mathbf{x},t) - \mathbf{x}
\end{equation} \\]
即质点$\mathbf{x}$在$t$时刻占据的位置$\mathbf{r}(\mathbf{x},t)$减去初始时刻的位置$\mathbf{x}$。

**Eulerian描述** 关注的则是空间固定位置上的介质性质(space-fixed)，或者说是一种“场”的描述。Eulerian描述下的位移可以表示为
\\[ \begin{equation}
\mathbf{u_E}(\mathbf{r},t) =
\mathbf{r} - \mathbf{x}(\mathbf{r},t)
\end{equation} \\]
即$\mathbf{r}$位置减去$t$时刻占据$\mathbf{r}$位置的质点的初始位置$\mathbf{x}(\mathbf{r},t)$。

从上面两式中位移$\mathbf{u}$的空间自变量我们也可以看出，$\mathbf{u_L}$的自变量为质点初始位置$\mathbf{x}$，而相应地，$\mathbf{u_E}$的自变量为空间中的某一位置$\mathbf{r}$。

进一步地，我们还可以得到两种描述下的位移之间的关系
\\[ \begin{equation}
\mathbf{u_E}(\mathbf{r},t) =
\mathbf{u_L}(\mathbf{x}(\mathbf{r},t),t) = \mathbf{u_L}(\mathbf{r}-\mathbf{u_E}(\mathbf{r},t),t)
\end{equation} \\]
如果位移为小扰动的话，
\\[ \begin{equation}
\mathbf{u_E}(\mathbf{r},t) =
\mathbf{u_L}(\mathbf{r},t) - \mathbf{u_E}(\mathbf{r},t) \cdot \nabla \mathbf{u_L}(\mathbf{r},t)
\end{equation} \\]
可以看出两种不同描述中的位移之间的差异只是二阶小量，所以在实际计算中，我们可以忽略不同描述对于位移的影响，在后面的推导中，我们将两种位移均简单记为$\mathbf{u}$。

在分析密度、引力势和应力的扰动量之前，我们先给出任一物理量的扰动量对应的两种描述之间的关系。在一阶近似下，物理量$q$的Lagrangian扰动量$q_L'$和Eulerian扰动量$q_E'$分别由下面两式定义
\\[ \begin{equation}
q_L(\mathbf{x},t) = q_0(\mathbf{x}) + q_L'(\mathbf{x},t)
\end{equation} \\]
\\[ \begin{equation}
q_E(\mathbf{r},t) = q_0(\mathbf{r}) + q_E'(\mathbf{r},t)
\end{equation} \\]
类比前面对于位移的分析，我们得到两种描述下的物理量的关系为
\\[ \begin{equation}
q_E(\mathbf{r},t) = q_L(\mathbf{r}-\mathbf{u},t)
\end{equation} \\]
将公式(12)和(13)代入公式(14)，我们得到
\\[ \begin{equation}
q_E’(\mathbf{r},t) = q_L'(\mathbf{r},t) - \mathbf{u}(\mathbf{r},t)\cdot\nabla q_0(\mathbf{r})
\end{equation} \\]

下面具体分析密度的扰动量，在Lagrangian描述下，初始位置为$\mathbf{x}$的介质在$t$时刻的密度为
\\[ \begin{equation}
\rho_L(\mathbf{x},t) = \rho_0(\mathbf{x})+\rho_L'(\mathbf{x},t)
\end{equation} \\]
一阶近似下，扰动量(incremental Lagrangian density)为
\\[ \begin{equation}
\rho_L'(\mathbf{x},t) = - \rho_0(\mathbf{x})\nabla \cdot \mathbf{u}(\mathbf{x},t)
\end{equation} \\]
从上式我们可以发现，由于Lagrangian描述追踪某个质点，所以相应的密度变化主要来自质点微元的体积变化($\nabla \cdot \mathbf{u}$)。

对于Eulerian描述，$t$时刻在位置$\mathbf{r}$处的介质的密度为
\\[ \begin{equation}
\rho_E(\mathbf{r},t) = \rho_0(\mathbf{r})+\rho_E'(\mathbf{r},t)
\end{equation} \\]
利用公式(15)，我们有
\\[ \begin{equation}
\rho_E'(\mathbf{r},t)  = \rho_L'(\mathbf{r},t) - \mathbf{u}(\mathbf{r},t)\cdot\nabla \rho_0(\mathbf{r})
\end{equation} \\]
将公式(17)代入上式，我们得到Eulerian描述下相应的扰动量(incremental Eulerian density)
\\[ \begin{equation}
\rho_E'(\mathbf{r},t)  = - \rho_0(\mathbf{r})\nabla \cdot \mathbf{u}(\mathbf{x},t) - \mathbf{u}(\mathbf{r},t)\cdot\nabla \rho_0(\mathbf{r})
= - \nabla\cdot \left\[ \rho_0(\mathbf{r}) \mathbf{u}(\mathbf{r},t) \right\]
\end{equation} \\]

类似地，我们定义Lagrangian描述下引力势及其扰动量为
\\[ \begin{equation}
\phi_L(\mathbf{x},t) = \phi_0(\mathbf{x}) + \phi_L'(\mathbf{x},t)
\end{equation} \\]
Eulerian描述下的各量为
\\[ \begin{equation}
\phi_E(\mathbf{r},t) = \phi_0(\mathbf{r}) + \phi_E'(\mathbf{r},t)
\end{equation} \\]
与之前分析相似，利用公式(15)，我们得到
\\[ \begin{equation}
\phi_E'(\mathbf{r},t) = \phi_L'(\mathbf{r},t) - \mathbf{u}(\mathbf{r},t)\cdot\nabla\phi_0(\mathbf{r})
\end{equation} \\]

对于应力张量$\mathbf{T}$，Lagrangian描述和Eulerian描述下的应力及其扰动量分别为
\\[ \begin{equation}
\mathbf{T}_L(\mathbf{x},t) = \mathbf{T}_0(\mathbf{x}) + \boldsymbol{\sigma}_L'(\mathbf{x},t)
\end{equation} \\]
\\[ \begin{equation}
\mathbf{T}_E(\mathbf{r},t) = \mathbf{T}_0(\mathbf{r}) + \boldsymbol{\sigma}_E'(\mathbf{r},t)
\end{equation} \\]
两种描述下应力的扰动量之间的关系同样可以通过公式(15)得到
\\[ \begin{equation}
\boldsymbol{\sigma}_E'(\mathbf{r},t) = \boldsymbol{\sigma}_L'(\mathbf{r},t) - \mathbf{u}(\mathbf{r},t)\cdot\nabla\mathbf{T}_0(\mathbf{r})
\end{equation} \\]

### Eulerian描述下的运动方程
接下来我们推导扰动条件下的运动方程。对于$t$时刻位于空间位置$\mathbf{r}$处的微元的质量为
\\[ \begin{equation}
dm = \rho_E(\mathbf{r},t)dV = \left \[ \rho_0(\mathbf{r}) - \nabla\cdot \left \( \rho_0 \mathbf{u}  \right \)  \right\]dV
\end{equation} \\]
其中$dV$为微元在$t$时刻占据的体积。

这样，这一微元在$t$时刻受到的引力为$\nabla \phi_E(\mathbf{r},t) dm$，

将公式(22)和(27)代入上面的表达式，我们得到
\\[ \begin{equation}
\nabla \phi_E(\mathbf{r},t) dm = \left\[
\rho_0(\mathbf{r}) \nabla\phi_0(\mathbf{r}) + \rho_0(\mathbf{r}) \nabla\phi_E'(\mathbf{r},t) - \nabla\cdot \left \( \rho_0 \mathbf{u}  \right \) \nabla\phi_0(\mathbf{r}) \right \] dV
\end{equation} \\]
另一方面，弹性介质在受到外力作用变形时，其内部会产生一定的内力来抵抗外力的作用，从而形成使介质恢复到初始状态的趋势。这种应力作用又被称为弹性反馈(elastic feedback)。对于之前分析的微元，周围物质对它的应力作用在Eulerian描述下可以写为
\\[ \begin{equation}
\nabla\cdot\mathbf{T_E}(\mathbf{r},t) dV = \left\[
\nabla\cdot\mathbf{T}_0(\mathbf{r}) + \nabla\cdot\boldsymbol{\sigma}_E'(\mathbf{r},t)
\right\]dV
\end{equation} \\]
此外，在地球的旋转参考系中，介质还受到惯性力的作用，即Coriolis力和离心力(centrifugal force)，考虑公式(27)，惯性力的具体表达式为
\\[ \begin{equation}\begin{split}
& -\left \[ 2\boldsymbol{\Omega}\times\partial_t\mathbf{r} + \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\) \right \] dm = \\\\\
& \left \[ -2 \rho_0(\mathbf{r}) \boldsymbol{\Omega}\times\partial_t\mathbf{u}  - \rho_0(\mathbf{r}) \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\)  +
\nabla\cdot \left \( \rho_0 \mathbf{u}  \right \) \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\)
\right \] dV \end{split}
\end{equation} \\]
需要说明的是，通常在Eulerian描述下，对质点微元位移的时间求导应当采用随体导数(substantial or material derivative) $D_t=\partial_t+\mathbf{v}\cdot\nabla_r$，其中$\mathbf{v}$为$t$时刻占据空间位置$\mathbf{r}$的质点微元的速度。在一阶近似条件下，$D_t\mathbf{u} = \partial_t \mathbf{u}$，所以我们在上式中直接采用时间偏导数来替代随体导数。

最后，根据在(地球)旋转参考系中的牛顿第二定律，Eulerian描述下的运动方程可以写为
\\[ \begin{equation}
\nabla \phi_E(\mathbf{r},t) dm + \nabla\cdot\mathbf{T_E}(\mathbf{r},t) dV
-\left \[ 2\boldsymbol{\Omega}\times\partial_t\mathbf{r} + \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\) \right \] dm
= \partial_t^2 \mathbf{r} dm
\end{equation} \\]
将公式(4),(27)-(30)代人公式(31)，并考虑微元体积$dV$的任意性，整理之后我们可以得到
\\[ \begin{equation}\begin{split}
& \rho_0(\mathbf{r}) \left \[
\partial_t^2\mathbf{u} + 2 \boldsymbol{\Omega}\times\partial_t\mathbf{u} +  \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\) \right \] -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\)
= \\\\\
& \rho_0(\mathbf{r}) \left\[ \nabla\phi_0(\mathbf{r}) + \nabla\phi_E'(\mathbf{r},t) \right \] -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \nabla\phi_0(\mathbf{r})+
\nabla\cdot\mathbf{T_0}(\mathbf{r}) + \nabla\cdot\boldsymbol{\sigma_E'}(\mathbf{r},t)
\end{split}\end{equation} \\]
根据公式(1)的第一个式子，空间位置$\mathbf{r}$处初始的平衡状态可以表示为
\\[ \begin{equation}
\rho_0(\mathbf{r}) \nabla \phi_0(\mathbf{r}) + \nabla \cdot \mathbf{T_0} - \rho_0 (\mathbf{r}) \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r}) = 0
\end{equation} \\]
从公式(32)中减去公式(33)，得到Eulerian描述下增量的线性化运动方程，
\\[ \begin{equation}\begin{split}
& \rho_0(\mathbf{r}) \left \[
\partial_t^2\mathbf{u} + 2 \boldsymbol{\Omega}\times\partial_t\mathbf{u} \right \]
= \\\\\
& \rho_0(\mathbf{r}) \nabla\phi_E'(\mathbf{r},t) -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \nabla\phi_0(\mathbf{r})+
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\) +
\nabla\cdot\boldsymbol{\sigma_E'}(\mathbf{r},t)
\end{split}\end{equation} \\]
如果我们定义离心力势$\psi$为
\\[ \begin{equation}
\psi(\mathbf{x}) = \frac{1}{2}\left \[ \Omega^2x^2 - (\boldsymbol{\Omega}\cdot\mathbf{x})^2
\right\]
\end{equation} \\]
从而使得离心力$-\boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{x} \right\) $为
\\[ \begin{equation}
-\boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{x} \right\) =
\nabla \psi(\mathbf{x})
\end{equation} \\]
并定义地球重力势(位)$W$为
\\[ \begin{equation}
W(\mathbf{x}) = \phi(\mathbf{x})+\psi(\mathbf{x})
\end{equation} \\]
那么公式(34)可以改写为
\\[ \begin{equation}\begin{split}
& \rho_0(\mathbf{r}) \left \[
\partial_t^2\mathbf{u} + 2 \boldsymbol{\Omega}\times\partial_t\mathbf{u} \right \]
= \\\\\
& \rho_0(\mathbf{r}) \nabla\phi_E'(\mathbf{r},t) -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \mathbf{g_0}(\mathbf{r}) +
\nabla\cdot\boldsymbol{\sigma_E'}(\mathbf{r},t)
\end{split}\end{equation} \\]
其中$\mathbf{g_0}(\mathbf{r})=\nabla W_0(\mathbf{r})$为初始状态下地球的重力。
相应地，扰动状态下的Poisson方程为
\\[ \begin{equation}
\nabla^2 \phi_E(\mathbf{r}) = -4\pi G \rho_E(\mathbf{r})
\end{equation} \\]
将公式(18),(20)和(22)代入上式并与公式(1)中第二式比较，我们可以得到Eulerian描述下引力势增量对应的Poisson方程
\\[ \begin{equation}
\nabla^2 \phi_E’(\mathbf{r}) = 4\pi G \nabla\cdot \left\[ \rho_0(\mathbf{r}) \mathbf{u}(\mathbf{r},t) \right\]
\end{equation} \\]
这样我们就得到了Eulerian描述下的运动方程
\\[ \begin{equation}\begin{cases}
& \rho_0(\mathbf{r}) \left \[
\partial_t^2\mathbf{u} + 2 \boldsymbol{\Omega}\times\partial_t\mathbf{u} \right \]
= \rho_0(\mathbf{r}) \nabla\phi_E'(\mathbf{r},t) -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \mathbf{g_0}(\mathbf{r}) +
\nabla\cdot\boldsymbol{\sigma_E'}(\mathbf{r},t) \\\\\
& \nabla^2 \phi_E’(\mathbf{r}) = 4\pi G \nabla\cdot \left\[ \rho_0(\mathbf{r}) \mathbf{u}(\mathbf{r},t) \right\]
\end{cases}
\end{equation} \\]

### Lagrangian描述下的运动方程

首先，需要明确的是，由于Lagrangian描述是基于质点微元初始位置的“物质描述”，因此相应的积分需要在未形变的框架下进行，举例来说，体积分的单元为$dV_0$而不是$dV$。同样由于这个原因，我们首先给出一些会用到的变换关系(Chapter 2 in Dahlen & Tromp, 1998)
\\[ \begin{equation}
d\mathbf{r} = [\mathbf{I}+(\nabla \mathbf{u})^T] \cdot d\mathbf{x},\quad
d\mathbf{x} = [\mathbf{I}-(\nabla \mathbf{u})^T] \cdot d\mathbf{r}
\end{equation} \\]
\\[ \begin{equation}
\mathbf{\hat{n}}ds = (1+\nabla\cdot\mathbf{u})\mathbf{\hat{n_0}}ds_0 -
(\nabla \mathbf{u})\cdot\mathbf{\hat{n_0}}ds_0
\end{equation} \\]
\\[ \begin{equation}
dV = (1+\nabla\cdot\mathbf{u})dV_0
\end{equation} \\]
其中下标$0$表示初始状态下的各种变量。相应的守恒关系为(Chapter 2 in Dahlen & Tromp, 1998)
\\[ \begin{equation}
\int_V \rho_E \chi_E dV = \int_{V_0} \rho_0 \chi_L dV_0
\end{equation} \\]
其中$\chi_L(\mathbf{x},t)=\chi_E(\mathbf{r}(\mathbf{x},t),t)$为物理量的“特定密度”(specific density)，相对于传统密度为单位体积的物理量，$\chi$表示单位质量的物理量。类比公式(12)-(15)，物理量$q$可以表示为
\\[ \begin{equation}
q_E = \rho_E \chi_E
\end{equation} \\]
>>对公式(45)守恒关系的理解：左侧为$t$时刻介质所受的某种力，如引力这样的体力或者牵引力这样的面力，这个力的整体作用可以看作是空间中每个位置的质点微元$\rho_E dV$受到的作用$\chi_E$的积分，也就是对Eulerian描述下每位置的积分；右侧则是“整体作用”在Lagrangian描述下的表达，由于Lagrangian描述采用的是“物质坐标”，因此积分本质上是对初始位置$\mathbf{x}$上质点微元的积分(而非对$t$空间位置的积分)，对于每一个单独的质点微元，其“质量”始终为$\rho_0 dV_0$，$t$时刻受到的作用为$\chi_L$.

利用公式(45)，我们可以从牛顿第二定律在Eulerin描述下的形式(公式(31))得到其在Lagrangian描述下的形式
\\[ \begin{equation}
\rho_0 \left\[
\partial_t^2 \mathbf{r} +  2\boldsymbol{\Omega}\times\partial_t\mathbf{r} + \boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{r} \right\)
\right\]  =
\rho_0 \mathbf{h_L}  + \nabla\cdot \mathbf{T_{PK}}
\end{equation} \\]
其中$\mathbf{h_L} = \mathbf{h_0} + \mathbf{h_L'}$为Lagrangian描述下质点微元受到的引力，一阶近似下，并利用公式(15)，我们有
\\[ \begin{equation}
\mathbf{h_0} = \nabla\phi_0, \quad
\mathbf{h_L'} = \nabla\phi_E’ + \mathbf{u}\cdot\nabla(\nabla\phi_0)
\end{equation} \\]
$\mathbf{T_{PK}}$称为Piola-Kirchhoff应力，可以被简单理解为单位初始界面面积上的牵引力，即
\\[ \begin{equation}
d\mathbf{f_E} = \mathbf{\hat{n_0}} \cdot \mathbf{T_{PK}}ds_0
\end{equation} \\]
其中
\\[ \begin{equation}
d\mathbf{f_E}=\mathbf{\hat{n}} \cdot \mathbf{T_{E}}(\mathbf{r},t)ds =
\mathbf{\hat{n}} \cdot \mathbf{T_{L}}(\mathbf{x},t)ds
\end{equation} \\]
利用之前给出的初始状态和$t$时刻面积微元之间的转换关系(公式(43))，我们得到扰动量$\boldsymbol{\sigma_{PK}’}(\mathbf{x},t)=\mathbf{T_{PK}}(\mathbf{x},t)-\mathbf{T_0}(\mathbf{x},t)$和$\boldsymbol{\sigma_L'}(\mathbf{x},t)$之间的关系
\\[ \begin{equation}
\boldsymbol{\sigma_{PK}'} = \boldsymbol{\sigma_L'} +(\nabla\cdot\mathbf{u})\mathbf{T_0}-(\nabla\mathbf{u})^T \cdot \mathbf{T_0}
\end{equation} \\]
与之前分析类似，从公式(47)中减去初始状态(公式(1)中式一)，并将相应的一阶近似结果代入，我们得到Lagrangian描述下增量的运动方程如下
\\[ \begin{equation}
\rho_0 \left\[
\partial_t^2 \mathbf{u} +  2\boldsymbol{\Omega}\times\partial_t\mathbf{u} \right\] =
\rho_0\nabla\phi_L' - \rho_0\nabla(\mathbf{u}\cdot\nabla\phi_0)+
\rho_0\mathbf{u}\cdot\nabla\mathbf{g_0} +
\nabla\cdot\boldsymbol{\sigma_{PK}'}
\end{equation} \\]
这里我们还利用了由离心力势计算公式(公式(36))推导出的关系$\boldsymbol{\Omega} \times \left\( \boldsymbol{\Omega}\times \mathbf{u} \right\) = \mathbf{u}\cdot\nabla\nabla\psi$.

此外，我们还可以采用另一种简单的方式得到这一运动方程。由于$\nabla_r = \nabla_x - (\nabla_x\mathbf{u})\cdot\nabla_x$，因此增量的运动方程中的不同空间求导之间的区别在一阶近似下可以被忽略。这样，我们可以直接根据Eulerian描述下的运动方程得到对应的Lagrangian描述下的运动方程。将公式(23)和(26)代入公式(41)式一，我们得到:
\\[ \begin{equation}\begin{split}
& \rho_0 \left\[ \partial_t^2 \mathbf{u} +  2\boldsymbol{\Omega}\times\partial_t\mathbf{u}
\right\] = \\\\\
& \rho_0\nabla\phi_L' - \rho_0\nabla(\mathbf{u}\cdot\nabla\phi_0) -
\nabla\cdot(\rho_0\mathbf{u})\mathbf{g_0}+
\nabla\cdot\boldsymbol{\sigma_L'} - \nabla\cdot(\mathbf{u}\cdot\nabla\mathbf{T_0})
\end{split}
\end{equation} \\]
对于公式(52)和公式(53)给出的两种Lagrangian描述下的运动方程，我们可以利用初始状态平衡方程(公式(1)式一)和$\boldsymbol{\sigma_L'}$与$\boldsymbol{\sigma_{TK}'}$的关系(公式(51))来证明其等价性。
>> 等价性的证明：
\\[ \begin{split}
 \rho_0\mathbf{u}\cdot\nabla\mathbf{g_0} + \nabla\cdot\boldsymbol{\sigma_{PK}'}
= & -\mathbf{u}\cdot\nabla(\nabla\cdot\mathbf{T_0}) + \nabla\cdot\boldsymbol{\sigma_L'} +
\nabla\cdot[(\nabla\cdot\mathbf{u})\mathbf{T_0} - (\nabla\mathbf{u})^T\cdot\mathbf{T_0}] \\\\\
= & \nabla\cdot\boldsymbol{\sigma_L'} +(\nabla\cdot\mathbf{u})\nabla\cdot\mathbf{T_0}
-\nabla\mathbf{u}:\nabla\mathbf{T_0} -\mathbf{u}\cdot\nabla(\nabla\cdot\mathbf{T_0})\\\\\
= & \nabla\cdot\boldsymbol{\sigma_L'} - \nabla\cdot(\rho_0\mathbf{u})\mathbf{g_0}
-\nabla\cdot(\mathbf{u}\cdot\nabla\mathbf{T_0})
\end{split}\\]

利用类似的思路，将公式(23)代人公式(40)，我们可以得到Lagrangian描述下引力势的Poisson方程，从而写出Lagrangian描述下与公式(41)相对应的完整的运动方程:
\\[ \begin{equation}\begin{cases}
& \rho_0 \left\[ \partial_t^2 \mathbf{u} + 2\boldsymbol{\Omega}\times\partial_t\mathbf{u}
\right\] = \\\\\
& \rho_0\nabla\phi_L' - \rho_0\nabla(\mathbf{u}\cdot\nabla\phi_0) -
\nabla\cdot(\rho_0\mathbf{u})\mathbf{g_0}+
\nabla\cdot\boldsymbol{\sigma_L'} - \nabla\cdot(\mathbf{u}\cdot\nabla\mathbf{T_0}) \\\\\
& \nabla^2 \phi_L' = 4\pi G \nabla\cdot ( \rho_0 \mathbf{u} ) + \nabla^2(\mathbf{u}\cdot\nabla\phi_0)
\end{cases}
\end{equation} \\]

### 混合描述下的运动方程
我们可以看出，完全采用Lagrangian描述的运动方程中，引力势的表达较为复杂，这是因为对于引力这样的“场量”，Eulerian描述是再自然不过的了。另一方面，通常我们在定义应变和应力应变之间的关系，即本构关系时，均是在Lagrangian描述下进行的，这是采用Lagrangian描述的优势。考虑到这两点，在地球物理中大家往往采用混合描述下的运动方程(mixed form of equations of motion)，即采用Eulerian描述的势函数和Lagrangian描述的应力，具体写为
\\[ \begin{equation}\begin{cases}
& \rho_0 \left \[
\partial_t^2\mathbf{u} + 2 \boldsymbol{\Omega}\times\partial_t\mathbf{u} \right \]
= \rho_0 \nabla\phi_E' -
\nabla\cdot\left\(\rho_0\mathbf{u}\right\) \mathbf{g_0} +
\nabla\cdot\boldsymbol{\sigma_L'} - \nabla\cdot(\mathbf{u}\cdot\nabla\mathbf{T_0}) \\\\\
& \nabla^2 \phi_E’ = 4\pi G \nabla\cdot \left\( \rho_0 \mathbf{u} \right\)
\end{cases}
\end{equation} \\]

## 边界条件
