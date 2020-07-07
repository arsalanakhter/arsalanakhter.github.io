---
title:  "Using Supervised Learning to solve Mixed Integer Optimization Problems"
date:   2020-06-30 15:16:00
categories: [Optimization and ML]
tags: [Optimization, Machine Learning, Cartpole, MILP]
---

Our goal in this post is to build a neural network based classifier that could solve Mixed Integer programs MIP close to optimality but much faster than a MIP solver (e.g. Gurobi or MOSEK).

To do that, we will first generate labeled data for an optimal control problem. The data will consist of parameter values and their optimal solutions. This data will then be used to train a calssifier that could take parameter values as an input and give an optimal solution as the output.

We'll be re-implementing the paper <strong>Learning Mixed-Integer Convex Optimization Strategies for Robot Planning and Control</strong> by *Abhishek Cauligi, Preston Culbertson, Bartolomeo Stellato, Dimitris Bertsimas, Mac Schwager, and Marco Pavone*. Their implementation can be found at [https://github.com/StanfordASL/mlopt-micp](https://github.com/StanfordASL/mlopt-micp)


<h3>Cartpole Problem</h3>

The cartpole problem is taken from the paper <strong>Warm Start of Mixed-Integer Programs for Model Predictive Control of Hybrid Systems </strong>by *Tobia Marcucci and Russ Tedrake*. Consider the following cartpole system. 


<div style="text-align:center"><img src="{{site.baseurl}}/images/micp/cartpole.jpg" /></div>

with following parameters:

- \\(x^t \in \mathbb{R}^4\\) : State of the cartpole. This includes position of cart \\(x^t_1\\), angle of pole \\(x^t_2\\), and their derivatives \\(x^t_3\\) and \\(x^t_4\\)
- \\(u^t \in \mathbb{R}\\) : Force applied to the cart.
- \\(s^t \in \mathbb{R}^2\\) : Contact forces imparted by the two walls.
- \\(\lambda^t \in \mathbb{R}^2\\) : Relative distance of the tip of the pole w.r.t to the walls.
- \\(\gamma^t \in \mathbb{R}^2\\) : Relative distance of the tip of the pole w.r.t to the walls. 
- \\(\kappa, \nu\\) : Parameters of the soft contact model with the wall.


