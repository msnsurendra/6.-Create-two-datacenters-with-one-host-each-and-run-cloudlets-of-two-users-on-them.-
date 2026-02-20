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
import org.cloudbus.cloudsim.*;
import org.cloudbus.cloudsim.core.CloudSim;
import org.cloudbus.cloudsim.provisioners.*;

import java.util.*;

public class TwoDatacenterSimulation {

    public static Datacenter createDatacenter(String name) {

        List<Host> hostList = new ArrayList<>();

        List<Pe> peList = new ArrayList<>();
        peList.add(new Pe(0, new PeProvisionerSimple(1000)));

        Host host = new Host(
                0,
                new RamProvisionerSimple(2048),
                new BwProvisionerSimple(10000),
                1000000,
                peList,
                new VmSchedulerTimeShared(peList)
        );

        hostList.add(host);

        DatacenterCharacteristics characteristics =
                new DatacenterCharacteristics(
                        "x86","Linux","Xen",hostList,
                        10.0,3.0,0.05,0.001,0.0
                );

        Datacenter datacenter = null;

        try {
            datacenter = new Datacenter(
                    name,
                    characteristics,
                    new VmAllocationPolicySimple(hostList),
                    new LinkedList<Storage>(),
                    0
            );
        }
        catch (Exception e) {
            e.printStackTrace();
        }

        return datacenter;
    }

    public static void main(String[] args) {

        try {

            CloudSim.init(1, Calendar.getInstance(), false);

            Datacenter dc1 = createDatacenter("Datacenter_1");
            Datacenter dc2 = createDatacenter("Datacenter_2");

            DatacenterBroker broker = new DatacenterBroker("Broker");
            int brokerId = broker.getId();

            // ---------- VMs ----------
            List<Vm> vmList = new ArrayList<>();

            vmList.add(new Vm(0, brokerId, 500, 1, 512, 1000, 10000,
                    "Xen", new CloudletSchedulerTimeShared()));

            vmList.add(new Vm(1, brokerId, 500, 1, 512, 1000, 10000,
                    "Xen", new CloudletSchedulerTimeShared()));

            broker.submitVmList(vmList);

            // ---------- CLOUDLETS ----------
            List<Cloudlet> cloudletList = new ArrayList<>();
            UtilizationModel model = new UtilizationModelFull();

            long[] lengths = {20000, 40000, 60000, 80000}; // different execution times

            for(int i = 0; i < 4; i++) {

                Cloudlet cloudlet = new Cloudlet(
                        i,
                        lengths[i],
                        1,
                        300,
                        300,
                        model,
                        model,
                        model
                );

                cloudlet.setUserId(brokerId);
                cloudletList.add(cloudlet);
            }

            broker.submitCloudletList(cloudletList);

            // ---------- RUN ----------
            CloudSim.startSimulation();
            List<Cloudlet> results = broker.getCloudletReceivedList();
            CloudSim.stopSimulation();

            // ---------- OUTPUT ----------
            System.out.println("\n========== RESULT ==========");

            for (Cloudlet cl : results) {
                System.out.println(
                        "Cloudlet " + cl.getCloudletId()
                                + " | Length: " + cl.getCloudletLength()
                                + " | VM: " + cl.getVmId()
                                + " | Datacenter: " + cl.getResourceId()
                                + " | Time: " + cl.getActualCPUTime()
                );
            }

        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
}


## Output
<img width="761" height="141" alt="image" src="https://github.com/user-attachments/assets/599045df-6fe6-48be-bd3b-9459d4c8fb30" />




## Result
Cloudlets from different users were successfully executed across two datacenters. The simulation demonstrates distributed task execution and broker-based scheduling.

---

## Conclusion
This experiment verifies that CloudSim accurately simulates multi-user and multi-datacenter environments. It demonstrates how distributed infrastructure handles workloads and how resources are allocated efficiently in cloud systems.

---
 
 
