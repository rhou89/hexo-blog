title: Grover Search as a Naturally Occurring Phenomenon
cover: 
thumbnail: 
date: 2020-5-5
tags:
- Physics
- Quantum Computing
- Study
categories:
- [Physics, AMO Physics]
- [Physics, Quantum Computing]
- [Computer Science, Quantum Computing]
---

A few days ago, when I was browsing papers [recently accepted by Phys. Rev. Lett.](https://journals.aps.org/prl/accepted) I noticed an interesting article [Grover Search as a Naturally Occurring Phenomenon](https://doi.org/10.1103/PhysRevLett.124.180501), which has just been published online today. I found this work really very fascinating, so I write this short note describing the work.

<!-- more -->

## A short summary
The idea is quite simple. The authors have studied a single-particle discrete-time [Quantum walk](https://en.wikipedia.org/wiki/Quantum_walk) (QW) on certain lattice geometry and find that the particle tends to localize around the topological defects in $O(\sqrt{N})$ steps with a probability $O(1/log~N)$. If you are familiar with the [Grover's algorithm](https://en.wikipedia.org/wiki/Grover%27s_algorithm) and consider the problem as the single particle searching for the defects on a large library of lattice sites, it looks like the fermion is doing Grover's search! Two things are extremely important here:

1. In Grover's algorithm, the oracle, or the so-called diffusion operator, is repeated $O(\sqrt{N})$ time. However, the free-propagating particle on the lattice knows nothing about the oracle!

2. While a successful demonstration of Grover's algorithm on a quantum computer (beating classical limits) is not possible right now, can we turn the way around and use the QW to simulate a Grover search in a gigantic database?

## Results
In this work, the authors have focused on a class of QW called Dirac QW in a 2D square or triangle lattice. While the lattice geometry is not essential here, the Dirac QW means that the QW can be effectively described by the Dirac Hamiltonian $$p_x\sigma_x+p_y\sigma_y+m_z\sigma_z$$, where $\sigma_i$ denotes Pauli matrices. The defect studied in this work is mainly vacancy, namely, there are few sites missing in the lattice.

With the above preliminaries, the quantum dynamics can be simulated with any given initial state. The authors prepare the initial state with a uniform distribution on both real and spin space. The author first measure the probability distribution around a defect with radius 2 and find it a periodic function over time. This is also a characteristic feature of Grover's algorithm. The authors then carefully measure the scaling of time and localization probability to $N$, which are consistent with that of Grover's algorithm.

### Discussions
Finally, the author also throws a profound question: while QW can be linked to both Grover's algorithm and Dirac fermions, does this suggest that the Dirac fermion can really perform Grover' algorithm naturally? My personal wondering is that, if so, does this suggest that Nature computes in a quantum-computing way as we do now?

## Reference
- [Grover Search as a Naturally Occurring Phenomenon](https://doi.org/10.1103/PhysRevLett.124.180501)
- [Grover's algorithm](https://en.wikipedia.org/wiki/Grover%27s_algorithm)
- [Quantum walk](https://en.wikipedia.org/wiki/Quantum_walk)