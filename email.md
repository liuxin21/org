hi tanya

i plan to go through my research in this outline:

- models:
1. started with the matched density model (simple, in oerder to get a result at least)
2. abel 2012 model

- numerical method:
1. first order projection method
2. extend it with prediction-correction

if you are avalible next week, I can show you the drafts of the process.
I'll apporeciate it if you can give me some advice after you read it next week.


另：提出一些问题。
could you give me some code examples of meshing in 3D by Python?


I try to run the code of the most simple case in my paper 
(matched density and viscosity, first derivative in space, the most basic explicit method),
but I can not get a result.

May you help me to point out what mistakes I made in this code?

Only the code of the simplest case is running, I can solve the complecated cases in my paper.

I'll appreciate it if you can send me an example code of basic two phase flow.

## re

I fixed the phi, so phi will not blow up quite significantly.

As for the mistakes you pointed out last time:

3. I didn't find some wrong with the Neumann bc

4. pressure correction is usually only done once, you don't need to make a for loop. But in the lecture you gave me last time, he uses for it=1:maxit to slove pressure.

Do you have any other advice? like, will it be easy to use 三对角方程组，托马斯算法，Crank-Nicolson ?