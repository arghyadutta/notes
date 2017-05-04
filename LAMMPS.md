# Titbits of LAMMPS
Nothing original here, everything compiled from other sources. But it is hard to find useful instruction about LAMMPS in one place on the web. I am trying to put together few useful commands and ideas which I got online in one place for *my* easy comprehension.

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

This can be done by own code or using dedicated packages like pizza.py.    
Example [Link](http://lammps.sandia.gov/doc/99/data_format.html)  
  
#### fix `bond/create` command

```
fix ID group-ID bond/create Nevery itype jtype Rmin bondtype keyword values 
```
* Nevery = attempt bond creation every this many steps
* itype,jtype = atoms of itype can bond to atoms of jtype
* Rmin = 2 atoms separated by less than Rmin can bond (distance units)
* bondtype = type of created bonds

zero or more keyword/value pairs may be appended to args
* keyword = iparam or jparam or prob or atype or dtype or itype

	* i/j-param values = maxbond, newtype
    	* maxbond = max # of bonds of bondtype the i/j-type atom can have
  		* newtype = change the i/j-type atom to this type when maxbonds exist
	* prob values = fraction seed
  		* fraction = create a bond with this probability if otherwise eligible
  		* seed = random number seed (positive integer)
	* atype value = angletype
  		* angletype = type of created angles
	* dtype value = dihedraltype
  		* dihedraltype = type of created dihedrals
	* itype value = impropertype
  		* impropertype = type of created impropers

*Examples*
```
fix 5 all bond/create 10 1 2 0.8 1
fix 5 all bond/create 1 3 3 0.8 1 prob 0.5 85784 iparam 2 3
fix 5 all bond/create 1 3 3 0.8 1 prob 0.5 85784 iparam 2 3 atype 1 dtype 2
```
*Description*

Create bonds between pairs of atoms as a simulation runs according to specified criteria. This can be used to model cross-linking of polymers, the formation of a percolation network, etc. In this context, a bond means an interaction between a pair of atoms computed by the bond_style command. Once the bond is created it will be permanently in place. Optionally, the creation of a bond can also create angle, dihedral, and improper interactions that bond is part of. 

#### The underlying principle

#### Setting up the force field 
#### Pair potential set up:
* `pair_style lj/cut rc`
Means set up a LJ potential between pairs and put a cutoff at $r_c*\sigma$ distance. The potential is of the form  
$E=4\epsilon\(\frac{\sigma}{r^{12}}-\frac{\sigma}{r^6})$.
* `pair_coeff * * 1 1 rc`  
Means change the pair potential parameters $\epsilon=1$ and $\sigma=1$. Also change the cutoff to $r_c$.  
* `pair_modify shift yes`
Means now shift the potential so that the value at $r_c$ becomes 0. After the 2 changes above the pair potential should become:   
$E=4\(\frac{1}{r^{12}}-\frac{1}{r^6}\)-4\(\frac{1}{r_c^{12}}-\frac{1}{r_c^6}\)$  
If you set $r_c=\sqrt[6]{2}$, then the minima of the potential with value -1 will be shifted upwards by 1, and the minima
will now be 0. So this has now become a purely repulsive truncated shifted Lennard-Jones potential.

#### LAMMPS units 

#### Running the simulation  
* [`fix nve/limit`](http://lammps.sandia.gov/doc/fix_nve_limit.html)  
`fix ID group-ID nve/limit xmax`
xmax = maximum distance an atom can move in one timestep (distance units)  

*Example*
`fix 1 all nve/limit 0.1`

*Description*

Perform constant NVE updates of position and velocity for atoms in the group each timestep. NVE means update is done in microcanonical ensemble. A limit is imposed on the maximum distance an atom can move in one timestep. This is useful when starting a simulation with a configuration containing highly overlapped atoms. Normally this would generate huge forces which would blow atoms out of the simulation box, causing LAMMPS to stop with an error.

* [`fix langevin`](http://lammps.sandia.gov/doc/fix_langevin.html)
* `fix ID group-ID langevin Tstart Tstop damp seed keyword values ...  `
ID, group-ID are documented in fix command  
langevin = style name of this fix command  
Tstart,Tstop = desired temperature at start/end of run (temperature units)  
Tstart can be a variable (see below)  
damp = damping parameter (time units)  
seed = random number seed to use for white noise (positive integer)  
zero or more keyword/value pairs may be appended  
keyword = angmom or omega or scale or tally or zero  
*Example*
`fix 3 boundary langevin 1.0 1.0 1000.0 699483`
Apply a Langevin thermostat as described in (Schneider) to a group of atoms which models an interaction with a background implicit solvent. Used with fix nve, this command performs Brownian dynamics (BD), since the total force on each atom will have the form:

F = Fc + Ff + Fr
Ff = - (m / damp) v
Fr is proportional to sqrt(Kb T m / (dt damp))
Fc is the conservative force computed via the usual inter-particle interactions (pair_style, bond_style, etc).

The Ff and Fr terms are added by this fix on a per-particle basis. See the pair_style dpd/tstat command for a thermostatting option that adds similar terms on a pairwise basis to pairs of interacting particles.

Ff is a frictional drag or viscous damping term proportional to the particle’s velocity. The proportionality constant for each atom is computed as m/damp, where m is the mass of the particle and damp is the damping factor specified by the user.

Fr is a force due to solvent atoms at a temperature T randomly bumping into the particle. As derived from the fluctuation/dissipation theorem, its magnitude as shown above is proportional to sqrt(Kb T m / dt damp), where Kb is the Boltzmann constant, T is the desired temperature, m is the mass of the particle, dt is the timestep size, and damp is the damping factor. Random numbers are used to randomize the direction and magnitude of this force as described in (Dunweg), where a uniform random number is used (instead of a Gaussian random number) for speed.

Note that unless you use the omega or angmom keywords, the thermostat effect of this fix is applied to only the translational degrees of freedom for the particles, which is an important consideration for finite-size particles, which have rotational degrees of freedom, are being thermostatted. The translational degrees of freedom can also have a bias velocity removed from them before thermostatting takes place; see the description below.


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
