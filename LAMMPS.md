# Titbits of LAMMPS
Nothing original here, everything compiled from other sources. But it is hard to find
useful instruction about LAMMPS in one place on the web. I am trying to put together 
few useful commands and ideas which I got online in one place for *my* easy comprehension.

#### Parts of an input script: [Source](http://www.u.arizona.edu/~stefanb/Files/HPCTutorials/MD-lammps-Final.pdf)
* Parts of An Input Script
  * Initialize: units, dimensions, etc.
  * Atomic positions and velocities
  * Settings:
    * Interatomic potential
    * Run time simulation parameters (e.g. timestep)
    * Fixes - operations during dynamics (e.g. thermostat)
    * Computes - calculation of properties during dynamics
  * Run!

#### Generating the initial configuration

This can be done by hand or using dedicated packages.

#### The underlying principle

#### Setting up the force field 

#### LAMMPS units 

#### Running the simulation  
* [fix nve/limit](http://lammps.sandia.gov/doc/fix_nve_limit.html) 

fix ID group-ID nve/limit xmax

xmax = maximum distance an atom can move in one timestep (distance units)

fix 1 all nve/limit 0.1

Perform constant NVE updates of position and velocity for atoms in the group each timestep. A limit is imposed on the maximum distance an atom can move in one timestep. This is useful when starting a simulation with a configuration containing highly overlapped atoms. Normally this would generate huge forces which would blow atoms out of the simulation box, causing LAMMPS to stop with an error.
#### Output particle position 

#### Output thermodynamic variables 

#### Helpful web-pages 
1. [Official LAMMPS Documentation](http://lammps.sandia.gov/doc/Manual.html) (most unhelpful for beginners, IMHO. :-1:) . Useful for looking up commands.
2. LAMMPS for dummies. :+1:
[part 1](http://wp.df.uba.ar/gebi/wp-content/uploads/sites/9/2016/06/lammps.pdf)
[part 2](http://wp.df.uba.ar/gebi/wp-content/uploads/sites/9/2016/06/ferlammps.pdf)
3. This: http://www.u.arizona.edu/~stefanb/resources.html
4. To get an idea about how you can progressivley build a MD code from scratch and increase its 
efficiency using paralleism. And, how that compares with LAMMPS. From Axel Kohlmeyer. [Link](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxha29obG1leXxneDo0YTNhZTUwMzU2NTIzNzYy)

#### Books:
1. D. Frenkel and B. Smit, Understanding Molecular Simulations: From  Algorithms to Applications, Academic Press, 2nd edition. 

2. R. LeSar, Introduction to Computational Materials Science: Fundamentals to Applications, Cambridge University Press, 1st edtion. 

3. J.G. Lee, Computational Materials Science: An Introduction. Ideal for quickly using LAMMPS and VASP
