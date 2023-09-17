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
  
### OpenLANE directory structure in detail 

<img width="416" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/264589dd-a16d-43ba-a23b-0df5ac663015">

<img width="482" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/0a6630d8-6ea6-4ab1-9c62-b90278e4568e">

<img width="518" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/b95fc4be-0d02-4770-89d4-014e63c3bcc8">

- skywate-pdk : contains all pdk related files.
- open_pdks : set of scrips and files that converts foundry level pdks to be compatible with open source pda tools.
- sky130A : It is a variant of pdk.
- libs.tech : specific to technology
- libs.ref : specific to tools

### Design preparation steps


<img width="342" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/7753c73b-e9c1-4006-8a43-1480eca4107d">





<img width="381" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/99a8d4ab-33ba-4bda-bc7e-d54c4f40b92a">



<img width="573" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/4d7c6351-6a7b-4b71-9f64-76f8b88012bc">



``` less config.tcl ```


<img width="511" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/da96657a-8ed4-4df2-90de-76f6490a6c74">

``` less sky130A_sky130_fd_sc_hd_config.tcl ```

<img width="322" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/1b383da5-b9b3-4075-825d-b9f0c61d8c5e">

**Design setup stage**

<img width="601" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/64294755-5b46-4b77-8d84-0a9aed67bf8a">

### Review files after design prep and run synthesis

<img width="522" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/c4dfe649-c06a-427b-8dc8-dfa1018c6503">


``` less merged.lef ```

<img width="430" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/43a7480d-6ccd-4742-8c3d-df4e7914ce96">

``` less config.tcl ```

<img width="605" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/422c65b3-b2bd-41aa-987e-fcd3c6ce497e">

**Synthesis results**

<img width="173" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/4688d9eb-88f6-429e-b01a-ce15b8299151">

``` No of cells =```14876
``` No of dff = ``` 1613
``` flop ratio=``` 0.108


``` less picorv32a.synthesis.v```

<img width="601" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/4de900cb-ecf8-4431-b775-78921198feac">


</details>


# Day 2 - Good floorplan vs bad floorplan and introduction to library cells
<details>
<summary>  Chip Floor planning considerations </summary> 

### Utilisation Factor and aspect ratio

**How do we find W and H ??**

<img width="416" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/88e3af4a-aa59-4e7d-811f-6188bae9a3a6">

**Lets take an example**
- we begin with a simple netlist takiing two D flip flips,aka launch flop and the capture flop with a simple combinational logic between them.

<img width="448" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/092f2da8-868b-4b05-802c-c729f6504d63">

-  convert it into physical dimension.
<img width="417" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/d1954fa7-ca86-4012-b785-d9daf431da7c">

- give some unit area for the each logic gate as shown below:
<img width="579" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/bf87bf69-f41c-4d86-8022-9e2555b72e96">


- we implment this die multiple times on the silicon wafer to increase the throughput.
- when we implment the logic into the core,the logic cells occupied 100% of the core,thereby occupying Utilising 100% of the core.

<img width="582" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/658e9ab3-8fe3-450d-8558-70882c27fe71">

- To find Utilisation factor :
<img width="248" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/66c9259d-b660-4408-bcf0-96e1eb7c1d14">

- Here in our example *Utilisation factor* is 1

- Aspect ratio :
  - aspect ratio refers to the ratio of the width to the height of a transistor. It is a critical parameter in the design and fabrication of integrated circuits.
- Here in our example aspect ratio is
<img width="247" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/e8805a35-eeab-4d2a-9f48-665bad085a51">

- Whenever the aspect ratio is 1 it signifies that the chip is a square shaped chip.when the aspect ratio is other than 1 then it signifies that our chip is rectangle in shape.


### Concept of Pre placed cells

<img width="547" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/afe3334d-9e9d-4da0-9d79-a1d25c2c9a71">

<img width="269" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/d4253952-e03f-492a-ab42-e8287c4042dc">

- separate the two blocks as two different IP's and modules.
- we can implment this one time and can be REUSED multiple times.


<img width="455" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/065fc0b8-5d35-4991-a728-c03119f80bcd">

<img width="458" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/c54354a9-ce00-46fe-a42a-06faace90217">

### De-coupling capacitors

- Decoupling capacitors are a fundamental tool in ensuring the reliable and noise-free operation of digital circuits and ICs. Properly selected and placed decoupling capacitors can help prevent signal integrity issues, reduce electromagnetic interference (EMI), and improve the overall performance and reliability of electronic systems.

<img width="577" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/b2a968d9-b686-4b3a-8cc1-46e24a69d4fe">

- If Vdd' goes below the noise margin, due to Rdd and Ldd, the logic '1' at the output of circuit wont be detected as logic '1' at the input of the circuit following this circuit.
<img width="462" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/87f2781e-2052-4a53-b557-ede8d9032e33">

- Having a large distance from the power supply and the main circuit has a disadvantage as there are multiple voltage drops happening before it reaches the main circuit giving a less voltage at the main circuit due to voltage drops therefore we cannot gaurantee that our logic gates in the circuit are getting either a high voltage(logic 1) or a low voltage(logic 0) or a danger region or gray region(Either Logic can go to 1 or 0 giving high or low volts) hence we have a disadvantage of Voltage being far from our circuit design.

- To solve this we use Decoupling Capacitors
  - they are huge capacitors completely filled with charge,therefore if our main voltage is source is 1v our deocupling capacitors also get charged to 1V.

<img width="579" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/1c574b07-a6b5-452a-bce9-6921a89db806">

- surround the preplaced cells with the decoupling capacitors in order to keep the current flow as required without any problems of voltage drops.thereby ensuring each preplaced cells are getting the supply from the Decoupling capacitors.

<img width="415" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/c2bee96c-6677-4295-913a-1d2ba3b720fa">

### Power planning

- Power planning involves the careful management of power distribution, delivery, and consumption in an IC to ensure its proper functioning and efficiency.

<img width="322" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/8e51df59-d182-46ef-96b3-a230f46be2ab">

- Consider the above circuit which we used for decoupling capacitors and convert it into a Macro,now this Macro is repeated multiple times on the chip creating a current Demand for each and every element of the particular macro.Now suppose one is driver and other is loader each macro have a decoupling capacitors and we need to send signal from driver to load, we need to make sure the particular line between the driver to load maintains the same particular signal.

<img width="432" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/5749c54e-6071-46a7-b5f0-881e67c62d1b">

- The line between the driver and load should get the necessary power from the power supply as decoupling capacitors cannot be placed in between therfore having a possibility of voltage drop as the power supply is far from the signal line.
- Hence we consider a 16 bit bus connected to an inverter when we pass the logic to the inverter the output will be inverted value of the input therfore all the capacitors charged to logic 1 are now dischraged to Logic 0 and vise versa.

<img width="453" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/7ab5589a-5f16-4b9d-9d2c-bf5a26820f51">

<img width="437" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/a137db98-0906-43ff-9eb4-86599a10993a">

- when all the other capacitors charging from Logic 0 to logic 1 in that case all these capacitors are demanding for supply from the main power supply at the same time and we have a single voltage line for all the capacitors hence we get a Voltage Droop

<img width="440" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/e6da813d-05d5-49f1-959d-72274e1e4410">

- We put multiple power supplies instead of single one by creating multiple vdd and vss lines,therby giving any power supply demand to the circuit.
**The power planning structure**

### Pin placement and logical cell placement blockage

- Pin placement, also known as I/O (Input/Output) pad placement, refers to the process of determining the locations and arrangement of input and output pins on an IC or PCB. These pins are used to interface with external devices or other components.
<img width="443" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/bb5f3c42-4a93-4410-9d14-c88622057eeb">

- lets take 2 more designs but both are driven using different clocks with a common pre placed cell as shown below:

<img width="465" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/932631eb-512c-416a-828a-6246dcfffd82">

<img width="471" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/08172ee4-f587-43b3-aa68-f303b8875487">

- Clock 1 and clock 2 drive the complete chip.

**Pin Placement**
<img width="520" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/16360952-d320-4093-a941-8530898cf0d4">

- After Pin placement we make sure that none of the automated placement and routine tool doesnt place any cells in the particular area that the gaps between each clock ports,the area should be blocked for placement and routine tool,hence we do logical cell placement blockage.
<img width="508" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/e5af433c-d0e8-4bb0-ac80-1001a2fc3b04">

### Steps to run floorplan using OpenLANE
```less README.md``` 

<img width="445" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/058b0ac3-e49c-4156-85ed-c4ed25e16294">

<img width="602" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/6b57fa7b-2e10-4e81-a789-da194f097950">

```less floorplan.tcl```
<img width="335" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/720fd7a2-2c16-4c3e-a465-c8c444dab7ba">
















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
