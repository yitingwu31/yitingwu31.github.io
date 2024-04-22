---
title: "Deterministic Routing using Genetic Algorithm"
description: "An exploration around deterministic routing of network on chip with routing table populated with genetic algorithm."
pubDate: "Mar 2024"
link: "https://github.com/yitingwu31/booksim"
heroImage: "/post_img.webp"
tags: ["NoC", "Network Simulation"]
hashtags: ["Booksim", "NoC Routing", "Genetic Algorithm"]
---

Efficient routing for both large-scale networks and network-on-chip has become increasingly important as modern applications often require low-latency, high-throughput packet transmission.
State-of-the-art adaptive routing is designed to reflect and react to real-time network traffic. However, adaptive routing often adds overhead as it stores, computes and propogates network states. Adaptive routing also comes with the pitfall of weighing local information more than global congestion information.
On the other hand, deterministic routing has minimal overhead as routes are pre-computed, which could be a viable approach in scenarios where workloads are known beforehand.

In this work, we explore the middle ground of adaptive and deterministic routing, by generating a deterministic routing table with genetic algorithm (GA). The GA generates the routing table by iteratively choosing paths for all source-destination pairs, running a network simulation, and selecting optimal paths based on the simulation score. The process of generating the routing table resembles adaptive routing in its iterative nature and path selection based on network congestion. We compare the results of deterministic routing with GA with traditional deterministic routing, oblivious routing and adaptive routing on various benign and harsh traffic. 

The simulation is done with [Booksim](https://github.com/booksim/booksim2) by Jiang, Becker, Michelogiannakis, Balfour, Towles, Kim and Dally. GA script is written in Python and NoC simulation written in C++.
