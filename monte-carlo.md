## Monte Carlo without equations
* Aim : explain monte carlo using sentences, no equations.
* Content source : [Daan Frenkel, Understanding MD Simulation](https://books.google.fr/books?id=5qTzldS9ROIC&lpg=PP1&pg=PP1#v=onepage&q&f=false)

## Motivation
Monte Carlo is a place in Italy famous for its casinos.
Monte Carlo in simulation lingo assumes that random kicks act on particles in a box to simulate velocities.
Computationally these random numbers can be added to the postions using random number generators, which take a random seed as input.

##### some side tracking
There are some cracked games that require us to move our cursor around a specified zone in the installation GUI, which the software uses
as random seed for some purpose. Read more about that [here](https://security.stackexchange.com/a/10443).

## Definitions
Here we consider that we are in NVT. Read about [NVT](http://webcache.googleusercontent.com/search?q=cache:http://www.quimica.urv.es/~bo/MOLMOD/General/Dynamics/Ensembles.html&num=1&strip=1&vwsrc=0).
* Partition Function (Q)
This is a classical way to introduce the position, momenta and energies (Hamiltonian) of all the particles in a box.
* Hamiltonian (H)
This is another way to call the energies in the system. There will be contributions from Kinetic and Potential energies to this term. If we add up all the kinetic and potential enrgies in an isolated system of particles, then this will give the total energy, which is the Hamiltonian. 
* Need for numerical technique?
Lets imagine an observable (a measurable quantity) A, which a function of cordinates and momenta. As we know kinetic energy is itself written as the function of momenta. Since we have to integrate over all particle contribution to compute the kinetic energy, we can reasonably assume that analytical calculations for momenta can be done easily (since it is a quadratic function). But integrating over all the particle coordinates in the system can be difficult -- This begs for a numerical method. One such method is MC.

##### some side tracking
There is a famous musical called a Hamilton, which is a musical about the life of American Founding Father Alexander Hamilton, with music, lyrics and book by Lin-Manuel Miranda, inspired by the 2004 biography Alexander Hamilton by historian Ron Chernow.


## Future
Simpsons rule
