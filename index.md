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

![Contracts](./images/Contracts.svg)

Additionally, we build and evaluate BOLT, a technique and tool for computing such performance contracts for the entire software stack of NFs written in C, including the core NF logic, DPDK packet processing framework, and NIC driver. 
BOLT takes as input the NF implementation code and outputs the corresponding contract.
Under the covers, it combines pre-analysis of a library of stateful NF data structures with automated symbolic execution of the NF's code.
We evaluate BOLT on four NFs---a Maglev-like load balancer, a NAT, an LPM router, and a MAC bridge---and show that its performance contracts predict the dynamic instruction count and memory access count with a maximum gap of 7% between the real execution and the conservatively predicted upper bound. With further engineering, this gap can be reduced.

If you'd like to more about Performance Contracts or BOLT, feel free to [contact us](mailto:rishabh.iyer@epfl.ch) 
