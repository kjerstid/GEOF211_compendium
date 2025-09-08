(BoundaryConditions:Introduction)=
# Boundary conditions

When you run a numerical model, you will naturally have to make some choices for the size of the model domain. We cannot have infinite model domain sizes, so in 1D, for example, we typically define an x-range such as $x\in[0,L]$)an then construct an initial condition matching that x-range. 

When we set a maximum range for a model domain, we introduce boundaries. Not all boundaries exist in real life. Let's say you want to make a model of a long and narrow fjord. You will typically place the fjord inside a rectangular model domain, where one of the boundaries cut across the fjord inlet. This boundary does not exist in real life. The circulation inside the fjord is connected to the coastal region outside of the fjord, and you will loose some of the true nature of the flow dynamics inside your fjord. This is especially problematic for for propagation of pressure waves. In the real world they will propagate smoothly through the fjord inlet, while they cannot doe so in your model. 

For simple problems, like the ones we have looked at so far, we have deliberately avoided the boundaries by 1) constructing an initial conditions that does not have high values or gradients near the boundaries, and 2) ensuring that the model does not run long enough for the initial signal to reach the boundaries. This works well for simple examples, and is also widely used in regional models where you can make the model domain larger than necessary and disregard the model output near the boundaries. However, in most modeling tasks (unless you run a global scale spherical model), we will have to consider boundary conditions. 

There are many types of boundary conditions. For each model experiment, we will have to consider what physics we are trying to replicate at the boundaries. Should for example, the boundaries appear as walls that enclose your domain, as in a lake? Or should the boundaries be open, such as in a fjord mouth, where water can flow in and out of the boundary? Or could you avoid the issue with boundaries by bending the 1D model domain into a circle, where the fluid is smoothly flowing out of one boundary an re-entering at the other end - like a circular channel?

In this chapter we will look into various types of boundary conditions and the termiology we use for these boundary conditions in mathematical sense, and in practical modeling sense. 

 
```{tableofcontents}
```
