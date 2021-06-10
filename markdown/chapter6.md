# Applications and Limitations

## Applications

### Continuous control data

CHON simulates the continuous movement of particles, so the most obvious mapping of this system is to continuous control data. A continuous control signal is a constant stream of values that are relatively fine-grained. This is the default situation in CHON. The OSC data is sent out in a continuous stream at 60 frames per second, reporting the displacements of each particle in the x, y, and z directions. The additive synthesis engine in CHON also uses this data to modulate its FM and AM parameters.

When CHON is set to only have one particle, the movement of that particle is strictly sinusoidal. In this configuration, the signal that CHON generates resembles a very common control signal in electronic music: the LFO. An LFO (low frequency oscillator) is a continuous signal that modulates a parameter of sound synthesis or sound processing. LFOs come in various wave shapes, but the basic case is a sinusoidal LFO. Composers of electronic music often have dozens of independent LFOs controlling various parameters in their digital audio workstation. One way to think of CHON is to imagine a group of LFOs that are not independent. Instead, they push and pull on one another, creating a physical connection between modulating parameters.

Mapping the continuous displacement of particles in CHON presents many possibilities. Some basic synthesis options are included in the internal audio engine of CHON, as described in chapter 4. Pairing the OSC output of CHON with a digital audio workstation, one could map the displacement of each particle to the panning or volume of various tracks. CHON could also control audio processing parameters on each track such as filter frequency, reverb wet/dry signal, pitch shift, distortion/saturation level, and others.

CHON can also be treated as a module on a modular synthesis rack. A physical module that translates OSC data into control voltage such as 2.4SINK by Instrument of Things, or the WiFiMIDI from SDS Digital can enable CHON to gain control over an entire modular synthesis patch. Of course a simpler, and much less expensive, version of this is to use the software modular synthesis application VCVRack. One capable virtual module for this purpose in VCVRack is TrowaSoft's cvOSCcv. Using this module, and its extensions the user can send dozens of control signals from CHON all over a virtual patch. The possibilities are endless.

### Trigger control data

In some cases, it does not make sense to use continuous control data. There are various ways to take the continuous data from CHON and extract discrete trigger data. Unlike continuous data, trigger control data only causes a change in the target parameter at a moment in time, when a condition "triggers". This is a boolean logic. The trigger signal sends a constant value of 0 until the condition is met, at which time it sends a single 1, which can trigger an event.

This is how the Bell synth in the internal synthesis engine of CHON works. When a particle crosses its equilibrium point, it triggers the bell sound, which decays on its own according to its ADSR envelope. Each particle has 3 equilibrium points, since it can move in up to 3-dimensions. CHON can cause triggers when a particle crosses its x, y, and z equilibrium points, respectively. 

### Generating musical scores

CHON can also be used to write instrumental music. In Summer of 2020, Hocket, an LA-based piano duo, put out a call for very short compositions of 1 minute or less. I took the opportunity to make a first attempt at composing a piece of music using CHON. The result is the 45-second miniature piece called *Pandæmonium*. 

I set up a 4-particle system in CHON and sent the OSC output to an algorithmic music composition tool called SCAMP created by Marc Evanstein[@evanstein_scampsuite_2019]. I configured SCAMP to interpret the OSC data as the contour of a unique arpeggio for each hand. Each of the 4 particles dictated the movement of one hand of the performers, so that the movement of the performers hands to the right and left of the keyboard would reflect the movement of the particles from right to left in CHON. The displacement data of each particle was quantized to a different scale.

I decided that the entire piece would be one single gesture. I set CHON into motion and configured the damping effect so that the particles would come to rest after about one minute. The result is like a sonic explosion that gradually dissipates while each arpeggio pushes and pulls on one another.

## Limitations

CHON is designed to simulate many configurations of one particular kind of physical system: a network of coupled harmonic oscillators. While this is a fundamental model in theoretical physics, it is not well-suited to every application.

CHON is not meant to be a scheme for physical modeling synthesis, but rather a control signal scheme for shaping musical parameters using physically plausible interactions. Rather than an innovation in physical modeling synthesis, I consider CHON to be an innovation on the traditional LFO (Low Frequency Oscillator) model. Nonetheless, CHON does employ physical modeling for musical purposes, and so we can look to prior research for evaluating these types of systems.

Castagné and Cadoz have conceptualized a convenient framework to evaluate Physical Modeling schemes for musical applications[@castagne_10_2003]. Under this framework, CHON scores well in criteria *PM1* (efficiency -- CHON is efficient enough to achieve its goal of real-time interactive simulation of up to 100 particles), *PM4* (extra-sonic applications -- CHON can provide control signals for any medium), *PM5* (robustness of "plausibility" -- a complete novice can make plausible musical gestures with CHON), *PM6* (modularity -- CHON is highly modular in its applications thanks to its OSC functionality), *PM7* (intuitiveness of mental model -- CHON's behavior is predictable even to a non-physicist, with room for surprise and discovery), *PM8* (deepness of model -- CHON simulates a fundamental physical system), *PM10* (user-friendly interface - CHON is highly accessible to non-specialists).

![\small Criteria for evaluating physical modeling schemes[@castagne_10_2003]. \label{PMcriteria}](figures/PMcriteria.png)

*PM2* (faithfulness of reproduced sound), *PM3* (diversity of simulated instruments), and *PM9* (existence of generation algorithms) are mostly irrelevant to the goals of CHON. However, the Euler Method, which is used in CHON to calculate the movement of the particles, is known to have a margin of error proportional to the framerate of the simulation. Therefore if *PM2* is taken to mean more generally "how well does the scheme fit to physical reality," then the scheme that CHON employs is not the most precise when compared to others.

CHON can simulate a complex system with many moving parts. The motion of an individual particle in CHON may be difficult to predict, but it is not random. When set in motion and left alone, CHON is deterministic (non-linearities can be introduced by user-interaction). CHON is not suited for random signal generation or chance music. The movement of a particle in CHON may appear complicated, but it also has an intuitive tangibility thanks to its physical basis.
 
Some systems, such as the CORDIS-ANIMA software[@cadoz_cordis-anima_1993], go far beyond CHON in terms of flexibility, allowing the user to construct systems of thousands of particles and define parameters for each one. CHON is limited to 100 particles in a 1D or 2D configuration. This limitation in physical configuration is a deliberate choice to make CHON easier to use. I determined that 100 parameter control signals is sufficient for the vast majority of use-cases.

The problem of parameter mapping is an important and sometimes difficult one in algorithmic composition. CHON's internal sound engine provides three examples of mapping its control signals to synthesis parameters. However, when broadcasting OSC signals from CHON to an external application, two problems become apparent. The first thing one will likely notice is the challenge of deciding to which parameter the control signals should be attached. The possibilities are practically limitless and it may take some serious experimentation and imagination to find the most compelling configurations. The second challenge is that setting up a high number of OSC connections can become quite tedious. This isn't exactly a problem with CHON in and of itself; CHON automatically sends out OSC data with the click of a button. Nonetheless, the daunting task of manually configuring 50 or 100 parameters in your DAW to accept the OSC data from CHON may present a barrier to some of the more elaborate setups.

