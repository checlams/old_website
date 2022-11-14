---
layout: distill
title: Data-Driven Computational Framework for Solving Complex PDEs
description: Facilitating numerical solution by incorporating physics 
img: assets/img/projects/richards.png

authors:
  - name: Zheyu Jiang
    affiliations:
      name: CLAMS @ OSU
  - name: Zeyuan Song
    affiliations:
      name: CLAMS @ OSU

bibliography: richards.bib

toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: FVM-based Discretization
  - name: Data-Driven Random Walk Algorithm
  - name: DRW Architecture

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

## Introduction

Many partial differential equations (PDEs) arise from transport phenomena involve a combination of first order conservation equations or second order PDEs that are as elliptic, parabolic, and hyperbolic. Many of these PDEs are highly nonlinear and very difficult to solve in practice. For example, the Richards equation, which captures irrigation, precipitation, evapotranspiration, runoff, and drainage mechanisms of water in porous medium such as soil, has the form:

$$
\begin{align*}
    &\partial_t\Theta(\psi)+\nabla \cdot \textbf{q} = 0,\\
    &\textbf{q} = -\textbf{K}(\Theta)\nabla (\psi+z)
\end{align*}
$$

In particular, variable $$\textbf{K}$$ denotes the unsaturated hydraulic water conductivity expression and is a highly nonlinear function, making the Richrads equation challenging to solve. Most existing PDE solvers are based on discretization approaches such as finite difference, finite element, and finite volume. However, for finite difference and finite element methods, we observe that, upon discretization, the useful physical information associated with the transport phenomena of the PDEs is typically not preserved. On the other hand, FVM adopts an integral form of the PDE, thereby preserving some of the useful physical insights. Unfortunately, even if the PDE of interest is discretized using FVM, the discretized equations are usually transformed into a matrix equation and solved numerically. Again, this solution process loses the physical insights. Therefore, our goal is to enhance the quality and performance of the solution process by developing a novel computational framework that explores and utilizes the underlying physics behind the PDEs derived from transport phenomena.

***

## Solution Strategy
To explore and incorporate additional useful physical insights to our algorithm, we introduce the concept of **random walk**, a stochastic process that describes the paths as $$N$$ particles or molecules move in random steps, to the FVM framework to model the particles' transport phenomena subject to external forces (e.g., gravity) and obstacles<d-cite key="song:2022:richards"></d-cite>. Such a concept has been used to solve partial differential equations with strong physical background, such as the heat<d-cite key="lawler2010random"></d-cite> and diffusion<d-cite key="sandev2018continuous"></d-cite> equations. In our case, we anticipate that the number of water molecules inside a unit volume of soil at any time is also a random process. With this, we can develop a systematic computational framework for solving the Richards equation effectively. Specifically, we use multi-layer neural network to learn a data-driven random walk model, which is then incorporated into a modified FVM scheme to obtain solutions of the Richards equation. Through an illustrative case study, we demonstrate the accuracy and effectiveness of our innovation solution framework and compare it with state-of-the-art numerical methods.

***

## FVM-based Discretization

FVM is a classic numerical method that incorporates conservation laws to allow volume integrals to be converted into surface integrals by applying the divergence theorem. Using the Richards equation as an example, we first integrate both sides of it to obtain the integral form of the Richards equation over a $$n+1$$-dimensional control volume $$V$$. Next, we apply the divergence theorem to convert the volume integral into a $$n$$-dimensional surface integral after determining the outward pointing unit normal vector $\textbf{n}$:

$$
\int_V  \partial_t\Theta(\psi)\mathbf{d}V=\int_V \nabla \cdot [\textbf{K}(\Theta)\nabla (\psi+z)]\mathbf{d}V
$$

To adopt the FVM, we discretize the control volume $$V$$ and its surface $$S_V$$ into $$N_{\omega}$$ small cells $$V_i$$ with $$i=1,\cdots, N_\omega$$, and small surfaces $$\omega$$ with volume $$A_\omega$$ with $$\omega=1,\cdots, N_\omega$$, respectively. Now, we discretize the integral equation by denoting the discretized version of the operator $$\textbf{K}(\cdot)\nabla (\cdot)$$ with respect to the small surface $$\omega$$ as $$[\textbf{K}(\cdot)\nabla (\cdot)]_\omega$$. 

The RHS of the integral equation can be discretized by summing over $$[\textbf{K}(\cdot)\nabla (\cdot)]_\omega$$ for all $$\omega$$:

$$
    \partial_t\Theta(\psi)\text{vol}(V_i)=\sum_{\omega=1}^{N_\omega} [\textbf{K}(\Theta)\nabla (\psi+z)]_\omega \cdot\textbf{n}_\omega A_\omega
$$

To apply time stepping on the LHS of the integral equation, we discretize the time domain and approximate the time derivative $$\partial_t\Theta(\psi_i)$$ as $$\frac{\Theta_i^{m+1,s+1}-\Theta_i^m}{\Delta t}$$, where $$\Theta_i^{m+1,s+1}$$ represents the discretized $$\Theta$$ in the $$i$$-th small cell at time step $$m+1$$ and iteration step $$s+1$$, and $$\Theta_i^m$$ is the converged $$\Theta$$ value in the $$i$$-th small cell at the current time step $$m$$. Overall, we have:

$$
    \frac{\Theta_i^{m+1,s+1}-\Theta_i^m}{\Delta t} \text{vol}(V_i)=\sum_{\omega=1}^{N_\omega} [\textbf{K}(\Theta)\nabla (\psi+z)]_\omega \cdot\textbf{n}_\omega A_\omega
$$

After time stepping is complete, the conventional FVM practice typically writes and solves the discretized equations in matrix form. Due to the stiffness and sparsity of the resulting matrix, solving such a matrix equation is known to be computationally challenging. Therefore, we propose an alternative route that solves the discretized equations in an iterative manner using an adaptive L-scheme by adding the term $$L_i^{m+1,s}(\psi_i^{m+1,s+1}-\psi_i^{m+1,s})$$ to the discretized LHS of the integral equation. This adaptive L-scheme extends the idea of standard static L-scheme<d-cite key="suciu2021global"></d-cite> by ensuring convergence of the L-scheme<d-cite key="song:2022:richards"></d-cite>.

Overall, we obtain an adaptive linearized FVM numerical scheme that favors the preservation of physical information of the original PDE:

$$
\begin{aligned}
     \psi_i^{m+1,s+1} =& \frac{1}{L_i^{m+1,s}}\sum_{\omega=1}^{N_\omega} \textbf{K}_\omega^{m+1,s}\cdot\textbf{n}_\omega\frac{(\psi+z)_j^{m+1,s}-(\psi+z)_i^{m+1,s}}{d(j,i)}A_\omega\\&-\frac{1}{L_i^{m+1,s}}\frac{\Theta_i^{m+1,s+1}-\Theta_i^m}{\Delta t}\text{vol}(V_i)+\psi_i^{m+1,s}.
\end{aligned}
$$


***

## Data-Driven Random Walk Algorithm

We further introduce a data-driven random walk (DRW) algorithm that will be integrated with the FVM scheme to solve the PDE. Compared to pure FVM-based approaches, the additional underlying physical knowledge implicitly learned by the DRW algorithm can be very useful in obtaining accurate solutions of the PDE. Let $$n_i^{m+1,s}$$ be the number of particles in cell $$i$$ at fixed-point iteration step $$s$$ and time step $m+1$, and $$\delta n_{i,j}^{m+1,s}$$ be the number of particles moved from cell $$i$$ to cell $$j$$ at iteration $$s$$ and time step $$m+1$$. Without loss of generality, let us consider the 1-dimensional case of the Richards equation in which the number of water molecules in cell $$i$$ follows:

$$
  n_i^{m+1,s}=\delta n_{i,i}^{m+1,s}+\delta n_{i+1,i}^{m+1,s}+\delta n_{i-1,i}^{m+1,s}
$$

We point out that the concept of random walk of particles has been adopted previously<d-cite key="vamos2001global"></d-cite> for solving the diffusion equation. However, we observe that directly using this random walk concept is insufficient, as the relationship between pressure head $$\psi_i$$ and the number of particles $$n_i$$ still remains unclear. Therefore, we suggest model the relationship using a multi-layer neural network (MNN), which are known to be possible given that the neural network contains enough neurons. MNN enables us to approximate $$\psi_i$$ as a nonlinear function of $$n_i$$, $$\psi_i=f(n_i)$$, at any fixed time step and iteration step, which can be incorporated in the discretized equation to yield the following data-driven random walk (DRW) formulation:

$$
\begin{aligned}
     n_i^{m+1,s+1} =& \frac{1}{L_i^{m+1,s}}\sum_{\omega=1}^{N_\omega} \textbf{K}_\omega^{m+1,s}\cdot\textbf{n}_\omega\frac{n_j^{m+1,s}-n_i^{m+1,s}}{d(j,i)}A_\omega \\&+ f^{-1}(\textbf{J}) +n_i^{m+1,s},
\end{aligned}
$$

where $$\textbf{J}=\sum_{\omega=1}^{N_\omega} \textbf{K}_\omega^{m+1,s}\cdot\textbf{n}_\omega\frac{z_j^{m+1,s}-z_i^{m+1,s}}{d(j,i)}A_\omega-\frac{1}{L_i^{m+1,s}}\frac{\Theta_i^{m+1,s+1}-\Theta_i^m}{\Delta t}\text{vol}(V_i)$$.

***

## DRW Architecture

The figure below shows our DRW architecture for solving the Richards equation. Of course, such architecture can be generalized to other PDEs.

<div class="row">
    <div class="col mt-3 mt-md-0">
    </div>
    <div class="col-10 mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/publication_preview/drw_focapo.svg' | relative_url }}" alt="DRW architecture"/>
    </div>
    <div class="col mt-3 mt-md-0">
    </div>
</div>

During offline learning, we first obtain reference solutions from the global random walk solvers developed by <d-cite key="suciu2021global"></d-cite>. We also introduce Gaussian noise to these reference solutions to reflect the stochastic nature of the relationship between $$\Psi_i^s$$ and $$n_i^s$$ and improve the robustness of DRW algorithm by enhancing its generalization performance. Introducing Gaussian noise also improves the quality of solutions obtained, as the reference solutions themselves exhibit random error and are not strictly accurate. The noise-added reference solutions are used as training and validation sets to train two MNNs, namely MNN1 and MNN2. In MNN1, we learn $$f$$ that maps the number of particle in a cell to the pressure head information, whereas in MNN2, we learn the inverse mapping $$f^{-1}$$ from pressure head information to the number of particles. Once offline learning is complete, we proceed to the actual solution process, where the Richards equation to be solved is first discretized to the adaptive linearized FVM scheme. Then, the discretized form is sent to the DRW algorithm, where it passes through the inverse mapping $$f^{-1}$$ learned from MNN2 to generate the solution of the Richards equation in terms of the particle distribution in each cell, $$n_i$$. Finally, to convert this solution $$n_i$$ to physically meaningful solutions such as pressure head $\Psi$, flux $$q$$, and moisture content $$\Theta$$, we apply the trained mapping $$f$$.

For more information about the numerical case study for illustrating the effectiveness of the DRW algorithm architecture, please refer to our recent publication<d-cite key="song:2022:richards"></d-cite>.