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





</details>










<details>
<summary> Get familiar to open-source EDA tools </summary> 



</details>
