(BoundaryConditions:Introduction)=
# Boundary conditions

When you run a numerical model, you will naturally have to make some choices for the size of the model domain. In 1D, for example, we typically define an x-range such as $x\in[0,L]$)an then consturct an initial condition matching that x-range. 

For simple problems, like the ones we have looked at so far, we have deliberately avoided the boundaries by 1) constructing an initial conditions that does not have high values or gradients near the boundaries, and 2) ensuring that the model does not run long enough for the initial signal to reach the boundaries. This works well for simple examples, but in most modeling tasks (unless you run a global scale spherical model), we will have to consider boundary conditions. 

There are many types of boundary conditions. For each model experiment, we will have to consider what physics we are trying to replicate at the boundaries. Should for example, the boundaries appear as walls that enclose your domain, as in a lake? Or should the boundaries be open, such as in a fjord mouth, where water can flow in and out of the boundary? Or could you avoid the issue with boundaries by bending the 1D model domain into a circle, where the fluid is smoothly flowing out of one boundary an re-entering at the other end - like a circular channel?

In this chapter we will look into various types of boundary conditions and the termiology we use for these boundary conditions in mathematical sense, and in practical modeling sense. 

 
```{tableofcontents}
```
