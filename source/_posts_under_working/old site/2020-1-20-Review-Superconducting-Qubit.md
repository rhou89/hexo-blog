---
layout: post
title: Review of superconducting qubits for quantum engineers (Updating)
date: 2020-1-20 11:20:00
tags: QI SC-Qubit
categories: QuanCom AMO
author: ryan

---
Last Update: 3 Feb 2020

Right now, superconducting qubit is probably the mostly practiced physical platform for quantum computers and thus, I think it would be nice to write an introductory, yet comprehensive note to grab the most essentials of superconducting qubit. Hopefully, I could make this a series note covering trapped ion, which is used mainly for quantum simulation, as well as neutral atoms, which provides a relatively scalable platform.

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

## Introduction
Quantum bit (Qubit), as a quantum counterpart of classical bit, is the building block of quantum computers, judging by its name. If we follow the binary convention in classical computer, qubit is nothing but a gapped two-level quantum system (in principle, a $d$-level system is feasible). Two-level system is ubiquitous in quantum mechanics and many physical degrees of freedom like spin or hyperfine state can be utilized to engineer a qubit.  Nevertheless, to build a universal quantum computer, the candidate system has to be of controllability, tunability and accessibility. So far, there're ton of systems have been used to build or simulate quantum-computing platforms, e.g., [quantum dots](https://en.wikipedia.org/wiki/Quantum_dot), [trapped ions](https://en.wikipedia.org/wiki/Ion_trap), [ultracold atoms](https://en.wikipedia.org/wiki/Ultracold_atom), [NV center](https://en.wikipedia.org/wiki/Nitrogen-vacancy_center) and [polarized photon](https://en.wikipedia.org/wiki/Photon_polarization). 

So far, the most commonly practised platform would be the superconducting qubit, which is also the main topic of this note. If I have time, I'll also prepare notes on both trapped ion and cold atoms. I'm less familiar with NV center, but you can check out this [paper]( https://doi.org/10.1557/mrs.2013.20) if you're interested. Finally, photons are so far mainly used for the purpose of quantum communication, instead of computing.

## Superconducting circuits
### Superconducting qubit from quantum LC circuit
With such a title, you may wonder how a circuit could be a qubit since a qubit is a two-level system? The answer's simple as we take the ground state and the first excited state of the circuit to form a two-level system. To proceed, we first revisit classical [LC circuit](https://en.wikipedia.org/wiki/LC_circuit).
#### Classical LC circuit and harmonic oscialltor
The following figure (from [Wiki](https://upload.wikimedia.org/wikipedia/commons/b/b2/LC_parallel_simple.svg)) demonstrates a LC circuit, where "L" and "C" denote inductor and capacitor respectively. It common to refer the electric/magnetic energy stored in the circuit as "kinetic"(capacitor)/"magnetic"(inductor) energy.
<amp-img src="https://upload.wikimedia.org/wikipedia/commons/b/b2/LC_parallel_simple.svg" width="300" height="200" alt="" class="mb3"></amp-img>
If you know some basics of electromagnetism, it won't be hard to recall that the energy associated with the capacitor and inductor are $\frac{1}{2}C\dot{\Phi}^2$ and $\frac{1}{2L}\Phi^2$, where $\Phi=\int V(t)dt$ is the "magnetic" flux defined as integral of voltage $V(t)$. By definition, the Lagrangian is $\mathcal{L}=\frac{1}{2}C\dot{\Phi}^2-\frac{1}{2L}\Phi^2$. Through [Legendre transformation](https://en.wikipedia.org/wiki/Legendre_transformation), we have $H=Q\dot{\Phi}-\mathcal{L}=\frac{1}{2}CV^2+\frac{1}{2}LI^2$, where $Q=\frac{\partial\mathcal{L}}{\partial\dot{\Phi}}$ is the conjugate variable of $\Phi$. We immediately realize that such a Hamiltonian micmics that of a [harmonic oscillator](https://en.wikipedia.org/wiki/Harmonic_oscillator) $H=\frac{1}{2}mv^2+\frac{1}{2}kx^2$.

Recall that a [quantum harmonic oscillator](https://en.wikipedia.org/wiki/Quantum_harmonic_oscillator) has discrete energy level $\hbar\omega(n+1/2)$, we would have a well-defined $d$-level system now. The remaining step is to promote the LC circuit to its quantum version!
### Transmon qubit in Josephson qubit circuit
There are mainly three different archetypes of superconducting qubit, namely, charge qubit, flux qubit and phase qubit. All of them involves a structure called [Josephson junction](https://en.wikipedia.org/wiki/Josephson_effect), in which a insulator is sandwiched by two superconductors. Such a quantum-mechanic device works because the quantum tunneling allows Cooper pairs (electron pairs in conventional low-temperature superconductors) to "travel" between the two superconductors. Here, we study a so-called "transmon" qubit, which can be considered as an improved version of the charge qubit so that it is no longer sensitive to charge noise (the fluctuation of Cooper pairs).

To image a Josephson qubit circuit, you may replace the inductor in the classical LC circuit with a Josephson junction so that the Hamiltonian is similar. Now, we rewrite the flux $\phi=2\pi\Phi/\Phi_0$ in the unit of a magnetic flux quantum $\Phi_0=h/2e$ and define the Cooper pair number $n=Q/2e$ so that the total Hamiltonian now becomes $H=4E_Cn^2+\frac{1}{2}E_L\phi^2$, where $E_C=e^2/2C$ is charging energy and $E_L=(\Phi_0/2\pi)^2/L$ is inductive energy. The charging energy basically specifies the energy required to add a Cooper pair into the Josephson junction island. Would such a system serves as a good qubit? The answer is no! Because in this case, we will have many equally spaced energy levels. This means that whenever a try to couple the ground state with 1st excited state, higher states will be involved.

Luckily, this issue does not really exist in real life because Josephson junction has a non-linear inductance. Its potential energy shows a period with respect to $\phi$. In fact, the Hamiltonian should be something like $H=4E_Cn^2-E_J\cos(\phi)$. Note that, once expanded around $\phi_0$, the Hamiltonian returns to the quantum harmonic oscillator if only leading order is kept. That is to say, when $E_J\gg E_C$, the potential energy becomes dominate. The level spacing is no longer even (less spacing in high excited states) and the system is robust to charge noise. Such a system thus realizes a transmon qubit. Oppositely, in the region $E_J\approx E_C$, we call it the Cooper-pair box charge qubit, which is not of interests here.

Technically, the energy spacing between the ground state and 1st excited state (the qubit energy) $\omega_q=(\sqrt{8E_CE_J}-E_C)/\hbar$ is generally a few GHz (3~6 GHz). This means that the current qubits are generally manipulated through microwave. If we look at the energy different between 1st and 2nd states, it is usually a few hundred MHz (100~300 MHz) smaller than $\omega_q$. If we keep only 1st excited state, the effective Hamiltonian becomes $\frac{1}{2}\omega_q\sigma_z$, which is a simple two-level system we need.

### Reference
- [A Quantum Engineer's Guide to Superconducting Qubits](https://arxiv.org/abs/1904.06560v2)
- [Superconducting quantum computing - Wiki](https://en.wikipedia.org/wiki/Superconducting_quantum_computing)
- [Transmon - Wiki](https://en.wikipedia.org/wiki/Transmon)
- [Superconducting Qubits and the Physics ofJosephson Junctions](https://web.physics.ucsb.edu/~martinisgroup/classnotes/finland/LesHouchesJunctionPhysics.pdf)
- [JOSEPHSON QUBIT CIRCUITSAND THEIR READOUT](http://qulab.eng.yale.edu/documents/talks/Devoret-APS_Tutorial_090316s.pdf)
