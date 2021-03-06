Volume-of-Fluid (VoF) based CFD techniques have been used by researchers to model droplet-film impacts by **applying an extremely fine computational mesh** to resolve the **flow around the droplets and the film**. Such methods, because of the **computing cost** are, however, not practical for applications of interest in this work.

In this work, droplets are not explicitly resolved to a computational mesh, they are represented as **point source terms** in an **unsteady Lagrangian formulation**. 
Representing droplets in Lagrangian formulation, as done here, is not new but the coupling with the continuous phase to form flowing film from user defined source terms and onward tracking of splashing droplets using published correlations are novel. 
The mass and momentum of the Lagrangian particle are transferred into VoF by adding the source term as a “handover” of mass from the discrete phase to VoF film, in the continuity and momentum equations after interface tracking is done. 
Heat transfer is achieved by mass averaging of the temperatures in the spread zone equivalent to the spherical droplet. 
The particle tracking is then stopped and the particle is subsequently removed from the simulation. 
The method is developed using the ANSYS-Fluent CFD software and formulated using an enhanced VoF technique. 
The developed technique is validated using a series of simple numerical checks on single Lagrangian droplet-to-film to more complex spray-to-film test cases to check for mass, momentum and heat transfer with reasonably good performance.

在这项工作中，液滴不是明确地解析为计算网格，它们被表示为非稳定拉格朗日公式中的点源项。用拉格朗日公式表示的液滴并不是新的，而是与连续相耦合，从用户定义的源项形成流动膜，并使用公开的相关性追踪飞溅液滴。通过将源项作为从离散相到VoF膜的质量的“切换”，在接口跟踪完成之后的连续性和动量方程中，将拉格朗日粒子的质量和动量转移到VoF中。传热是通过质量平均扩散区中的温度相当于球形液滴实现的。然后停止粒子跟踪，然后从模拟中除去粒子。该方法使用ANSYS-Fluent CFD软件开发，并使用增强型VoF技术进行配制。所开发的技术通过一系列简单的拉格朗日液滴到膜的简单数值检验，对更复杂的喷涂到膜测试案例进行验证，以检查质量，动量和传热性能，并具有相当好的性能。