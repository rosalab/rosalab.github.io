---
title: 2nd Workshop on eBPF and Kernel Extensions
layout: post
author: Milo Craun 
website: https://milocraun.com
---

Our lab published two workshop papers to the [2nd Workshop on eBPF and Kernel Extensions](https://conferences.sigcomm.org/sigcomm/2024/workshop/ebpf/) held at SIGCOMM in Sydney.
After over 24 hours of travel from peaceful Blacksburg to Sydney, we successfully arrived in Sydney to present our work and participate in the workshop.

To start off the day, [Brenden Gregg](https://www.brendangregg.com/), of eBPF performance
    engineering fame, gave a keynote outlining the history and development of eBPF, as
    well as presenting his plan for "Fast by Friday".

The first session featured work about challenges to eBPF development.
Each paper tried to highlight some existing challenge with eBPF and present 
    some solution to the challenge.
Our work on [eliminating untraced overhead](https://dl.acm.org/doi/10.1145/3672197.3673431)
    was presented here.
One key takeaway from this session was the large gap between new eBPF feature creation and
    adoption.
The documentation for new features is often not clearly available, and it takes time 
    for information to trickle down into the rest of the community.
Additionally, many eBPF tools were created before new features were available, further
    growing the gap.
It is not exactly clear how this gap can be solved.

The second session featured work on extending eBPF capabilities.
Our work on [eBPF program nesting](https://dl.acm.org/doi/10.1145/3672197.3673440)
    was presented in this session.
One key takeaway from the session is the need for a more global view in eBPF verification.
Our work and work on 
    [functional verification of eBPF](https://dl.acm.org/doi/10.1145/3672197.3673435) both
     point out the need for verification to understand more about the system and 
    interactions between eBPF programs.
Another key idea that was brought up in discussion was thinking through why one would
    use eBPF as a VM for other use cases, as opposed to other technologies such as
    WebAssembly.

The final session featured work on application acceleration with eBPF.
Continuing in the line of research work such as 
    [BMC](https://www.usenix.org/conference/nsdi21/presentation/ghigoff)
    this session looked for opportunities to improve application performance by
    utilizing eBPF's ability to move where computation can occur.
One key takeaway from this session was the need to continue to look for and implement
    other kinds of eBPF hook points.
Over time the set of available hook points has continued to grow, and looking for new
    opportunities to add hook points allows for new possibilities with eBPF.

The workshop is a great opportunity to bring together researchers interested in all 
    things eBPF.
We presented multiple works at the previous iteration of the workshop, and we hope
    to continue to be present in the future.


