---
layout: post
title: Quadrotor Control
description: Robust Predictive Control for Quadcopter Hover Stabilization
img: /img/rolling-spider1.jpg
---

For a course project (ME 290J, Advanced Model Predictive Control) in graduate school, I designed a robust model predictive control strategy to improve the accuracy
of quadcopter hover stabilization. Traditional methods typically involve a simple PID controller, tuned using a nominal model of the quadrotor dynamics linearized 
around hover conditions. My method demonstrated improved results over both this approach and a nominal model predictive control algorithm.

<div class="img_row">
	<img class="col three" src="{{ site.baseurl }}/img/rolling-spider1.jpg" alt="" title="Rolling Spider"/>
</div>
<div class="col three caption">
	The Parrot Rolling Spider, a miniature quadrotor. Picture by <a href="http://www.techcrunch.com/2014/08/11/jumping-spider-rolling-sumo-review/">TechCrunch</a>.
</div>

The PID and nominal MPC algorithms are tuned using a model of the quadrotor dynamics linearized around hover conditions. The robust MPC strategy uses an additive 
uncertainty model, which was empirically obtained. This uncertainty captures any linearization error that arises when operating around hover conditions.

For controller synthesis, <a href="http://control.ee.ethz.ch/~mpt/>MPT3</a>, a MATLAB library for multiparametric optimization was used. MPT3 allows for the formulation
of explicit controllers, which mitigates the runtime complexity of MPC at the cost of required disk space. Control paramters were tuned to balance accuracy control 
against limitations from onboard hardware.

<div class="img_row">
	<img class="col one" src="{{ site.baseurl }}/img/pid.jpg" alt="" title="PID"/>
	<img class="col one" src="{{ site.baseurl }}/img/mpc.jpg" alt="" title="MPC"/>
	<img class="col one" src="{{ site.baseurl }}/img/rmpc.jpg" alt="" title="Robust MPC"/>
</div>
<div class="col three caption">
	Results comparing the three control strategies. From left to right: PID, MPC, and robust MPC.
</div>

Metrics used for assessment were mean drone position and variance. The Robust MPC approach performed the best under both of these metrics. The PID controller 
performed better than the nominal MPC strategy in terms of mean position, but the nominal MPC controller results displayed lower variance.
