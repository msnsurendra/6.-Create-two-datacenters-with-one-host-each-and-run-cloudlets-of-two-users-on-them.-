 # Experiment 6  
## Create two datacenters with one host each and run cloudlets of two users on them

---

## Overview
This experiment demonstrates a CloudSim simulation where two users submit cloudlets that execute across two different datacenters. Each datacenter contains one host, and tasks are scheduled using brokers representing users. The experiment shows distributed task execution and resource allocation in a cloud environment.

---

## Aim
To create two datacenters with one host each and execute cloudlets of two different users on them.

---

## Objectives
- Simulate multiple datacenters
- Simulate multiple users
- Configure hosts and resources
- Create VMs for users
- Execute cloudlets
- Observe distributed execution behavior

---

## Tools and Requirements

| Component | Version |
|--------|---------|
| Java | JDK 8+ |
| CloudSim | 3.0.3 |
| IDE | IntelliJ / Eclipse |
| OS | Windows / Linux |

---

## Datacenter Configuration

| Parameter | Value |
|----------|------|
| Datacenters | 2 |
| Hosts per DC | 1 |
| RAM | 2048 MB |
| Storage | 1,000,000 MB |
| Bandwidth | 10000 Mbps |
| Scheduler | Time Shared |

---

## VM Configuration

| VM | MIPS | RAM |
|----|------|-----|
| VM1 | 500 | 512 MB |
| VM2 | 1000 | 512 MB |

---

## Cloudlet Configuration

| Cloudlet | Length |
|----------|--------|
| C1 | 20000 |
| C2 | 40000 |
| C3 | 60000 |
| C4 | 80000 |

---

## Algorithm
1. Initialize CloudSim library  
2. Create two datacenters  
3. Create two brokers (users)  
4. Create VMs for each user  
5. Submit VMs to brokers  
6. Create cloudlets for each user  
7. Submit cloudlets to brokers  
8. Start simulation  
9. Collect results  
10. Stop simulation

 ## Sample Output

========== RESULT ==========
Cloudlet 0 executed in Datacenter 2 using VM 0
Cloudlet 1 executed in Datacenter 3 using VM 1
Cloudlet 2 executed in Datacenter 2 using VM 0
Cloudlet 3 executed in Datacenter 3 using VM 1


## Program 












## Result
Cloudlets from different users were successfully executed across two datacenters. The simulation demonstrates distributed task execution and broker-based scheduling.

---

## Conclusion
This experiment verifies that CloudSim accurately simulates multi-user and multi-datacenter environments. It demonstrates how distributed infrastructure handles workloads and how resources are allocated efficiently in cloud systems.

---
 
 
