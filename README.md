# BdG-ML
This project aims to optimize the computational time of superconductivity simulations using the Bogoliubov–de Gennes (BdG) and Machine Learning(ML) methods.





# Introduction
Mean-field or self-consistent approximations are commonly performed in numerous areas of statistical physics that involve interactions among multiple agents, such as magnetism \cite{magnetism}, epidemic models \cite{epidemia}, and superconductivity \cite{supercondutividade}. These approximations are useful in determining numerical values for order parameters in phase transitions of these systems. This method involves approximating these interactions by the average contributions of the agents (degrees of freedom), disregarding terms that are smaller than the fluctuations associated with these averages. However, this formalism \textbf{always} implies solving self-consistent (implicit) equations for the order parameter, which often have numerical solutions with very high computational time and storage requirements.

Therefore, this work aims to reduce the computational time of these solutions and, consequently, enable the exploration of more complex systems with higher dimensions. To achieve this, the Bogoliubov–de Gennes (BdG) equations for superconductivity were chosen, and machine learning methods were selected to solve the problem of finding the superconducting gap ($\Delta$).


# Equations

In continuous space, the BdG equation is represented as follows:
$$\Delta = \lambda \int_{-Ec}^{Ec} \Delta \frac{tanh(\frac {\sqrt{\xi^2 + |\Delta|^2}}{2K_{b}T})}{2\sqrt{\xi^2 + |\Delta|^2}}d\xi $$

In discrete space, a Hamiltonian representing a one-dimensional chain with nearest-neighbor hopping and periodic boundary conditions was chosen:

$$ H = \sum_{<i,j>} t_{ij} c^{\dag}{i} c{j} + \sum_{<i, j>} \Delta_{ij}c^{\dag}{i} c^{\dag}{j} + \sum_{<i, j>} \Delta_{ij} c_{i} c_{j}$$

# Idea 


Considering the problem and the mentioned computational complexities, one might wonder: could a machine learn the patterns existing in the determination of $\Delta$ and find a function $f$ such that $\Delta \gets f(T, V, N, E_{c}, \text{etc})$? By using only the physical parameters that determine the system, it would be possible to optimize the computational time.

To accomplish this, Random Forests were considered due to their low computational complexity and the low dimensionality of the physical parameters. The idea is to improve the initial guess for $\Delta$, which is usually random. The machine would then learn this pattern and provide a guess closer to the correct value, thus optimizing the computational time.
