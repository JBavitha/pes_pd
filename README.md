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

```
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan

```

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

``` run_floorplan```

<img width="603" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/2625fa1d-1a38-4032-aaf0-0fd8fc65e88d">

### Review floorplan layout in Magic

```
magic -T /home/nickson/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged. lef def read picorv32a.floorplan.def & 
```

<img width="926" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/0f85eb87-7e1f-4001-8c04-840ab4209ca2">

<img width="722" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/f645881b-bbdb-4204-8a9e-311185d70a1b">

- Select **S** to select the layout press **V** that will fit layout on the screen 

<img width="390" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/f70e2a0a-dcaf-4ef7-9fe5-9c27fc238960">


</details>


<details>
<summary>   Library Binding and Placement </summary> 


### Netlist binding and initial place design

**Placement and Routing**

- The most important step in placement and routing is to bind the netlist with the physical cells


<img width="583" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/981d964b-437e-4414-a9a0-7b511d25b8a8">


- The library also holds the information of each logic gate like delays and etc,the library can be classified into either 2 types one that holds the shapes and one that holds the information of each logic gate.
The library will have the information of the shape the width and height,the delay information of each and every cell and the required condition of the particular cells.

<img width="595" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/53b5f1a0-e847-4406-a551-605a94378d73">

- we now place each of the shape cells from the physical deisgn view of logic gates in a proper manner such that ther are no delay contraints,we place them in such a way that they are close to thier respective input and ouput port pins, we place them close because if FF2 was placed somewhere below and the distance from FF2 to dout1 wud be higher therby having more timing delay to communicate with the output pin.

<img width="595" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/02c35d41-c8f6-472e-b362-41198d1ab87a">


### Optimize placement using estimated wire-length and capacitance

**To solve the problem**

<img width="596" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/573d12bd-34e5-445b-b4ca-568bde354794">

- we fix this problem by placing a Repeater in between Din2 and FF1 of 2nd stage to pass on the signal thereby reducing delay and buy having loss of data,therfore whatever is told to Din2 is succesfully retained by FF1 of 2nd stage and This is called Signal Integrity.

- **Repeaters** are basically buffer that will recondition the original signal make a new signal replicates original signal and send it again in this way signal integrity is maintained.
- In the 1st stage we dont need any repeaters, Signal Integrity is based on the wire length estimation and calculation.
- SLEW is basically depended upon the value of the capacitor,higher the value of capacitor the amount of charge required to charge the capacitor will be high resulting in BAD slew.
- In stage 2 we see that the distance was far from Din2 and FF1 of stage 2,slew is basically transmission and it goes beyond the limit in the 2nd stage and resulting it in more difficulty in reaching the FF1,therfore we add some repeaters to it as shown below:

<img width="594" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/6f781280-db82-4f69-b248-2498b13c0885">

- The stage 3 is placed as shown below:
<img width="597" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/e16fef7d-56d4-4c1f-98ed-f4374029f91c">

- The stage 4 is placed as shown below:
<img width="594" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/66dabec4-5ab8-4cbb-b790-66e6f926e7b5">

### Need for libraries and characterization

Typical IC design flow that every design needs to go through if it wants to be implemented on a chip are:

- 1st step is the Logic synthesis,output of logic synthesis is arrangment of gates in thier original functionality that we have described using RTL.
- 2nd step is the Floorplanning,in this step we import the Netlist that we get out of logic synthesis and decide the size of the core and die.
- 3rd step is the Placement step we take the logic cells present from the logic synthesis and place it on the chip in such a manner that the initial timing is met.(ie we place the fast ones together and the ones with different functionality we keep them depending on that).
- 4th step is the CTS(Clock tree Synthesis), if we want the clock to be spread across the logic cells at equal time (ie: all flip flops sitting far or close apart should recieve clock at the same time) therfore in CTS we attack a tree which controls the clock for each logic cells.
- 5th step is the Routing stage , if we want to route each cells there are certain flow routing has to go through and it is depended on the characteristics of the cell.
- 6th step is the STA(static timing analysis) we do static timing analysis to find out what the setup time, hold time,maximum achivable frequency of circuit.

<img width="318" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/a35bb65e-2c28-4710-bdcf-6292c934495a">


From all these steps we see that there is one thing common and that is the Gates oR cells ,this is where Library characterization plays and imporatant role,the collection of these cells is known as library when placed in some area. we introduce these gates in a manner such that the tools understand what these gates are, we need to model them in a way that the EDA tools can understand it.

### Congestion aware placement using RePlAce

```run_placement```

<img width="591" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/dd1e9bb0-6ffa-406e-a9bd-b70f96269768">

<img width="599" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/507d9e1c-aa7c-4f29-bf2d-3932574245c1">

<img width="579" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/f567f29a-9e3e-4819-a876-ed1ab412e3ba">

</details>


<details>
<summary>  Cell design and characterization flows </summary> 

### Inputs for cell design flow

- The cell design flow involves the systematic creation and enhancement of discrete digital logic cells that constitute a standard cell library. Within these libraries, there exists a collection of pre-designed, characterized, and recyclable components, such as logic gates and flip-flops, fundamental for building integrated circuits. These libraries encompass various essential elements, including PDK, DRC, and LVS rules, SPICE models, as well as user-defined specifications. These user-defined specifications, such as pin placement and gate length parameters, are incorporated into the library by the library developer.
![image](https://github.com/ani171/pes_pd/assets/97838595/28ef7c44-3535-46f7-a45b-3f99c5f3f5a8)
![image](https://github.com/ani171/pes_pd/assets/97838595/be1e9c0e-feff-4110-8e49-5f6ed92008ac)

### Circuit Design

- Circuit Design Phase: In this initial phase, we begin by implementing a specific function using a combination of NMOS (N-type Metal-Oxide-Semiconductor) and PMOS (P-type Metal-Oxide-Semiconductor) transistors. Subsequently, we create a network graph that represents the interconnections between these transistors. From this graph, we derive Euler's path, which serves as a crucial aspect of the design. Additionally, we construct a stick diagram that visually represents the physical layout of the circuit based on the graph.
![image](https://github.com/ani171/pes_pd/assets/97838595/668f9253-50d7-4ab0-9c1d-0dc5fe59353e)

- Layout Design Phase: Following the stick diagram, we proceed with the layout design, adhering to Design Rule Check (DRC) rules to ensure manufacturability. This phase involves accurately converting the stick diagram into a layout that meets the specified DRC constraints. Furthermore, we extract parasitic elements, such as resistances and capacitances, from the layout. This information is then compiled into an extracted spice list.
![image](https://github.com/ani171/pes_pd/assets/97838595/5f88c636-0802-40f7-af0e-6126dbcfb546)
![image](https://github.com/ani171/pes_pd/assets/97838595/51e5811f-39af-4b3c-9118-2d7356573c01)

- Characterization Phase: In this step, we focus on characterizing the circuit's performance in terms of timing, noise, and power. We begin by importing the necessary models and technology files. Using this information, we generate an extracted spice netlist that reflects the circuit's behavior. Subsequently, we read subcircuits and integrated power sources into the design. We also apply a stimulus to the characterization setup, introduce required output capacitance loads, and provide the essential simulation commands to thoroughly evaluate the circuit's behavior under various conditions.
![image](https://github.com/ani171/pes_pd/assets/97838595/4a2c4af9-4a7f-4667-9703-09179ae4ca74)

This process involves transitioning from the initial logical representation of the circuit to its physical layout, ensuring adherence to design rules, extracting parasitic effects, and ultimately characterizing its performance through simulation and analysis.
- We have the description of this buffer as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/b2490d1e-9190-443b-bb6a-c3bd093f25eb)

- For this, we have spice extracted Netlist basically whatever we have in the Layout buffer that contacts the metal layers, and everything for each element will have a resistance and capacitances we have extracted them all in terms of a spiced Netlist as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/1be3c9ff-c613-4763-a08c-59ba00559250)

- We have the sub-circuit file loaded, it contains the actual PMOS and NMOS models as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/581fcb78-4102-43e1-a0ef-2a26d4b9f99e)

- The industry-standard characterization flow comprises several key steps
1. Model Reading: The initial step involves reading the models, which are the first files received from the foundry.
2. Extracted Spice Netlist Reading: Next, we read the extracted spice netlist, which provides an essential representation of the circuit.
3. Behavior Recognition: In this stage, we identify and characterize the behavior of the buffer or logic gate that has been implemented.
4. Loaded Subcircuit File Reading: We proceed by reading the loaded subcircuit file to integrate the necessary components.
5. Power Source Attachment: Essential power sources are attached to the circuit to ensure proper operation.
6. Stimulus Application: Stimulus is applied to initiate and observe the circuit's response.
7. Output Capacitance Variation: Output capacitance is adjusted within a specified range to assess circuit performance under different conditions.
8. Simulation Commands: Crucial simulation commands are provided to simulate and evaluate the circuit.
- These eight steps are typically consolidated into a configuration file that is input into the characterization software, known as GUNA. GUNA performs comprehensive characterization, generating separate timing, power, noise, and .lib (library) files. As a result, characterization is further subdivided into timing, power, and noise characterization processes.



</details>

<details>
<summary>  General timing characterization parameters </summary> 

- By examining the descriptive image of the buffer during characterization, we gain insights into various threshold points within the waveform. These points are referred to as "Timing Threshold Definitions." Below, you can find the timing thresholds for the depicted image.
- The output of the waveform looks like this shown below:
  
![image](https://github.com/ani171/pes_pd/assets/97838595/c59122ae-54ae-4352-94b4-d20560d13572)

- The waveform presented above is designed to provide insights into the slew rates of the signal. The red graph represents the rising slew, while the blue graph illustrates the falling slew, with distinct high and low values for each. Additionally, similar representations are available for input rise and fall as well as output rise and fall, with the input rise and fall depicted below.

![image](https://github.com/ani171/pes_pd/assets/97838595/587ed7c7-3982-4bd8-aa90-418583f675cf)

- The output rise and fall is shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/3865300c-c92a-460d-9063-2d70a2d6a4fb)

- Timing threshold definitions

![image](https://github.com/ani171/pes_pd/assets/97838595/ffbbe4be-4138-40a7-8fba-d40cb45d9405)

- Propagation delay: The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value.
```
Propagation delay=time(out_fall_thr)-time(in_rise_thr)
```
![image](https://github.com/ani171/pes_pd/assets/97838595/afe8aa07-d711-4422-a60d-0a58f4db33c7)
![image](https://github.com/ani171/pes_pd/assets/97838595/ade0f4eb-d796-4405-94cc-9ef8a12eed0a)

- Transition Time: The time it takes the signal to move between states is the transition time, where the time is measured between 10% and 90% or 20% to 80% of the signal levels.
```
Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)
```
```
Fall transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
```
![image](https://github.com/ani171/pes_pd/assets/97838595/cb5f8e16-e0f0-476a-a6c6-f20e5094b87f)

</details>


# Day 3 - Design library cell using Magic Layout and ngspice characterization

<details>
<summary>Labs for CMOS inverter ngspice simulations</summary>

- The IO Placer revision process in Place and Route (PnR) is an iterative workflow, allowing for adjustments to environment variables as needed. One example is the flexibility to modify the pin configuration within the core area, transitioning from an initially evenly distributed placement to an alternative arrangement when necessary.
![image](https://github.com/ani171/pes_pd/assets/97838595/80426bdf-8c04-4fe3-b43e-93bdabbeab56)
- Here in the above image we see that all the I/O pins are located at output equidistant of each other.
- to view the floorplan mode we can go to `floorplan.tcl`
![image](https://github.com/ani171/pes_pd/assets/97838595/9465ae6a-b61f-489a-b72f-ca078c7e2cf7)

- After making modifications to the run floorplan by changing the mode to 2, the resulting layout features a structure in which the I/O pins are positioned in a stacked configuration, meaning they are arranged vertically, with one pin directly above another. This stacking arrangement can be useful for optimizing space utilization and improving signal routing efficiency in the design.

![image](https://github.com/ani171/pes_pd/assets/97838595/0e024cb4-1a88-4ae1-a83d-f86f987b9e79)

### Lab steps to git clone vsdstdcelldesign

- During this lab session, our task involves utilizing Git to clone document files associated with PMOS and NMOS spice models. Subsequently, upon performing the Git clone operation, a VSD standard cell design file will be generated within OpenLane.
- Cloning repository
```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
<img width="597" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/759da788-9961-4ce2-bf95-2207413911f7">
- To obtain the layout
```
magic -T sky130A.tech
magic -T sky130A.tech sky130_inv.mag &
```
<img width="847" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/dc37cc29-3a6d-4a25-96d7-e1fd18788faa">


</details>


























# Day 4 : Pre-layout timing analysis and importance of good clock tree

<details>
<summary>Timing modelling using delay tables</summary>

### Lab steps to convert grid info to track info

- Guidelines to follow while making standard cell set
  - input and output port must lie on the intersection of the vertical and horizontal tracks
  - the width of the standard cell should be odd multiple of the track pitch and height should be odd multiple of vertical pitch
 
- Tracks are used during routing stage 

<img width="564" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/7c98d580-457a-43cb-8de0-2787af698303">


<img width="89" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/01767b64-7258-454b-a92b-87c988eee5ec">

- press g : grids get activated

<img width="488" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/5c74e8df-e186-433b-a91a-2fef695e6b37">

<img width="582" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/889f335e-cf68-42a4-af67-2a6eb811f5cb">

###  Lab steps to convert magic layout to std cell LEF

- To generate the cell LEF file from Magic first we save the modified layout and then we open the file and extract LEF we type the command in the tkcon window

```
save sky130_vsdinv.mag
```
```
magic -T sky130A.tech sky130_vsdinv.mag
lef write
```
- width of the standard cell should be in the odd multiple of X pitch

<img width="801" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/c95e5203-8da0-4a62-9570-078b60d9f46e">

<img width="185" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/399865b1-665f-40e4-8007-4f2022481825">

### Introduction to timing libs and steps to include new cell in synthesis

- We copy the lef file created and the sky130 library that to the src folder of picorv32a folder.

<img width="656" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/b465765d-d484-4974-a54e-c76daabf344d">

<img width="559" alt="image" src="https://github.com/JBavitha/pes_pd/assets/142578450/ecad975d-8acc-4f96-bee0-f385f183d389">








