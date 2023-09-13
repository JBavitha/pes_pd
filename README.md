# pes_pd
# Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
<details>
<summary> How to talk to computers </summary>

<details>
<summary> RISC-V(Reduced Instruction Set Computing-Five) </summary>

- Open Standard: RISC-V is an open standard ISA, which means that its specifications are freely available to the public. This openness encourages collaboration, innovation, and the development of a wide range of processors by various organizations and individuals.
- Simplicity: RISC-V follows the RISC philosophy of simplicity and orthogonality. It has a relatively small number of instructions with a regular encoding format, making it easier to design and optimize processors.

</details>

<details>

<summary> From Apps to Hardware </summary> 

Application software ---> System software ---> Hardware

This Application Software enters into a block called as System Software and this system software intern converts application program into  binary language.
- Major components of system sofware are:
  1. OS(Operating System)
  2. Compiler
  3. Assembler
![Screenshot from 2023-08-21 17-19-03](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c61ccc96-f3ad-4a8d-842c-0c0d5186eb4d)

### Type of Instructions
- Pseudo Instructions
- Base Integer Instructions(RV64I)
- Multiply Extension(RV64M)
- Single and Double precision floating point Extension(RV64F and RV64D)
</details>
</details>



<details>
<summary> SoC design and OpenLANE </summary> 

![image](https://github.com/JBavitha/pes_pd/assets/142578450/b2b20b8b-6564-46d5-8c02-9fc30d3f2fae)

## Simplified RTL to GDSII Flow

<img width="603" alt="Screenshot 2023-09-11 174858" src="https://github.com/JBavitha/pes_pd/assets/142578450/a6644fa7-83a0-48bf-8c94-cee34d5c5025">

```Synthesis : ``` Synthesis in the context of ASIC (Application-Specific Integrated Circuit) design is a crucial step in the overall ASIC design flow. It involves converting a high-level hardware description language (HDL) representation of a digital design into a gate-level netlist, which consists of logical gates (AND, OR, XOR, etc.) and flip-flops (registers).

```Floor planning :``` Floor planning is the process of determining how the various functional blocks, or modules, of an ASIC will be physically placed on the silicon die. It defines the overall chip's dimensions, the location of key components, and the routing channels for interconnects.

```Power planning :```Power planning, also known as power grid design, is the process of distributing power and ground throughout the ASIC to ensure stable and efficient power delivery. It involves creating a network of power rails and ground connections.

```place :```

1.Global Placement:
- Global placement is the initial phase of placement and focuses on finding a rough positioning of the cells on the chip's layout.
- It does not specify the exact coordinates but rather provides a high-level allocation of resources.
- The goal is to create a feasible floorplan that meets the chip's size and aspect ratio requirements while optimizing for factors like wirelength, timing, and power.

2.Detailed Placement:
- Detailed placement follows global placement and focuses on refining the positions of individual cells to achieve precise spatial coordinates.
- It determines the exact locations of each cell and ensures that cells are placed according to design constraints and the logical interconnections between them.

```Clock Tree Synthesis (CTS) :```CTS aims to efficiently distribute clock signals to all flip-flops and sequential elements in the design. This ensures that all clocked elements receive a synchronized clock signal, minimizing clock skew (the variation in arrival times of clock signals) and ensuring consistent operation.

```Signal Routing :```It involves the process of connecting various electronic components and interconnecting the signal paths to ensure proper functionality.

1. Global Routing:
- Global routing focuses on finding a rough path for each signal through the available routing channels to connect the source and destination points.
- It doesn't specify the exact path of each wire but rather defines high-level routing structures.

2. Detailed Routing:
- Detailed routing follows global routing and focuses on refining the exact paths of each signal.
- It specifies the specific routing resources (metal layers, vias, etc.) to be used for each net and resolves conflicts.

```Sign Off :```
- Physical Verifications
  - Design Rules Checking (DRC)
  - Layout vs. Schematic (LVS)
- Timing Verification
  - Static Timing Analysis (STA)

## Introduction to OpenLANE 
```Open-Source ASIC Design:``` OpenLane is designed to democratize the ASIC design process by providing open-source tools and methodologies. It aims to reduce the barriers to entry and enable more people to design custom integrated circuits.


- Main Goal:
  - Produce a clean GDSII with no human intervention (no-human-in-the-loop)

- Clean means:
  - No LVS Violations
  - No DRC Violations



### StriVe SoC Family

<img width="246" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/2cc4a4ae-1d0f-43a7-a281-f53cd835f9e0">

### OpenLANE ASIC Flow

![image](https://github.com/JBavitha/pes_pd/assets/142578450/d8db7b57-d549-4f66-af91-795a2df28fc2)

### Design For Test (DFT)

- Scan Insertion
- Automatic Test Pattern Generation (ATPG)
- Test Patterns Compaction
- Fault Coverage
- Fault Simulation

### Physical implementation 
- Also called automated PnR (Place and Route)
  - Floor/Power Planning
  - End Decoupling Capacitors and Tap cells insertion
  - Placement: Global and Detailed
  - Post placement optimization
  - Clock Tree Synthesis (CTS)
  - Routing: Global and Detailed

### Logic Equivalence Check

- Every time the netlist is modified, verification must be performed
  - CTS modifies the netlist
  - Post Placement optimizations modifies the netlist
- LEC is used to formally confirm that the function did not change after modifying the netlist

### Dealing with Antenna rules Violations
- When a metal wire segment is fabricated, it can act as an antenna.
  - Reactive ion etching causes charge to accumulate on the wire.
  - Transistor gates can be damaged during fabrication.
** Two solutions : **
- Bridging attaches a higher layer intermediary
  - Requires Router awareness (not there yet!)
- Add antenna diode cell to leak away charges
  - Antenna diodes are provided by the SCL









</details>










<details>
<summary> Get familiar to open-source EDA tools </summary> 



</details>






















# Day 2 - Good floorplan vs bad floorplan and introduction to library cells
<details>
<summary>  Chip Floor planning considerations </summary> 


</details>



















<details>
<summary>   Library Binding and Placement </summary> 



</details>







































<details>
<summary>  Cell design and characterization flows </summary> 



</details>




















<details>
<summary>  General timing characterization parameters </summary> 



</details>
