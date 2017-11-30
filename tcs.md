
## Equation:
$$
\frac{\partial}{\partial t} (\rho \omega_i) + \Delta \cdot (\rho \omega_i \mathbf u) = - \Delta \cdot \bf j_i + R_i
$$

> NOTE:
> $\rho \omega_i = \rho_i$, 上式中 $\rho$ 和 $\bf u$ 是平均，其他的各peices都不同。

## transport mechanisms

The Transport of Concentrated Species interface (tcs) always accounts for transport due to diffusion. 

### diffusion model

#### 3个diffusion model: 

1. Maxwell-Stefan
2. Mixture-averaged
3. Fick’s law

#### additional transport mechanism

不同的模型描述 mass flux vector $bf j_i$ 的方程不一样，这里我们只介绍 Fick’s law diffusion model.

## Domain, Boundary, and Pair Nodes 

上来就有三个nodes，其中两个是domain(transport properties, initial values)，一个是bc(no flux)， 

Nodes 是根据你在 TCS settings 里勾选的选项所决定的。例如，如果勾了convection, 那么就会有Tturbulent mixing这个nodes选项。

### transport properties

transport properties node 的 Setting 里有以下这几个部分：
Model input (temperature & absolute pressure), density, convection, diffusion

#### model inputs
为 interface 提供 temperature 和 pressure, 既可以来自其他的 interface, 也可以是自己设置的值。

- temperature 
1. 用来计算 density (ideal gas law)
2. 用来计算 J 里面的 thermal diffusion (如果提供了 thermal diffusion coefficients 的话)

- pressure
1. 用来计算 density (ideal gas law)
2. 用来计算 diffusional driving force (如果用的是Maxwell-Stefan Diffusion Model 的话)
