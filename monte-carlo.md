## Monte Carlo without equations
* Aim : explain monte carlo using sentences, no equations.
* Content source : [Daan Frenkel, Understanding MD Simulation](https://books.google.fr/books?id=5qTzldS9ROIC&lpg=PP1&pg=PP1#v=onepage&q&f=false) and [Computer Simulation of Liquids, Second Edition by Allen P., Tildesley J. ](https://books.google.fr/books?id=WFExDwAAQBAJ&lpg=PP1&dq=Computer%20Simulation%20of%20Liquids&pg=PP1#v=onepage&q=Computer%20Simulation%20of%20Liquids&f=false) 
## Motivation
Monte Carlo is a place in Italy famous for its casinos/gambling?. 
Monte Carlo method was first developed by von Neumann, Ulam and Metropolis at the end of 2nd WW to study diffusion of neutrons in 
fissionable materials. Monte Carlo in simulation lingo assumes that repeated random sampling can provide approximate solutions. Randomness is associated with casinos also. Unless and until you cheat. Computationally random numbers can be used to cause fluctuations in particle postions to simulate particle motion. Approach towards MC problems is also the same. 

##### some side tracking
There are some cracked games that require us to move our cursor around a specified zone in the installation GUI, which the software uses as random seed for some purpose. Read more about that [here](https://security.stackexchange.com/a/10443).

## Definitions
We consider that we are in NVT. Read about [NVT](http://webcache.googleusercontent.com/search?q=cache:http://www.quimica.urv.es/~bo/MOLMOD/General/Dynamics/Ensembles.html&num=1&strip=1&vwsrc=0).
* Partition Function (Q)
This is a classical way to introduce the position, momenta and energies (Hamiltonian) of all the particles in a box.
* Hamiltonian (H)
This is another way to call the energies in the system. There will be contributions from Kinetic and Potential energies to this term. If we add up all the kinetic and potential enrgies in an isolated system of particles, then this will give the total energy, which is the Hamiltonian. 
* Need for numerical technique?
Lets imagine an observable (a measurable quantity) A, which a function of cordinates and momenta. As we know kinetic energy is itself written as the function of momenta. Since we have to integrate over all particle contribution to compute the kinetic energy, we can reasonably assume that analytical calculations for momenta can be done easily (since it is a quadratic function). But integrating over all the particle coordinates in the system can be difficult -- This begs for a numerical method. One such method is MC.

##### some side tracking
In 1952, Los Alamos Scientific Laboratory, under the supervison of von Neumann, made a computer called [MANIAC](https://books.google.fr/books/content?id=qB819m2ibUQC&pg=PA16&img=1&zoom=3&hl=en&sig=ACfU3U02fek1k2wyiALPu2ulFZNesNUQPQ&ci=50%2C210%2C882%2C1019&edge=0), which performed some the very first numerical analysis of the many-body problem.

## MC Integration
Configurational energy stored in a liquid can be computed in two ways:
A. Solve newtons equations of motion for the particles and average it over time
B. Find all configurations where the probablity of a particle being in a state is high and do an ensemble average
Both will lead to the same answer. This is called the [Ergodic Hypothesis](https://en.wikipedia.org/wiki/Ergodic_hypothesis).


[WIP]

## Future
Simpsons rule

### Other References
[1] https://math.dartmouth.edu/theses/undergrad/2014/Vaidyanathan-Thesis.pdf

[2] http://online_casino_news.hundredpercentgambling.com/2016/03/zero-margin-blackjack-randomness-test.html

[3] [Computing at LASL in the 1940s and 1950s](https://books.google.fr/books?id=qB819m2ibUQC&pg=PP1#v=onepage&q&f=false) 
