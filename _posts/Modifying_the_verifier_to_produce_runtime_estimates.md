---
layout: post
title:  "The BPF Runtime Estimator"
---

This blog is a technical walkthrough on modifying the BPF verifier to emit a [best - worst case] runtime

estimate for any given eBPF program at load time. The complete research statement and evaluations can be found in our research paper [Enabling BPF Runtime policies for better BPF management](/papers/ebpf23-runtime.pdf) which was presented in Workshop on eBPF and Kernel Extensions, SIGCOMM'23. 


### Why we need expected runtime estimates?
When a kernel developer wants to attach their BPF code to leverage one of the several benefits of using this in-kernel virtual machine, the performance impact of these seemingly innocent programs are mostly ignored. When I say mostly, I mean that there could be certain level of performance analysis done on the very hook point where the BPF program is going to get attached, but the overall impact of a new BPF program is not considered. 

As current age production servers are now deploying hundreds of BPF program for special use cases, it will increasingly become difficult to understand impact of one BPF program on other BPF programs, or on the system in general. Thus, we want to provide better insight to a kernel developer or a sysadmin who wants to know and control impact of these tiny BPF programs on the system.  

Obtaining a runtime estimate from the verifier about performance of a BPF program is just step 1 towards the desired world we are picturing here. If you are wondering what could be the next steps, we imagine it would be providing policy based decision making where an admin can specify maximum tolerable latency for critical kernel functionalities. Such runtime policies should be able to handle complex interaction between kernel-BPF and BPF-BPF fairly accurately with the admin having the control knobs that would be very simple and easy to operate.  


### Preface 
The BPF-verifier is responsible for ensuring that a BPF bytecode is not malicious and cannot stall the kernel in any way: by accessing and modifying pointers illegaly, infinite loops, branch predictors, etc.
These safety properties is what makes BPF stand uniquely compared to kernel modules. In order to achieve these properties, the verifier performs several different passes on the provided BPF bytecode, before it gives the Just-In-Time compiler (JIT) a green signal to convert the bytecode into an executable native code. 

Now, as the verifier needs to perform symbolic execution over every possible branch in the program, it faces the well-known issue of state explosion if the number of branches are too high. Due to this, BPF programs are restricted to 4k instructions while the maximum complexity traversed by a verifier should not exceed 1M. Why did I bring this fact here will be clear in a bit. 

As the instruction limit is very short and BPF programs are not allowed to access any kernel function at will, the BPF developers provided something known as helper functions. These helper functions are an interface between BPF and the kernel. The verifier is programmed to step over a helper call (after confirming that the arguments passed are correct) which means that if we want to analyze the performance of the given BPF program, the verifier only knows about which intructions and which helper calls exists and within which branches. But as these helper functions are nothing but a black box from the perspective of the verifier, the verifier has no way to differentiate one helper call from the other in terms of their performance impact. 

To address this problem, we used offline measurement of helper functions which basically means that we pass several different input to a helper and note down how much time it took to process and return. When done multiple times, we end up getting a range showing the min time (the best case) and the max time (the worst case) execution time of the helper function. Yes you are right, this does not guarantee completeness, but it atleast gives us something to start with! We are not going into the details about what kind of values were obtained, but to give a teaser, the observed ranges were not at all the happy well-definied ranges we expected when starting with the experiment (Find some interesting discussion points along in the paper!). 

With this step done we can now (FINALLY) move towards the more techy part : programming the verifier to emit runtime estimates. 

### Taming the verifier
The verifier maintains a big struct called `struct bpf_verifier_state`{:.C} to maintain states of all functions encouncered in the current branch. Whenever the verifier identifies a new branch instruction (if-else), it clones the states and pushes it to the internal stack for exploring later, while continuing to explore the other arm of the branch. For example,  say the verifier reached an if condition which checks some condition and exits the program, the verifier will clone and push the current state of the `bpf_verifier_state` and set this clone's next instruction to point to the else condition. This way the verifier will go into the if-block, until the branch end and only if none of the security requirements are violated, pop the next state from the stack and resume exploration from there.  





