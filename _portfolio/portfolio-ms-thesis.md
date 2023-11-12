---
title: "Towards the Reverse Engineering of DNN Structures on Heterogeneous Shared Cache Systems"
excerpt: "Exploring the exploitability of the shared cache between a CPU and GPU on an SoC<br/><img src='/images/Projects/ms_thesis/llc_and_ringbus.png'>"
collection: portfolio
---

# Overview
This project was completed as part of my masters thesis at Iowa State University under the guidance of Dr. Joseph Zambreno, Dr. Berk Gulmezoglu, and Dr. Henry Duwe.

The project explores the exploitability of a shared last-level-cache (LLC) on a 6th generation Intel SoC. The goal of the project was to demonstrate that it is possible to characterize the application accelerated by the intergrated graphics of the SoC through a timing side-channel on the CPU cores.

Timing side-channels require knowledge of the characteristics of your specific system. A side-channel leveraging a cache requires two baseline values; the time it takes for your system to complete a cache-hit, and the time it takes for a cache-miss. I used the [RDTSC](https://www.felixcloutier.com/x86/rdtsc "x86 - RDTSC") instruction available in the x86 instruction set to measure the cycle count between a memory access. I also forced cache misses using the [CLFLUSH](https://www.felixcloutier.com/x86/clflush "x86 - CLFLUSH") instruction. These two micro-benchmarks allowed me to establish a base-line threshold for what is considered a cache-hit or cache-miss.

![image](/images/Projects/ms_thesis/cache_hit_ubench.png)
![image](/images/Projects/ms_thesis/cache_miss_ubench.png)

# Observing GPU Activity
With a baseline set we can now perform a timing side-channel on the shared last-level cache of our Intel SoC. The timing side channel works by purposefully filling up a cache set with data and allowing the target application to run, the cache set addresses are then accessed again. During the second access we time how long it takes to access the data. An access time longer than our ground truth means the data was expelled from the cache  and we conclude that the target application accessed that cache location. 

Constructing the 