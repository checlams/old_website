---
layout: post
title: Our new paper is published in the 2022 Futures Issue of AIChE Journal
date: 2022-10-18 15:00:00-0500
description: An invited article that solves a longstanding challenge in chemical engineering
tags: process-synthesis math-modeling optimization
categories: new-papers
---

Dr. Jiang's [latest publication](https://onlinelibrary.wiley.com/share/author/7K2E6XCRU4PCJMF2SRXW?target=10.1002/aic.17929) (with [Mohit Tawarmalani](https://web.ics.purdue.edu/~mtawarma/) and [Rakesh Agrawal](https://engineering.purdue.edu/ChE/people/ptProfile?id=3942)) is accepted by the 2022 [Futures Issue](https://aiche.onlinelibrary.wiley.com/hub/futures-issues) of AIChE Journal. Each year, nominations for inclusion in this special issue were developed from suggestions from AIChE Journal's Associate Editors, Consulting Editors, academic department heads, and authors from earlier editions of the Futures Issue. The many suggestions that emerged from this process were then pared down to balance the many possible research topics that could be represented, resulting in a total of 17 articles included in this issue.


In this paper, we develop the first accurate, easy-to-implement shortcut model for multicomponent distillations in any general multi-feed, multi-product (MFMP) column.

<div class="row">
    <div class="col mt-3 mt-md-0">
    </div>
    <div class="col mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/blogpost/2022-10-18-mfmp.pdf'| relative_url }}" alt="MFMP column"/>
    </div>
    <div class="col mt-3 mt-md-0">
    </div>
</div>
<div class="caption">
    A general MFMP column may contain multiple feed and/or sidedraw streams, making it difficult to model mathematically.
</div>

MFMP columns are ubiquitous in multicomponent distillation systems, such as crude fractionation, shale gas separation, and air separation. For the past 80 years, researchers and industrial practitioners have been searching for a general shortcut model that is as simple and powerful as the classic McCabe-Thiele or Underwood's method to perform quick and accurate design calculations and optimization of MFMP columns. To solve this longstanding problem in chemical engineering, we utilize an develop multiple mathematical tools to come up with the first shortcut model that accurately characterizes the energy requirement and the internal liquid/vapor flow behavior of a general MFMP column, explore its mathemtical properties, derive constraints for feasible separation and minimum reflux operation, and discuss their geometric interpretations. We show that the classic McCabe-Thiele or Underwood's method is a special case of this generalized algorithmic approach. We also revisit some of the well-accepted design heuristics and modeling assumptions widely used in existing literature and design practices, which turn out to be inaccurate and can sometimes lead to minimum reflux ratio values that are off by more than a factor of 10 compared to the true results for several separation tasks. On the other hand, our shortcut model accurately estimates the minimum reflux ratios that are often <3% different from rigorous Aspen Plus simulation results.

In the following paper (to be submitted), we will discuss how this shortcut method can be incorporated in an NLP/MINLP-based global optimization framework to allow optimal synthesis and design of multicomponent distillation systems, which is key to improving energy efficiency and enabling decarbonization of chemical and refining industries. This work is proudly supported by Office of Energy Efficiency and Renewable Energy (EERE), U.S. Department of Energy, under Award Number DEEE0005768.