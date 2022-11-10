---
layout: page
title: Innovating future-generation separation technologies
description: To improve energy efficiency and enable industrial decarbonization
img: assets/img/projects/chemical plant.jpg
importance: 3
category:
---

Separations are ubiquitous in chemical process industries. They are energy intensive and are estimated to account for 40-60% of capital and operating costs as well as most of the carbon footprint associated with a chemical plant. As a result, industrial practitioners and the general public are calling for innovative solutions that improve the overall efficiency of separation processes. In particular, they are looking for systematic solutions to the following series of questions: 

> For a given separation task, what are all the possible flowsheet options? Which ones are the best? And how should they be built and operated? How to systematically generate intensified new designs from these options? How to validate these novel process designs?

To answer these questions, CLAMS will develop advanced computational tools and couple them with state-of-the-art experimental capabilities as well as novel conceptual design methodologies. Specifically, the separations research at CLAMS will focus on three distinct and interconnected components: **computational**, **experimental**, and **conceptual**. Computational research utilizes mathematical modeling, process optimization, and artificial intelligence to systematically synthesize optimal process flowsheets and their optimal operating conditions for a given separation task. Experimental research uses leading-edge process analytical technologies to generate valuable experimental data that can be used for model training. In addition, by building and testing pilot-scale process equipment prototypes, experimental research also serves to validate the feasibility and attractiveness of novel conceptual design ideas. Finally, conceptual process design gathers the computational and experimental research findings to come up with systematic process synthesis tools in the context of process intensification, modularization, continuous manufacturing. 

<div class="row">
    <div class="col mt-3 mt-md-0">
    </div>
    <div class="col-7 mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/projects/separations.svg' | relative_url }}" alt="Separations research consists of three distinct but interrelated components."/>
    </div>
    <div class="col mt-3 mt-md-0">
    </div>
</div>
<div class="caption">
    Separations research consists of three distinct but interrelated components.
</div>

### Computational Research

Computational research lays the theoretical and computational foundations for both experimental research and conceptual process synthesis research. It contains three thrusts: mathematical modeling, process optimization, and artificial intelligence. Mathematical modeling is fundamental to the success of other computation research thrusts. At CLAMS, we are interested in constructing insightful shortcut models to fundamentally understand and characterize different separation processes:

1. Developing structurally simple and numerically stable differential-algebraic equation (DAE) based models for rate-based separation processes (e.g., crystallization, adsorption, pervaporation, membrane based separations).

2. Constructing a unified shortcut model for equilibrium-staged multicomponent separation processes (e.g., distillation, absorption and stripping, extraction) and exploring its mathematical properties that makes it easily implementable in a global optimization framework.

Process optimization formulates and solves optimization problems related to synthesis and design of separation process systems that optimize certain objective, such as annual profit, energy consumption, carbon footprint, etc. These optimization problems will embed the shortcut models developed under the modeling thrust. Even though many of these problem formulations are known to be NP-hard, we aim at developing efficient and robust optimization algorithms that can solve these problems quickly. A strong emphasis will be put onto ensuring global optimality of the solution. We will derive and implement novel, formulation-tailored solution strategies, including new relaxation and discretization techniques as well as new algorithms, to solve the following problems:

1. Deterministic global (mixed-integer) dynamic optimization with nonlinear ODEs for batch crystallization and multicomponent membrane cascade synthesis and optimization.

2. Superstructure synthesis and optimization of hybrid separation process network consisting of various types of unit operations.

Artificial intelligence supports and facilitates both mathematical modeling and process optimization thrusts by introducing leading-edge breakthroughs in data analytics and machine learning. Machine learning will be particularly useful for solving problems that are not amenable to precise mathematical description. CLAMS will develop AI platforms that combine first-principle models and data-driven machine learning techniques. I am keen to solve the following challenges in separation:

1. Optimal control of batch crystallizer by developing state-of-the-art reinforcement learning approaches (e.g., Q-learning) and coupling them with online process analytical technologies.

2. Predicting azeotropic behavior of complex multicomponent systems via supervised learning.

### Experimental Research

Experimental research guides and facilitates both computational and conceptual design components. It generates valuable first-hand experimental data that can be utilized by the mathematical modeling thrust for assessing model accuracy, by the process optimization thrust for data-driven optimization, and by the AI thrust for predictive analytics, model training, and feedback control. Meanwhile, by building and testing prototypes and performing scale-down analysis, experimental research also serves to evaluate the feasibility and attractiveness of novel conceptual design ideas. Inspired by this, we plan to study the following problems:

1. Kinetic parameter estimation for batch crystallization using in situ process analytical technologies connected to integrated chemical synthesis platforms.

2. Exploring retrofit opportunities to facilitate the transition from batch to continuous manufacturing by experimentally validating innovative conceptual design ideas and building pilot-scale prototypes, such as fully operable dividing wall distillation columns.

### Conceptual Process Synthesis

Conceptual process synthesis takes all the research findings previously discovered to come up with new, intensified, sustainable, and cost-effective process flowsheet concepts. Recent trends in process intensification, modularization, and continuous manufacturing are also considered when formulating and refining these conceptual design methodologies, which should be easily convertible into a set of mathematical rules and constraints to enable systematic synthesis of new and attractive flowsheet options with the click of a button. Meanwhile, these methodologies and high-level concepts also generate new design ideas, which further open up new computational and experimental research directions. At CLAMS, we will develop a software suite that systematically synthesizes a slew of new, intensified separation process flowsheets in a fully automated manner.