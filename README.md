# Microwatt Momentum Hackathon: Project Proposal

## WattMover - A Programmable DMA Controller for Microwatt

**Author:** SRUTHY H
**GitHub:** SruthyH11

---

### 1. Project Description

This project proposes the design and implementation of "WattMover," a programmable Direct Memory Access (DMA) controller tailored for the Microwatt-based OpenFrame SoC. The primary goal of a DMA is to offload the main CPU from handling large, repetitive data transfer tasks. By delegating these bulk memory operations to this specialized hardware unit, the Microwatt CPU is freed up to perform more complex computational work, thereby significantly improving overall system performance and efficiency.

---

### 2. Problem Statement

In a typical embedded system, moving blocks of data—such as sensor readings or communication packets—requires the CPU to execute a software loop. This process consumes thousands of valuable CPU cycles, stalls the execution of other critical tasks, and creates a performance bottleneck. This project directly addresses this inefficiency by providing a dedicated hardware solution.

---

### 3. Proposed Solution & Key Features

I will design and verify a memory-mapped, single-channel DMA controller that integrates cleanly into the OpenFrame SoC. The Microwatt CPU will control the DMA through a simple register interface.

**Key Features:**
* **Programmable Registers:** The CPU will configure transfers by writing to:
    * `SOURCE_ADDRESS` Register
    * `DESTINATION_ADDRESS` Register
    * `TRANSFER_SIZE` Register
    * `CONTROL_STATUS` Register (to start the transfer and check for completion).
* **Independent Bus Master:** The DMA will operate as an independent master on the system bus to perform memory operations without CPU intervention.
* **Interrupt on Completion:** Upon finishing a data transfer, the DMA will assert an interrupt to notify the CPU that the data is ready.

---

### 4. High-Level Block Diagram (Conceptual)

The DMA controller will interface with the CPU and Memory via the main system bus.
+---------------+      +------------------+      +------------------+
| Microwatt CPU | <--> |   System Bus     | <--> |  DMA Controller  |
+---------------+      | (e.g., AXI/Wishbone) |  |   (WattMover)    |
+------------------+      +------------------+
|                      | (Master)
V                      V
+------------------------------------------+
|                  Memory                  |
+------------------------------------------+
### 5. Expected Outcome & Success Criteria

The final deliverable will be a fully verified and synthesizable DMA controller IP integrated within the OpenFrame user project area.

The project's success will be measured by a clear performance benchmark: a direct comparison of the CPU cycles required for a software-based memory copy versus a DMA-assisted copy. The expected outcome is a greater than 95% reduction in CPU overhead for the benchmarked task, proving the design's significant impact and value to the OpenPOWER ecosystem.
### 6. Future Enhancements
- Multi-channel DMA.  
- Burst transfers for higher throughput.  
- Scatter-gather list support.  
- Integration with high-speed buses (AXI/AHB).  

