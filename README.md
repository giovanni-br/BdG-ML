# BdG-ML
This project aims to optimize the computational time of superconductivity simulations using the Bogoliubov–de Gennes (BdG) and Machine Learning(ML) methods.





# Introduction
Mean-field or self-consistent approximations are commonly performed in numerous areas of statistical physics that involve interactions among multiple agents, such as magnetism \cite{magnetism}, epidemic models \cite{epidemia}, and superconductivity \cite{supercondutividade}. These approximations are useful in determining numerical values for order parameters in phase transitions of these systems. This method involves approximating these interactions by the average contributions of the agents (degrees of freedom), disregarding terms that are smaller than the fluctuations associated with these averages. However, this formalism \textbf{always} implies solving self-consistent (implicit) equations for the order parameter, which often have numerical solutions with very high computational time and storage requirements.

Therefore, this work aims to reduce the computational time of these solutions and, consequently, enable the exploration of more complex systems with higher dimensions. To achieve this, the Bogoliubov–de Gennes (BdG) equations for superconductivity were chosen, and machine learning methods were selected to solve the problem of finding the superconducting gap ($\Delta$).


# Equations

In continuous space, the BdG equation is represented as follows:
$$\Delta = \lambda \int_{-Ec}^{Ec} \Delta \frac{tanh(\frac {\sqrt{\xi^2 + |\Delta|^2}}{2K_{b}T})}{2\sqrt{\xi^2 + |\Delta|^2}}d\xi $$

In discrete space, a Hamiltonian representing a one-dimensional chain with nearest-neighbor hopping and periodic boundary conditions was chosen:

$$ H = \sum_{{\langle i,j \rangle}} t_{ij} c_{i}^{\dagger} c_{j} + \sum_{{\langle i,j \rangle}} \Delta_{ij}c_{i}^{\dagger} c_{j}^{\dagger} + \sum_{{\langle i,j \rangle}} \Delta_{ij} c_{i} c_{j}$$

After that, we implemented a spin model for the same system, with periodic and non-periodic boundary conditions:

$$ H = \sum_{{\langle i,j \rangle}} \sum_{{\sigma=\uparrow,\downarrow}}  t_{ij} c_{{i\sigma}}^{\dagger}c_{{j\sigma}} + \sum_{i=1}^N \left[\Delta_{i}c_{i\uparrow}^{\dagger} c_{i\downarrow}^{\dagger} +\Delta_{i}^*c_{i\downarrow} c_{i\uparrow}\right ]$$


# Idea 

Considering the problem and the mentioned computational complexities, one might wonder: could a machine learn the patterns existing in the determination of $\Delta$ and find a function $f$ such that $\Delta \gets f(T, V, N, E_{c}, \text{etc})$? By using only the physical parameters that determine the system, it would be possible to optimize the computational time.

To accomplish this, Random Forests were considered due to their low computational complexity and the low dimensionality of the physical parameters. The idea is to improve the initial guess for $\Delta$, which is usually random. The machine would then learn this pattern and provide a guess closer to the correct value, thus optimizing the computational time.


# Preliminary results
* For the equation in continuous space, and the first Hamiltonian, it was possible to compute the $\Delta$ **two times faster!**
* We believe this optimization could be improved, once the complexity of Random Forests for example goes with $\mathcal{O}(D.T)$, in which $D$ is the length of the tree and $T$ is the number of trees, while the conventional method goes with  $\mathcal{O}(n^3)$, where n is number of sites.
* **New physical behaviors** were possibly found for conditions where $V \approx t$. Possible unusual phase transitions of the order parameter, in bulk, and on the edge.

<p align="center">
  <img src="https://github.com/giovanni-br/BdG-ML/blob/main/gap_gif_nonperiodic_spin.gif" alt="animated" />
</p>

