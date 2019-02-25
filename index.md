---
layout: default
title: "Performance Contracts for Software Network Functions"
---

# {{ page.title }}

{::options parse_block_html="true" /}

Software network functions (NFs), or middleboxes, promise flexibility and easy deployment of network services but face the serious challenge of unexpected performance behaviour. 
This behaviour makes it harder for network operators to provision their networks and exposes a new attack surface for adversaries seeking to degrade network performance.
The goal of our work, is to provide network operators and NF developers with comprehensive understanding of the NF's entire performance profile, before it is deployed. 
Such understanding would, for instance, allow operators to conduct precise capacity planning and developers to make informed development decisions. 

In this work, we propose the notion of _performance contracts_ for NFs. A performance contract enables users to predict and scrutinize NF performance at fine granularities without having to run them. It providers users with an abstraction that enables them to easily parameterize arbitrary input workloads, whether typical, exceptional or adversarial. Given only this abstract description of the workload and not a concrete instance, the contract predicts the performance of the NF without actually running it. The performance predictions are in terms of human-readable formulae, expressed as a function of workload and environment variables, that we together call _Performance Critical Variables (PCVs)_. 

![Contracts](images/contracts.svg)

Additionally, we build and evaluate BOLT, a technique and tool for computing such performance contracts for the entire software stack of NFs written in C, including the core NF logic, DPDK packet processing framework, and NIC driver. 
BOLT takes as input the NF implementation code and outputs the corresponding contract.
Under the covers, it combines pre-analysis of a library of stateful NF data structures with automated symbolic execution of the NF's code.
We evaluate BOLT on four NFs---a Maglev-like load balancer, a NAT, an LPM router, and a MAC bridge---and show that its performance contracts predict the dynamic instruction count and memory access count with a maximum gap of 7% between the real execution and the conservatively predicted upper bound. With further engineering, this gap can be reduced.

If you'd like to more about Performance Contracts or BOLT, feel free to [contact us](mailto:rishabh.iyer@epfl.ch) 

<!-- ### What are PCVs? Why are contracts expressed using PCVs? 

The performance of the NF is a function of the incoming packet, the NF state left behind by packets that came before and configuration and environment variables. 
While it is infeasible to explicitly list every possible sequence of packets that came before, the PCVs allow us to succintly capture their impact on performance. 
Consequently, PCVs abstract away specificities in the NF state, distilling the key parameters that performance depends on. 

Predicting performance in terms of PCVS provides users with insight into what factors performance primarily depends on and how it varies. The PCVs also enable fluid navigation of the tradeoff between the level of detail that the contract exposes about the code and the contract’s legibility (i.e., how easy it is for a human to parse and draw useful conclusions from).
Different users may need different balances between detail and legibility. For instance, an NF developer who uses performance contracts to debug and optimise the performance of their own code will likely want more detail than a network operator who has no access to NF implementations and uses
performance contracts solely to provision their network. By using PCVs to abstract away details in a user-specific form, we can generate contracts that with different detail/legibility balance. -->

<!-- #### How does Bolt generate contracts?

Prior work proposed the [Vigor framework](vignat.github.io) for efficient analysis of NF code. This framework proposes a state-based demarcation, separating the hard-to-analyze stateful NF data structures from the stateless primitives that operate upon them. This separation allows the hard-to-analyze parts of the NF code to be encapsulated into a library, which if analyzed once (using human-aided techniques) can then be reused across NFs. 

Bolt relies on the Vigor analysis framework to efficiently analyze NF code. The process of generating performance contracts is a recursive one with 3 steps. 

1) The base case of our recursion are stateful data structures. Here BOLT uses the PCV abstraction to succintly summarise performance of the hard-to-analyze data structures. 

2) Next, to generate performance contracts for entire NFs, we use a technique called [Exhaustive Symbolic Execution](https://klee.github.io/) that allows us to list all the execution paths through the stateless code of the NF. While traversing each path, we tally the performance cost of the stateless code and simply plug-in the contracts for calls to stateful functions. 

3) Finally, to generate contracts for NF chains, we pair together packet classes from the contracts of communicating NFs and equate the packet sent by the first NF to the packet received by the second. This allows us to capture the inter-NF dependencies. 

![Vigor Method](images/temp.png)


### Results
We evaluate Bolt on 4 NFs - a Maglev-like load balancer, a NAT, an LPM router, and a MAC bridge.
For each NF, we generate traffic from several packet classes, measure the actual performance, and compare it against the values predicted in the contract. 
Irrespective of the NF and traffic classes, Bolt predicts the Instruction Count and Memory Accesses accurately, to within 7% of the measured values. 
For latency, BOLT is within 3x for typical workloads.  -->

<!-- ### Contact
{::options parse_block_html="true" /}

<div class="row">
<div class="col-md-3 text-center">
<img class="bumshot" src="images/headshots/arseniy_small.jpg" alt="Arseniy Zaostrovnykh"/>
<h5 class="card-title">Arseniy Zaostrovnykh</h5>
<p class="card-email"><a href="mailto:arseniy.zaostrovnykh@epfl.ch">
arseniy.zaostrovnykh@epfl.ch
</a></p>
</div>

<div class="row">
<div class="col-md-3 text-center">
<img class="bumshot" src="images/headshots/arseniy_small.jpg" alt="Arseniy Zaostrovnykh"/>
<h5 class="card-title">Arseniy Zaostrovnykh</h5>
<p class="card-email"><a href="mailto:arseniy.zaostrovnykh@epfl.ch">
arseniy.zaostrovnykh@epfl.ch
</a></p>
</div>

<div class="col-md-2 text-center">
<img class="card-img-top bumshot" src="images/headshots/solal_small.png" alt="Solal Pirelli"/>
<h5 class="card-title">Solal Pirelli</h5>
<p class="card-email"><a href="mailto:solal.pirelli@epfl.ch">solal.pirelli@epfl.ch
</a> </p>
</div>

<div class="col-md-2 text-center">
<img class="card-img-top bumshot" src="images/headshots/luis_small.jpg" alt="Luis Pedrosa"/>
<h5 class="card-title">Luis Pedrosa</h5>
<p class="card-email"><a href="mailto:luis.pedrosa@epfl.ch">luis.pedrosa@epfl.ch
</a> </p>
</div>

<div class="col-md-3 text-center">
<img class="card-img-top bumshot" src="images/headshots/katerina_small.jpg" alt="Katerina Argyraki"/>
<h5 class="card-title">Katerina Argyraki</h5>
<p class="card-email"><a href="mailto:katerina.argyraki@epfl.ch">
katerina.argyraki@epfl.ch
</a> </p>
</div>

<div class="col-md-2 text-center">
<img class="card-img-top bumshot" src="images/headshots/george_small.png" alt="George Candea"/>
<h5 class="card-title">George Candea</h5>
<p class="card-email"><a href="mailto:george.candea@epfl.ch">george.candea@epfl.ch
</a> </p>
</div>
</div> -->

