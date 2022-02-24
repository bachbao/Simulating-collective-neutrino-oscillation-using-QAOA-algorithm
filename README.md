# Simulating collective neutrino oscillation using QAOA algorithm

## 1. Introduction
In the out-of-equilibrium collective dynamics of a neutrino cloud with a high density of neutrinos, the existence of neutrino-neutrino interaction can trigger collective flavor oscillations. This phenomenon has not been profoundly understood due to the complication of solving for the real-time evolution of the strongly coupled many-body system. Nevertheless, scientists and researchers believe that by the use of quantum computers, we can gain a deeper insight into these kinds of phenomena. Here, we present a new way to simulate a small system - "two-flavor case" of interacting neutrinos using the IBMQ quantum devices.

The project aim is to demonstrate the time and space evolution of the set of amplitudes from a Schrodinger equation:

![a](https://latex.codecogs.com/svg.latex?\Large&space;|\phi(t)\rangle=e^{-iHt}|\phi_{0}\rangle) 


The H - Hamiltonian from the equation is the Hamiltonian for neutrino flavor evolution in an environment with high denisty of neutrinos which inlcude vacuum and forward-scattering interaction contributions. A direct solution of the
Schrodinger equation above, for a system of N configurations in energy and angle, incurs a computational
cost that is exponential in N which create a constraint to early explorations of the problem to systems with N = O(10)
neutrinos. However as stated above, quantum computers hold the promise to overcome these limitations, hence solve the full neutrino dynamics. In order to simulate the system on the current noisy, near-term quantum computers, we size down to small system with N = 4  neutrino amplitudes and use QAOA (Quantum Approximate Optimization Algorithm) introduced by Farhi et al to present this simulation. 

## 2. Spin model for neutrino oscillation
In our case, we are considering two-flavor case, therefore our system can be expressed as direction of momentum (denoted by q_i) and an amplitude for a neutrino of each energy E_i. The amplitudes that describe the being in the electron flavor or in a heavy (muon or tau) can be encoded in an SU(2) spinor basis. In this basis, the Hamiltonian can be written in terms of Pauli operators which can be charaterized as the sum of a one-body term, describing vacuum and forward scattering in matter and a two-body term, showing the neutrino-neutrino forward-scattering.

Here we lend our final Hamiltonian from [paper](https://arxiv.org/pdf/2102.12556.pdf?fbclid=IwAR2tZhjENa6-5z-XVVKu4VEPcE05QslG6C4XifwfqrPfNmiFzuoe97Sm5tA) with the their redefined value as our base model. Our job then is just simulate the Hamiltonian from the model.

## 3. Applying QAOA to achieve Hamiltonian

With the Hamiltionian above, we start analyses it to apply QAOA algorithm, 

## 4. Result
