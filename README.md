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

Here we borrow the Hamiltonian from [paper](https://arxiv.org/pdf/2102.12556.pdf?fbclid=IwAR2tZhjENa6-5z-XVVKu4VEPcE05QslG6C4XifwfqrPfNmiFzuoe97Sm5tA) with the their redefined value as our base model. Our job then is just simulate the Hamiltonian from the model.

## 3. Applying QAOA to achieve Hamiltonian 
(Interested reader might find detailed notes in .ipynb file helpful)
<img src="https://render.githubusercontent.com/render/math?math=">

The Hamiltonian that characterizes the system of $N$ interacting neutrinos (each represented by a qubit) is given by

![a](https://latex.codecogs.com/svg.latex?\Large&space;H=\sum_{k=1}^N\overrightarrow{b}\cdot\overrightarrow{\sigma_k}+\sum_{p<q}^NJ_{pq}\overrightarrow{\sigma_p}\cdot\overrightarrow{\sigma_q})

with the external field <img src="https://render.githubusercontent.com/render/math?math=\overrightarrow{b}%20=%20(b^x,b^y,b^z)%20=%20\left(\sqrt{1-0.925^2},%200,%20-0.925\right)"> and the pair coupling matrix <img src="https://render.githubusercontent.com/render/math?math=J_{pq}%20=%201%20-%20\cos(\theta_{pq})">, where <img src="https://render.githubusercontent.com/render/math?math=\theta_{pq}%20=%20\arccos(0.9)%20\frac{|p-q|}{N-1}">.

We trotterize the induced time evolution as
<img src="https://render.githubusercontent.com/render/math?math=e^{-iHt}=\prod_{i=1}^ne^{-iA_1\alpha_it}e^{-iA_2\beta_it}e^{-iA_3\gamma_it}e^{-iB_1\delta_it}e^{-iB_2\epsilon_it}e^{-iB_3\kappa_it}">, where

<p align="center">
<img src="https://latex.codecogs.com/svg.image?\begin{align}A_1%20&=%20\sum_{k=1}^N%20b^x%20\sigma_k^x,%20&A_2%20&=%20\sum_{k=1}^N%20b^y%20\sigma_k^y,%20&A_3%20&=%20\sum_{k=1}^N%20b^z%20\sigma_k^z,%20\notag\\B_1%20&=%20\sum_{p%3Cq}^N%20J_{pq}%20\sigma_p^x%20\sigma_q^x,%20&B_2%20&=%20\sum_{p%3Cq}^N%20J_{pq}%20\sigma_p^y%20\sigma_q^y,%20&B_3%20&=%20\sum_{p%3Cq}^N%20J_{pq}%20\sigma_p^z%20\sigma_q^z.%20\notag\end{align}">
</p>
 
Those unitaries can be implemented by a sequence single- and two-qubit rotation gates. In particular,
<p align="center">
<img src="https://render.githubusercontent.com/render/math?math=\begin{align}e^{-iA_1\alpha_it}=\prod_{k=1}^N\text{RX}_k(2\alpha_it)\notag\\e^{-iA_2\beta_it}=\prod_{k=1}^N\text{RY}_k(2\beta_it)\notag\\e^{-iA_3\gamma_it}=\prod_{k=1}^N\text{RZ}_k(2\gamma_it)\notag\\e^{-iB_1\delta_i}=\prod_{p<q}^N\text{RXX}_k(2J_{pq}\delta_it)\notag\\e^{-iB_1\epsilon_i}=\prod_{p<q}^N\text{RYY}_k(2J_{pq}\epsilon_it)\notag\\e^{-iB_1\delta_i}=\prod_{p<q}^N\text{RXX}_k(2J_{pq}\kappa_it)\notag\end{align}">
</p>
  

## 4. Result
(See the notebook for detailed settings)
### Experiment 1: 2 qubits - 1 layer - Time length of 1
![Exp1_Noiseless](/figures/exp1_noiseless.png "Noiseless")
![Exp1_Noisy](/figures/exp1_noisy.png "Noisy")

### Experiment 2: 3 qubits - 2 layers - Time length of 2
![Exp2_Noiseless](/figures/exp2_noiseless.png "Noiseless")
![Exp2_Noisy](/figures/exp2_noisy.png "Noisy")

### Experiment 3: 4 qubits - 4 layers - Time length of 3
![Exp3_Noiseless](/figures/exp3_noiseless.png "Noiseless")

### Experiment 4: 4 qubits - 4 layers - Time length from 1 to 6
![Exp4_Noiseless](/figures/exp4.png "exp4")

## About us
[Trong Duong Dinh](https://github.com/MyEntangled)- Korea Advanced Institute of Science and Technology, Year 3

[Bao Bach Gia](https://github.com/bachbao) - Ho Chi Minh University of Technology, Year 3 
