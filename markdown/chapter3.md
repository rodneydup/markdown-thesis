# Physics

CHON is built on the idea of generating musical material from a computer simulation of a real physical system. The system in question is that of coupled harmonic oscillators. A system of this kind is formed by connecting (coupling) two or more oscillating nodes (harmonic oscillators) via a spring-like force such that they exert a force on one another. The physics governing this system are that of classical mechanics. It can be completely described by the simple laws of motion posited by Isaac Newton in 1687 [@newton_newtons_1846], and by Hooke's Law [@hooke_potentia_1678].

I was inspired to create CHON when I saw two pendulums connected by springs oscillating in such a way that the two pendulums appeared to be, in a sense, passing an oscillation back and forth. see figure \ref{coupledPendulum}

![\small Coupled Pendulum - the amplitude of one pendulum's oscillation increases while the other decreases. Then, the process reverses. \label{coupledPendulum}](figures/coupledPendulum.pdf)

This was in fact a superposition of the two modes of oscillation of the system, but the appearance of an exchange of energy back and forth was what captivated me. I imagined sounds forcing each other into activity and contrapuntal structures in which sounds, instruments, and textures passed musical energy from one to another in a cascade of antiphony. In order to experiment with this kind of musical structure, I began working on CHON.

Before looking at coupled harmonic oscillator systems or networks, I will describe the case of a simple harmonic oscillator. A simple harmonic oscillator can be most simply represented by a mass or particle on a spring. There is a point of equilibrium for this mass where it will remain unless it is perturbed. If the mass is moved away from equilibrium, it will exert a force proportional to the displacement. If it is then released, it will move back toward equilibrium, pass it, and continue to oscillate at a fixed sinusoidal frequency (determined by the spring stiffness and the mass).

The behavior of springs (within elastic limits) is well described by Hooke's Law. Hooke's law can be stated as: the restoring force of a spring is linearly proportional to to its displacement. Mathematically:

$$F=-kx$$

Where $k$ is a constant "stiffness" of the spring, and $x$ is the displacement of the spring away from equilibrium. If the spring is at equilibrium, then the spring will not move unless acted upon by an external force. To stretch or compress the spring away from equilibrium by $x$, one would need to exert a force equal to the product of $k$ and $x$. The restoring force at that point $x$ will then be equal and opposite to this force. If the spring is released, it will accelerate toward equilibrium. Furthermore, provided the spring is not over-damped, the spring will be set into *harmonic motion*, meaning it's displacement will follow a sinusoidal curve. If the spring is not damped at all, this harmonic motion will continue at the same amplitude indefinitely.

![\small Simple Harmonic Oscillator - The restoring force is $F=-kx$. The motion is sinusoidal. \label{simpleHarmonicOscillator}](figures/simpleHarmonicOscillator.pdf)

Newton's laws of motion can also be useful in describing the simple harmonic oscillator, and they come into play in the software implementation of CHON. These laws state:

1) A body's velocity remains constant unless acted upon by an external force.
2) The force exerted on a body is the product of mass times acceleration.
3) A body will exert an equal and opposite force to any force exerted upon it.

These laws describe the vast majority of macroscopic objects that we are familiar with. Using these laws, one can predict and model many kinds of physical interactions between objects.

The first law is sometimes referred to as the "law of inertia." Aside from the way it is stated above, another way of positing it is that an object at rest will stay at rest and an object in motion will stay in motion. In a simple harmonic oscillator, the oscillating particle will not move from equilibrium until it is displaced by an external force. Once it is in motion, it will continue to be in motion unless a damping force is exerted on it.

The second law gives us the mathematical means to calculate important properties of an object in motion. Stated mathematically, it is:

$$F=ma$$

This equation, when combined with Hooke's law, can give us more information about a harmonic oscillator, such as its acceleration (which is especially important in the implementation of CHON). This can be shown by combining Hooke's equation with Newton's:

$$F=ma=-kx$$

And re-arranging to find our desired property:

$$ma=-kx$$
$$a=\frac{-kx}{m}$$

The second law also allows us to model the mass-spring problem by incorporating a mass term into the equation. We will continue to treat the mass of the spring itself as negligible.

The third law tells us that a body exerting a force on another body will experience a force of equal magnitude and opposite direction. This gives us a shortcut to calculate the forces of coupled harmonic oscillators in CHON, as I explain in chapter 4.

The frequency in Hz of the harmonic motion of a simple harmonic oscillator is determined by the spring stiffness $k$ and the mass of the object $m$.  It is given by the formula:

$$f=\frac{1}{2\pi}\sqrt \frac{k}{m}$$

So, the higher the spring tension, or the lower the mass, the faster the oscillation. Conversely, lower spring tension or higher mass results in slower oscillations.

Up to this point, we have not accounted for damping forces that cause the energy of a harmonic oscillator to dissipate over time. Damping forces come from several sources in the real world including air resistance, friction, and gravity. We can approximate the effects of these damping forces with a constant $b$. The damping effect is also a function of the velocity of the object. This term can be introduced into our combined newton-hooke equation above like so:

$$ma=-kx - bv$$

This new equation describes a *damped* harmonic oscillator. This can be thought of as a simple harmonic oscillator that loses its energy over time. The oscillation of the particle is now constrained by an envelope that decreases its amplitude over time.

If we add another particle to this system and affix both particles to a springs connected to unmoving anchors, and also connect the particles to each other via a third spring, we now have a basic coupled harmonic oscillator system. Now, each particle can experience a force from the spring attached to the anchor as well as the spring attached to the other particle. Each of these forces is a vector with a direction and magnitude. The addition of these vectors will give us the net force on the particle.

$$ \vec F_{net} = \vec F_1 + \vec F_2 $$

Substituting for hooke's law we get:

$$ \vec F_{net} = -kx_{anchor} + kx_{particle} $$

Previously, the displacement from equilibrium $x$ of the particle was determined relative to a fixed anchor. Now, one of the anchors is in motion. With this, we now have to take into account the displacement from equilibrium of both particles($x_1$ and $x_2$), the difference of which will determine our $x$.

$$ x_{particle} = x_2 - x_1 $$

And substituting into our previous equation:

$$ \vec F_{net} = -kx_{anchor} + k(x_{2} - x_1) $$

We can see that if the two particles move in sync with one another, there will be no force exerted between them, as the difference between their displacements will come out to zero.

![\small Coupled Harmonic Oscillator - The restoring force of each particle is a sum of two forces $\vec F_1$ and $\vec F_2$. \label{coupledHarmonicOscillator}](figures/coupledHarmonicOscillator.pdf)

With this simple two-particle system, there are now two frequencies of oscillation that can occur. These are called the modes of the system. The first mode can be seen when the two particles are in phase, or moving in the same direction at the same time. The second mode can be seen when the two particles are 180 degrees out of phase, moving in opposition to one another. Of course many other patterns of motion can arise depending on the phase relationship of the particles in oscillation, but all of these are really a superposition of the two modes. It is in this state of superposition that we see the "exchange of energy" characteristic of the coupled pendulum system that inspired CHON. The effect is more pronounced if the outside springs are stiffer than the spring connecting the two particles. The number of modes in the system is equal to the number of particles in the system.

![\small Modes - Left: Mode 1, Right: Mode 2 \label{modes}](figures/modes.pdf)

As particles are added to this system, it approaches a physical simulation of a string. This is the basis for the mass-spring method of string physical modeling (PM) synthesis. CHON bears a superficial resemblance to mass-spring PM synthesis, but their goals differ. PM synthesis utilizes the mass-spring method to simulate the displacement of a plucked string in order to generate a realistic string sound. In PM synthesis, each individual mass in the mass-spring system only matters inasmuch as it contributes to the overall string simulation. CHON uses a mass-spring system to simulate coupled particles and generate control data from each particle. The behavior of each individual particle is the central focus in CHON.

Another difference from a string simulation is that the particles of CHON can move in three dimensions. In a mass-spring string simulation, each mass moves only transversely (perpendicular to the length of the string). In CHON, the user can select the degrees of freedom. By default, the particles of CHON are constrained to move only longitudinally (in the x-axis). But the user can choose to allow the particles to move in the y-axis and z-axis as well, or in any combination of the three axes. The only change in the physics of this situation is that we now have to calculate $k(y_{2} - y_1)$ and $k(z_{2} - z_1)$ as well in our calculation of the net force on the particle.

In addition to laying out coupled harmonic oscillators in 1-dimension like a string, CHON can arrange particles in a 2-dimensional grid. This produces more complicated modal behavior and superpositions. As the number of particles increases in this grid, the simulation begins to resemble a membrane like a drumhead. In this configuration, each particle experiences forces from four neighboring particles.
