# Distributed systems and the web

## Things to get across
- Distributed systems are hard
- What is a distributed system
  - Set of processes that are spatially separated
  - "A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable." - Leslie Lamport
- Examples where distributed systems theory shows up in day to day work
  - Dirty writes
  - Database ordering
  - Message queueing
  - Consistency in systems
  - Monotonic clocks/time/leapseconds
- Lamport theory
  - ordering
  - clocks
  - lamport diagrams
- Contemporaries
  - Camille Fournier
  - Kyle Kingsbury
  - Caitie McCaffrey
  - Christopher Meiklejohn


## Papers
- On Distributed Communications Networks - Paul Baran
- https://github.com/aphyr/distsys-class
- Time, Clocks, and the Ordering of Events in a Distributed System - Leslie Lamport [http://amturing.acm.org/p558-lamport.pdf](http://amturing.acm.org/p558-lamport.pdf)

## Actual talk

### Intro
- Who knows what a distributed system is?
- Who works on one?
- Hopefully by the end of this everyone will answer yes for at least one of those questions

### What is a distributed system
- In general we can think of a distributed system as pieces of a system connected by a network
  - The cloud
  - Serverless architectures
  - Mobile devices
  - Web applications
- We live in a world of distributed systems
- This isn't new, was being studied heavily in the 70's by Leslie Lamport
- In more practical terms, I like to fall back on his famous quote 'A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable'.
- Examples
  - Browser making requests to a backend server
  - Backend server making requests to a database
  - Backend server making requests to another server
  - A cluster of datastores
  - Messaging system 

### Theory
- Falacies of distributed computing - Peter Deutsch
  1) The network is reliable.
    - Reorder
    - Drop
    - Redeliver
    - Use TCP for reliable networking
  2) Latency is zero.
    - Bounded by physics
    - Electricity moves at the speed of light - 1foot/nanosecond (Grace Hopper)
    - Fast delivery of data means moving the data closer to the customer
  3) Bandwidth is infinite.
    - Certainly untrue for mobile networks, but also true for "normal" networks
    - Faster to truck data in hard drives than to transport over the network
    - Amazon Snowmobile (come pick up your data and physically move it to the cloud)
  4) The network is secure.
    - Botnets
    - Use HTTPs
    - Watch Luke Crouch's talk - https://www.youtube.com/watch?v=0XDpJUhDTos
    - Don't be complacent 
  5) Topology doesn't change.
    - The internet routes around perceived damage
    - What was once fast may now be slow
    - Nodes on the network move (mobile devices, containers on the server)
  6) There is one administrator.
    - You don't control the network
    - VPNs, Corporate Firewalls, Etc...
    - Can't trust even basic "common usage"
  7) Transport cost is zero.
    - Two ways to interpret 
      - Money - Hardware costs money, a solution could work but is prohibitively expensive 
        - Cloud == reliability, also == cost to acheive that reliability
      - Time/space - It takes resources to even get things onto the network
        - JS async IO, single threaded computation, marshalling JSON == blocking
    - Think twice before microservices
  8) The network is homogeneous.
    - Different parts of the network have different latencies
    - Last leg may be incredibly slow
    - Some network links are less reliable than others
- Parts of the system will fail
  - You should be prepared, build with failure in mind
  - Ordering matters
  - Idempotency
  - Backpressure
- Clocks and ordering
  - Time
    - Wall clock time isn't reliable
    - Clocks drift
    - Monotonicity
  - Ordering and Consistency
    - Consistency - Safe history of events in a system
      - Higher consistencies need concensus
      - avoid concensus if you can
      - CRDTs - order free data types 
    - Lamport clocks, Paxos
      - Ways of acheiving ordering and consensus in a system
      - Left to reader to discover more

### Day to day
- Network unreliability
  - "Slow response"
  - "Inconsistent response"
- Users cause issues
  - "Double submit"
  - "User reloads POSTed page"
  - "User gets impatient"
- Concurrency
  - "Dirty writes"
  - "Internal ordering"
- It's Slow
  - Hardest to troubleshoot
  - What is slow?
  - What even is slow?
  - Network?
  - Application?
  - Interaction between nodes in the system?

### Summary
- Distributed systems are hard
- Essentially they and their problems are unavoidable 
- Being informed of these problems helps you make reliable systems

