# RISC-V-tapeout-Program-Week-6
Lets's Forwarding to the RISC-V , Week 6 is the Physical design workshop where we learn the interactive flow from RTL to GDS.

### VDI IMAGE
Firstly download th zipped file of openlane : 

https://vsdlabs.sgpl.cdn.digitaloceanspaces.com/vsd-labs/openlane.zip

Now to open an VDI image use an oracle virtualbox and create a new machine with name vsdworkshop.

### DAY 1: Inception of Open-Source EDA, OpenLANE and sky130PDk

* Introduction to QFN-48 package, chips, pads, core, die and IPs.

     - QFN is a quad flat no lead package.
     - Pads are the coonections from which we can send the signal inside the chip.
     - Core is the place where all logic are present.
     - Die is the size of entire chip. It is present at the centre.

<img width="895" height="805" alt="Screenshot 2025-10-29 090638" src="https://github.com/user-attachments/assets/2c6876d7-0c50-457b-b031-2beb9f585ee1" />
<img width="1194" height="788" alt="Screenshot 2025-10-29 090815" src="https://github.com/user-attachments/assets/9994adc1-ce7f-44cc-8459-148ff565c8de" />

RISC V: It consists of SRAM,SOC,ADC,DAC,SPI these all are called foundary IP's.All devices depends upon foundary where all chips are fabricated using deposition and lithography techniques and so on.

<img width="890" height="800" alt="Screenshot 2025-10-29 090830" src="https://github.com/user-attachments/assets/9f0c88c7-54b2-4655-8139-e5854d33e213" />

* Introduction to RISC-V
RISC-V, where five refers to the number of generations of RISC architecture that were developed at the University of California, Berkeley. RISC is an open standard instruction set architecture (ISA) based on established RISC principles. Unlike most other ISA designs, RISC-V is provided under open source licenses that do not require fees to use. A number of companies are offering or have announced RISC-V hardware, open source operating systems with RISC-V support are available, and the instruction set is supported in several popular software toolchains.

The instruction set is designed for a wide range of uses. The base instruction set has a fixed length of 32-bit naturally aligned instructions, and the ISA supports variable length extensions where each instruction can be any number of 16-bit parcels in length. The instruction set specification defines 32-bit and 64-bit address space variants. The specification includes a description of a 128-bit flat address space variant, as an extrapolation of 32 and 64 bit variants, but the 128-bit ISA remains "not frozen" intentionally, because there is yet so little practical experience with such large memory systems. Chip is connected to the package with the help of bond wires.

ISA in shortly is the language through which we can talk to computers.
<img width="1454" height="819" alt="Screenshot 2025-10-29 091117" src="https://github.com/user-attachments/assets/5fbd6b5f-a990-4941-b1d4-e274cb6daba9" />

* From Software applications to Hardware
Here we'll learn how applications runs in system. Fiven below is the basic flow.
<img width="1770" height="1079" alt="Screenshot 2025-10-29 091952" src="https://github.com/user-attachments/assets/bd9f20e9-378f-49e3-bb25-718dc88288a8" />

The applications first interact with the system software and then goes at the hardware level. System software consists of Operating system, compiler, assember. System software 

  - Operating System: It is used to handle the IO operations, to allocate memory and for low level system functions. OS produces output in the form of C, C++, Vb, JAVA. This output is taken by compiler.
  - Compiler: Compiler takes the output of OS as input and produces output in the form of instruction *.exe file.
  - Assember: Assember takes the instructions given by compiler into the binary language. This is then fed to the hardware and used to generate the flow. There is an Abstract interface between software and hardware called ISA or architechture of computer.

<img width="1197" height="712" alt="Screenshot 2025-10-29 092827" src="https://github.com/user-attachments/assets/97f3af97-d4f2-4546-a718-a21a66e37ac0" />


* Introduction to all components of Open-Source Digital ASIC Design

Digital Asic design needs RTL IPs, EDA tools and PDK data. 
- RTL: RTL stands for register transfer level which is the design abstraction models a synchronous digital circuit in terms of the flow of digital signals (data) between hardware registers, and the logical operations performed on those signals.for this designs many open sorces are available. like, librecores.org, opencores.org, github.com, etc
  
- EDA tools: The term Electronic Design Automation (EDA) refers to the tools that are used to design and verify integrated circuits (ICs), printed circuit boards (PCBs), and electronic systems, in general. many open sorces tools are available like Qflow, OpenROAD, OpenLANE, etc.

- PDK: PDk stands for process design kit. IIt is basically a interface between the FAb and design. It is a collection of files used to model a fabrication process for the EDA tools used to design an IC. Process dresign rules involves the DRC, LVS, PEX. It also consists of device models, digital standard cell libraried and IO libraries.

<img width="923" height="979" alt="Screenshot 2025-10-29 094242" src="https://github.com/user-attachments/assets/36cd6079-e63f-416c-a031-2f177a4d4c26" />

* RTL to GDS Flow: 
<img width="1705" height="674" alt="Screenshot 2025-10-29 094918" src="https://github.com/user-attachments/assets/9c19591c-4de8-4dde-98a1-2f2c3ff729e3" />

- Step 1: Synthesis:  In the synthesis, the design RTL is translated to a circuit out from the SCL. The resultant circuit is describes in HDL and usualy refered to the gate level netlist. the gate level netlist is functionaly equivelent to the RTL.
- Step 2: Floor/Power Planning: In the floor planning the chip is partition into different building blocks and the IO pads are placed. In macro floor planning we define the dimensions, pin locations and rows dimensions. In Power plaaning the supply of VDD and GND is connected to the IO pads wherever needed.
<img width="1160" height="420" alt="Screenshot 2025-10-29 095616" src="https://github.com/user-attachments/assets/f8526a2d-454e-4131-98cd-96d8acbcb7dd" />
<img width="649" height="351" alt="Screenshot 2025-10-29 095632" src="https://github.com/user-attachments/assets/9f7725ac-f7ae-4692-9995-371faa7a1811" />

- Step 3: Placement: In this process, the the cells are placed on the floorplan rows and are aligned with the sites. It is done in two steps:

        - Global Placement: It is the rough placement that may violate the other constraints.

        - Detailed Placement: Here we determine the exact route and layers for the netlist. Its objective of this is valid routing, minimizing the wirelength and meeting the timing constraints.

- Step 4: Clock Tree Synthesis:  Before routing the signals, we have to route the clock. In the process of clock synthesis, we have distribute the clock to the every sequential elements. for example flipflops, registers, ADC, DAC ete. Synthesization should be done in a manner that with minimum skew and in a good shape.To minimize the clock skew by using the low-skew global routing resources for clock signals.Microsemi devices provide various types of global routing resources that significantly reduce skew. Usually a tree is a H tree, X tree etc.

- Step 5: Routing: After routing the clock, the signal routing comes. Making physical connections between signal pins using metal layers are called Routing. Routing is the stage after CTS and optimization where exact paths for the interconnection of standard cells and macros and I/O pins are determined. There are two types of nets in VLSI systems that need special attention in routing: Clock nets Power/Ground nets

The sky130 PDK defines the 6 routing layers. the lowest layer is called local interconnect layer (titanium nitride layer). Other five layers are alluminium layers. In the proccess of routing, metal trackes forms a routing grids and these grids are huge. so, devide and conquer approach is use for routing. The two types of routing is used:

      - Global routing: Generates the routing guides

      - Detailed Routing: Uses the routing guides to implement the actual wiring.

<img width="1012" height="399" alt="Screenshot 2025-10-29 100008" src="https://github.com/user-attachments/assets/a1e80585-9655-417b-b7bc-8d3f8f93a8a3" />

- Step 6: Hence we obtain the final layout which goes under several verification. Two types of verifications are performed i.e physical verification which checks the DRC and LVS whereas timing verification which is used to perform the STA (static timing analysis).


* Introduction to OpenLANE
OPENLANE is an automated RTL to GDSII flow that is composed of several tools such as OpenROAD, Yosys, Magic, Netgen, Fault, CVC SPEF-Extractor, CU-GR, Klayout and a number of scripts used for design exploration and optimization. It is started as an Open-source flow for a true Open Source tape-out Experiment. Strive is a family of Open everything SOCs like Open DK, Open EDA, Open RTl etc.
<img width="1096" height="810" alt="Screenshot 2025-10-29 100613" src="https://github.com/user-attachments/assets/ae40e9d6-90ab-4ed5-98f7-baff738cf15d" />

The Main goal of openlane is to provide clean GDSII with no human intervention. Here clean means no DRC, LVS, timing Violations. Openlane is tuned for skywater 130nm open PDK. It also supports XFAB180 and GF130F. It can be used to harder i.e generating final layout (GDSII) of m=macros and chips.

Its has two modes of operations:
    i) Autonomous: It is a push buttom flow.
    ii) Interactive: It is used to generate the flow step by step.

* OpenLANE detailed ASIC FLow

<img width="1194" height="649" alt="Screenshot 2025-10-29 101150" src="https://github.com/user-attachments/assets/8199e171-0052-4911-9917-1efda10e6c4a" />

     - Synthesis exploration: It gives detailed report of delay and area affected by synthesis.
     - Design exploration: It is used to sweep the design configuration. It is used for regression testing.
     - DFT (Design for Test): It perform scan insertion, ATPG, test patterns compaction, fault coverage and fault simulation. 
     - Physical Impllementation: It is also called Automated PnR i.e Place and Route. It is done using OpenROAD. It invloves:
                    Floor/Power planning
                    End Decoupling cappacitors and tap cells insertion
                    Placement: Global and Detailed
                    Post placement Optimization
                    Clock tree synthesis (CTS)
                    Routing : Global and Detailed

     - Logic Equivalence checking (LEC): It is done using yosys. Everytime the nestlist is modified verification must be performed. CTS, Post placement optimizations modifies the netlist. LEC is used to formally confirm that the function didnot change after modifying the netlist. 
     - Dealing with Antenna: When metal wire segment is fabricated it can act as an antenna. It occurs when the reacitve ions etching causes the charges to accumulate on the wire or the transisotr gates get damage during fabrication. There are two solutions for this: 

           i) Bridging: It attaches a high layer intermediately. This technique requires router awareness.
<img width="625" height="435" alt="Screenshot 2025-10-29 102325" src="https://github.com/user-attachments/assets/7f252171-beb4-49e8-8f7e-313724563736" />

           ii) ADD antenna diodes cells to leak away charges. Antenna diodes are provided by SCL.
<img width="1095" height="297" alt="Screenshot 2025-10-29 102438" src="https://github.com/user-attachments/assets/a8f462e9-5b10-43ff-8620-aec10d961e06" />

We took a preventive approach by adding a fake Antenna diode next to every cell input after placement. Run the antenna checker (magic) on the routed layout. If the checker reports a violation on the input pin, then replace the fake diode cell by the real one.

   - Static timing Analysis (STA): It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. Resulting report will shows the timing violations if any violations is there.
   - Physical Verification: It involves the DRC and LVS. MAgic is used to for DRC and Spice extraction from layout. MAgic and Netgen are used for LVS.


* OpenLANE Directory Structure
Open the OpenLANE and open the working directory: 

<img width="880" height="777" alt="unnamed" src="https://github.com/user-attachments/assets/f9f62bc9-26f8-4dcc-91f2-cdaf5d3caac5" />

  * /Desktop/work/tools/openlane_working_dir/openlane

  * docker

  * ./flow.tcl -interactive : This command is used to run the complete flow of RTL to GDS step by step.

  This opens the prompt of openlane. Now we have to input all the packages which required to run the flow.

  * package require openlane 0.9
<img width="733" height="763" alt="unnamed" src="https://github.com/user-attachments/assets/b9624d17-084a-4c50-8fc8-d5eccc9566f2" />

  * prep -design picorv32a : This command is used to prepare the design stage.

<img width="1644" height="778" alt="unnamed" src="https://github.com/user-attachments/assets/d0c67e8f-5b8e-4b72-a0b2-74094f08672e" />

This preparation stage created the runs folder in the picorv32a. This command also contain the config.tcl file which contain the all the defaults value. Design folder in the openlane directory also contains the config.tcl, src where we find the verilog file and sdc file. This config.tcl contains the every details about the design like the clock period, clock period port etc.

In openlane default value is fixed, then in the config.tcl and then in sky130_fd_hd_config.tcl. Highest priority is gien to sky130 config.tcl file
<img width="1009" height="370" alt="unnamed" src="https://github.com/user-attachments/assets/77237056-8977-4981-9f2e-4a2e9b18ab81" />
<img width="648" height="191" alt="unnamed" src="https://github.com/user-attachments/assets/2b0b7596-4718-4d31-9573-1489fc62a9cb" />

Merged.lib file contains all the information of cell lib and tech lib.

<img width="711" height="816" alt="unnamed" src="https://github.com/user-attachments/assets/afcb3ed3-962c-4fb3-bbac-87c1ced587e1" />

<img width="1075" height="797" alt="unnamed" src="https://github.com/user-attachments/assets/73dfab40-f5e7-4f48-9564-6691a8b3a90f" />

After the prepapration step and the reviews of the file generated now go for the synthesis step.

  * Synthesis: run_synthesis
<img width="1814" height="818" alt="unnamed" src="https://github.com/user-attachments/assets/5dc6bf31-5bac-4989-b017-fd56bdbcbb01" />
<img width="692" height="817" alt="unnamed" src="https://github.com/user-attachments/assets/9ab2d325-4666-4286-b1bb-d0418a9538e6" />
<img width="609" height="645" alt="unnamed" src="https://github.com/user-attachments/assets/8b6a779c-5ed7-47eb-bd29-6104fd891caf" />

Flop ratio is calculated as: Number of D flip flop/ Total number of cells

Here number of D flip flops are : 1613 and total number of cells are : 14876 so the flop ratio is : 10.84%

The synthesized file created is : 
<img width="1857" height="816" alt="unnamed" src="https://github.com/user-attachments/assets/b321f2aa-eddd-40db-a9bb-0b298ae202d2" />

We can also check the timing report which will be present in reports directory of picorv32a folder named as 1-yosys_4.stat.rpt and also the opensta timing report.
<img width="479" height="806" alt="unnamed" src="https://github.com/user-attachments/assets/abcb607e-0498-45a1-8acd-79613f35517b" />

<img width="721" height="818" alt="unnamed" src="https://github.com/user-attachments/assets/a76e803f-f585-4cf0-b6fc-df11ac571423" />

### DAY 2: Good floorplan and Bad floorplan and Introduction to Library cell

* Chip Floor Planning Considerations:

1. Define the Width and Height of core and die: Consider two flip flops and standard cells. Let's standard cell have the dimensions 1unit*1unit so its area is : 1 sq. unit.
<img width="1278" height="1034" alt="Screenshot 2025-10-29 221243" src="https://github.com/user-attachments/assets/4d1a238c-eaa9-4083-91a7-1d5c60a892fd" />

A core is the section of the chip where fundamental logic of design is placed. A die is the area which consists of core. It is a small semiconductor material specimen on which fundamental circuit is fabricated. We need to place all the logic inside the core. 

Utilization factor and Aspect ratio are given as :
<img width="732" height="259" alt="Screenshot 2025-10-29 222153" src="https://github.com/user-attachments/assets/593a05a9-edaf-4e16-b298-bc4dfbfdaae0" />
If utilization factor is 1 then it means all the area is occupied. Ideally we go for 50-60%. Whereas if aspect ratio is 1 it means chip is of square size.

for example : If utilization factor= 0.25 it means out of the whole chip area only 25% area is utilized by the netlist and 75% is available for additional cells.

2.  Preplaced cells : Consider a large combinational circuit having large function so we'll divide the cirucit and separately implement the two blocks. In both the blocks lets extend the input output pins and now we will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. Now we'll seperate them out as two different IP's or modules.

This makes it easier to use them multiple times in the design. The arrangement of these IPs in the chip is referred to as floorplanning. These IP's blocks have user-defined locations and hence are placed in chip before automated placement and routing and are reffered to as pre-placed cells. Automated placement and routing tools places the remaining logical cells in the design onto chip.
<img width="1349" height="1012" alt="Screenshot 2025-10-29 223119" src="https://github.com/user-attachments/assets/9b40d50b-ba7c-4291-80b6-7350447e4c5e" />
<img width="1445" height="861" alt="Screenshot 2025-10-29 223754" src="https://github.com/user-attachments/assets/3d78082c-1429-4eef-965c-a056f7ef2b7a" />

3. Decoupling capacitors: We surround the preplaced cells with decoupling capacitors. Let consider some circuit, which is the part of the blocks which has been described earlier. When some gate (let consider AND gate) switched from 0 to 1 or 1 to 0, considered amount of the switching current required because of available small capacitance . This capacitor should be completely charged to represent logic 1 and completly discharged to represent logic 0. Consider capacitance to be 0. Rdd,Ldd,and Lss are well defined values. During switvhing operation, the circuit demands switching current i.e. peak current. Now, due to the presence of Rdd and Ldd, there will be a voltage drop across them and the voltage at Node 'A' would be Vdd' instead of Vdd.

<img width="1217" height="594" alt="Screenshot 2025-10-29 232008" src="https://github.com/user-attachments/assets/6305f6ae-12e9-4fa9-ad87-ed59475dc03c" />

<img width="1266" height="996" alt="Screenshot 2025-10-29 232139" src="https://github.com/user-attachments/assets/c2004e2e-be10-4bca-b709-a00e4c585d69" />
Decoupling capacitors are placed in between the block a, block b and block c. So here in this whole block it has been ensured that supply is being done by the de-coupling capacitor.

4. Power Planning: Lets consider a 16 bit bus where one particular line of 16-bit bus is logic 1 it says that the capacitor is being charged to Vdd, and whenever we say logic 0 it says that the capacitor is discharged to ground.Let consider this 16 bit bus connected to inverter. So, all the capacitor are initially charged will get discharged and vice-versa due to inverter.
This will cause a bump in 'ground' tap point during discharging. That bump is called as Ground Bounce. If the size of the bump exceeds the noise margin levelit might enter into an undefined state and due to undefined state it can either go to logic 1 or logic 0. So here thing becomes unpredictable. 
<img width="1328" height="474" alt="Screenshot 2025-10-29 233409" src="https://github.com/user-attachments/assets/33d7b136-fa07-4e8d-b6aa-b3d42db05aca" />
Also , all capacitors which were'0' volts will have to charge to 'V'volts through single 'vdd'tap point. This will cause lowering of voltage at Vdd tap point. As long as this voltage drop is in noise margin level we are good enough but if it goes into an undefined region then things become unpredictable.
<img width="1324" height="483" alt="Screenshot 2025-10-29 233521" src="https://github.com/user-attachments/assets/d18fc7fb-dfb1-4399-85be-939b7ecaa984" />

The phenomenon is occuring due to the lowering of the supply voltage,this problem occured because power has applied to one point only. The solution of the problem is use multiple power supply.
<img width="1293" height="1043" alt="Screenshot 2025-10-29 233642" src="https://github.com/user-attachments/assets/0cbb1418-d10c-4a74-b90a-e7812172a5d1" />
<img width="1650" height="1004" alt="Screenshot 2025-10-29 233835" src="https://github.com/user-attachments/assets/cd89ae93-3c33-409a-8b7a-147e776cbebc" />

5. Pin Placement: he connectivity information between the gates is coded using VHDL/Verilog language and is called as 'Netlist'. The pin is placed as per the information in the netlist.

Complete design is shown below as: 
<img width="1102" height="1005" alt="Screenshot 2025-10-29 234455" src="https://github.com/user-attachments/assets/6693ab5c-cfd9-425f-83db-a4db6dd8f7dc" />

Placement is shown as: 
<img width="1306" height="930" alt="Screenshot 2025-10-29 234635" src="https://github.com/user-attachments/assets/2355eee6-7976-4141-8b59-d4bfec061d0e" />

* Steps to Run Floorplan using OpenLANE
Before run the floorplanning, we required some switches for the floorplanning. these we can get from the configuration from openlane. The given variables are switches which are need to set for floorplan and placement. Here we can see the defualts values of the core utilization ratio is 50% and aspect ratio is 1. Here FP_PDN files are set the power distribution network.
<img width="1853" height="816" alt="unnamed" src="https://github.com/user-attachments/assets/e8c8fe27-1822-4de1-8545-fb3b3aecedd8" />

The file named "floorplan.tcl" containes the all the default values and it have the lowest priority. The data can be overridden by the data in the config.tcl or the highest priority file of sky130A...tcl. Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance.
<img width="746" height="803" alt="unnamed" src="https://github.com/user-attachments/assets/7170b9b5-1398-486b-871c-5b8c935c603b" />

After synthesis write the command in the openlane prompt:

run_floorplan
<img width="881" height="808" alt="unnamed" src="https://github.com/user-attachments/assets/44e850f9-1496-439d-ac21-7ef21d2eee7e" />

The file ioplacer.log contain the information of all input and output pins
<img width="890" height="407" alt="unnamed" src="https://github.com/user-attachments/assets/dda3914f-f331-4ad7-a8db-6413b33c2832" />

After the floorplan run the .def file is generated which contains the total die area, orientation etc. It contain the die area as (0 0) (660685 6714055) with the units in micron 1000.
<img width="891" height="693" alt="unnamed" src="https://github.com/user-attachments/assets/cb5cc864-4a3d-4771-8f5b-06bb78aa4294" />

<img width="577" height="805" alt="unnamed" src="https://github.com/user-attachments/assets/9dfa59df-c1f7-4b69-9b7f-eba860a2dc93" />

To view the actual layout use the command: 
magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
<img width="547" height="563" alt="unnamed" src="https://github.com/user-attachments/assets/e2cfde75-f2aa-4681-a6be-a2c049a75d2c" />
<img width="440" height="797" alt="unnamed" src="https://github.com/user-attachments/assets/3de5f8fe-37e0-428a-87c0-786ad49ac947" />
<img width="471" height="88" alt="unnamed" src="https://github.com/user-attachments/assets/6946629d-abc0-4df4-9dbf-8178e97b1db2" />

* Placement and Routing
Firstly bind the netlist with the physical cells. There are two types of library one is one which contain the only cells information while other contain the timing information. Next is to place the standard cells and optimize the placement using the estimated wire length and capacitance. Based on the estimated wire length we placed the buffers or repeaters. Cells are placed near to avoid the delay.
<img width="1909" height="940" alt="Screenshot 2025-10-31 070114" src="https://github.com/user-attachments/assets/51b8c522-5860-48eb-a439-cd4f4dfa7009" />
<img width="1281" height="901" alt="Screenshot 2025-10-31 071715" src="https://github.com/user-attachments/assets/8b74f21e-ec56-44fe-a1c5-b75b7da966d4" />

* Congestion aware placement using replace

Here we consider congestion as the constraints. Global placement reduces the wirelength. so our next step is to run placement. Open the openLANE prompt and type the command:

run-placement

In placement standard cells positions are fix. We can verify the placement by using placement.def file and see the layout in magic with command "magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
<img width="1430" height="527" alt="unnamed" src="https://github.com/user-attachments/assets/f0c2baca-f549-4e7e-8b4f-1d6077db07d5" />
<img width="551" height="818" alt="unnamed" src="https://github.com/user-attachments/assets/14af6597-0921-42ea-b2cc-3681bd2435fe" />

Placement in magic looke like: 
<img width="545" height="550" alt="unnamed" src="https://github.com/user-attachments/assets/3a4637c4-bc12-4a15-a728-ecd5d97093aa" />
<img width="678" height="598" alt="unnamed" src="https://github.com/user-attachments/assets/1cd27dad-97a7-44ba-8a67-6484d5f1d14f" />

* IO placer revision : We can modify the floorplan. Like instead of using the fp_Ip mode 1 we can change it to 2 by writeing the command in openLANE prompt: set:: env(fp_Ip mode) 2 and see the changes in the layout by again running the floorplan and see the layout in magic.
<img width="559" height="563" alt="unnamed" src="https://github.com/user-attachments/assets/b251a4f2-8127-457f-87ab-5c32b3c44eb0" />

* Cell Design and Characterization FLow:

Standard cells are present in the library. Library have different cells with different sizes and functionality. These different cells will have different threshold voltages.

- Cell Design flow includes the following steps:

     i) Inputs: PDKs: DRC,LVS, SPICE, user defined specs
     ii) Design steps: Circuit design, layout design, Characterization.
     iii) Outputs: Circuit description language (CDL)
  
  Circuit design involves the making of design with the library requirement and obtaining the PMOS, NMOS network grpah with euler's path and then draw the stick diagram and convert that stick diagram into the layout. The output CDL we get contains the GDSII, LEF, extracted SPICE and netlist.cir.
<img width="312" height="450" alt="Screenshot 2025-10-31 081225" src="https://github.com/user-attachments/assets/e9aa7d83-7e3c-4c09-b381-cb586a2944ad" />

- CHaracterization FLOW: It constains the extracted spice netlist and the subcircuit file contain PMOS and NMos.

         Read model files

         Read extracted SPICE netlist

         Define/ recognize the behaviour of buffer

         Read the subcircuit

         Attach the power sources

         Provide Output load capacitance

         Provide necessary simulations commands

Provide the above teps to tool GUNA which generate the timing characterization,noise, power.libs etc

* Timing CHaracterization: It contain the information of Slew, propagation delay and the transistion time.

       - Slew: It is the difference of the arrival of clock at two end points. Generally it is considered between 20-80%.
<img width="481" height="535" alt="Screenshot 2025-10-31 082810" src="https://github.com/user-attachments/assets/b52dcf9a-97ca-477b-9f95-c1099c694d0d" />

      - Propagation delay: It is calcualted as: Time(out_thr)-time(in_thr
<img width="1682" height="890" alt="Screenshot 2025-10-31 083317" src="https://github.com/user-attachments/assets/9fdc5e5f-48a8-403a-804b-8d4ddf57668f" />

     - Transition time: It is calculated as:  time(slew_high_rise_thr)- time(slew_low_rise_thr)
or 
transition time = time(slew_high_fall_thr)- time(slew_low_fall_thr)

### DAY 3: Design Library cell using MAGIC layout and ngspice characterization

* VTC Spice simuations: Here first part is to create SPICE deck, it contains the connectivity information about the netlist. It has input that are provided to the simulation and the deck points which will take the output.

Now define the component connectivity and their associated values and finally identify the nodes and name them.
<img width="1812" height="722" alt="Screenshot 2025-10-31 190601" src="https://github.com/user-attachments/assets/358986b2-15a4-46a2-9b6a-fac077b4b00f" />

CMOS is a robust device and its robustness parameters are the threshold voltage, noise margin eitc. Threshold volatge can be found by drwaing the straight line at 45 angle and wherever it will cut the curve will be the threshold voltage of the device. Switching thresold, Vm (the point at which the device switches the level) is the one of the parameter that defined the robustness of the Inverter. Switching thresold is a point at which Vin=Vout. 

CMOS VTC curve looks like:
<img width="478" height="413" alt="Screenshot 2025-10-31 191259" src="https://github.com/user-attachments/assets/dc45db02-ba86-4040-b381-7802d98463f9" />

* Lab steps to git clone vsdstdcelldesign
for the standard cell design we need to clone the given git repository:

git clone https://github.com/nickson-jose/vsdstdcelldesign.git
<img width="874" height="560" alt="unnamed" src="https://github.com/user-attachments/assets/273edbe2-04aa-427f-9224-f133729efd74" />
<img width="893" height="372" alt="unnamed" src="https://github.com/user-attachments/assets/27a0e740-d474-489d-a045-6c7e315a073a" />

Now copy the tech file from pdfsky130A/libs.tech/magic to the folder csdstdcelldesign. Now, we'll able to see the layout of the inverter in the magic.
<img width="456" height="586" alt="unnamed" src="https://github.com/user-attachments/assets/eccb4898-a1c7-4199-8013-4f1ba8e57c33" />

* Inception of Layout- CMOS Fabrication Process

- 16 Mask CMOS process:
1. Selecting a Substrate: Generally p-type substrate is used having the high resistivity with doping level 10^15 /cubic cm and orientation of 100. P-type substrate doping should be less than the newll doping.

2. Create active regions for transistors: These are the regions of PMOS and NMOS. Firstly grow 40nm SiO2 on p-type substrate and then deposits 80nm Si3N4 onto SiO2 layer. To make the pockets of transistors we need to specify where these pockets should locate. For this mask is used. Deposit 1um photoresist and then use photolithograohy and expose the substrate using mask then develop the solution and etched the remaning photoresist. Now place this in oxidation furnace of high temperature to form the isolation region. Si3N4 is used to protect the underneath region.  This process is known as the LOCOS (Local oxidation of silicon). Then Si3N4 is stripped off using hot phosphoric acid. This created the bird's beak.

<img width="1469" height="836" alt="Screenshot 2025-10-31 192230" src="https://github.com/user-attachments/assets/fe817575-2a3f-42d3-866c-46681823687a" />
<img width="1234" height="643" alt="Screenshot 2025-10-31 192349" src="https://github.com/user-attachments/assets/e1814535-a9d8-480d-b513-d5b99668ab1c" />
<img width="1250" height="570" alt="Screenshot 2025-10-31 192416" src="https://github.com/user-attachments/assets/832dadb5-0c8f-4ddf-995d-b96e4f210338" />
<img width="1232" height="518" alt="Screenshot 2025-10-31 192729" src="https://github.com/user-attachments/assets/effaa8b2-88c9-4edd-9a13-00e6f93b4746" />

3. N-well & P-well formation: Deposit photoresist and define pattern using Mask2 where pattern is to be deposited. Then expose the substrate to UV light which react with hotoresist. Remove mask and create p-well using Boron using ion implantation at 200Kev energy. Boron penetrate through the oxide and also damages the oxide layer. Similarly done for N-well by using phosphorus at 400Kev energy. Now take this susbtrate in the driving furnace for diffusion of boron and phosphorus atoms. 
<img width="1440" height="710" alt="Screenshot 2025-10-31 193024" src="https://github.com/user-attachments/assets/fdad085a-110b-49c4-adf3-3499c842099a" />
<img width="1649" height="794" alt="Screenshot 2025-10-31 193122" src="https://github.com/user-attachments/assets/1c17f31e-bea4-4dec-ac6f-8260dfceaf98" />
<img width="1280" height="645" alt="Screenshot 2025-10-31 193352" src="https://github.com/user-attachments/assets/26cc8163-f8e2-4c76-bd4a-28de7718f063" />
<img width="1429" height="834" alt="Screenshot 2025-10-31 193523" src="https://github.com/user-attachments/assets/f207b163-d671-4b7a-961a-7ce7c976a97c" />

4. Formation of Gate: Gate is used to control the threshold voltage. The equation is given as:
<img width="830" height="956" alt="Screenshot 2025-10-31 193659" src="https://github.com/user-attachments/assets/6804925d-d664-49b5-a064-ff2818cb7bbd" />
Again the Mask 4 is used to create the gate i.e photoresist,then mask,exposure and develop and then etching. Now at surface doping of boron at 60kev and similarply for newll mask 5 is used to create doping of arsenic at surface only.

Now etched the original oxide using dilute HF solution. Then regrown again and again to give high quality oxide of 10nm thin. 

For gate deposits 0.4um polysilicon layer. Gate area should be of low resistance. So it is doped with P or As for low gate resistance. Use Mask 6 and use photolithography to create the gate structure.
<img width="1277" height="844" alt="Screenshot 2025-10-31 194338" src="https://github.com/user-attachments/assets/5ab3624e-1e22-4a5c-bb8a-091276ab7311" />
<img width="1241" height="489" alt="Screenshot 2025-10-31 194422" src="https://github.com/user-attachments/assets/52fc6474-d299-4b8f-b07d-32f3e9cc5743" />

6. Lightly doped drain (LDD) formation: Two different doping are used P-/P+ and N- and N+ where - means lightly doped. These doping are required beacuse of hot electron and short channel effect. Hot electrons effect causes the breaking of Si-Si bonds abd also led the Si electrons to cross the 3.2ev of energy gap and reach the conduction band of SiO2. Whereas short channel effect causes the drain field to enters the channel. Thses effect arises due to increase in the electric field.

To creade LDD use Mask 7 and spin the photoresist and for doping in pwell use phosphorus as N- and similarly for Nwell use Mask 8 and doped with boron P-. Hence when we make actual source and drain it might affect the lighly doped regions so we need to project this region. So spaces are used by depositing the thick 0.1um Si3N4 or SiO2 then do plasma anisotropic etching i.e directional etching but here sidewalls remain. these sidewalls helps to rpevent the N- and P- regions.
<img width="1564" height="681" alt="Screenshot 2025-11-10 192305" src="https://github.com/user-attachments/assets/69a0cf3f-1b95-442a-a489-e3c09461463c" />

<img width="1574" height="693" alt="Screenshot 2025-11-10 192410" src="https://github.com/user-attachments/assets/314da40b-1e7a-4038-aad1-e88431b8b0d7" />

8. Source and Drain Formation: Mask 9 is used to create doping of Arsenic at 75keV in p well and mask 10 is used to create P+ doping in nwell at 50keV. Then high temperature is used for annealing.
<img width="1439" height="827" alt="Screenshot 2025-11-10 203610" src="https://github.com/user-attachments/assets/d443838e-7521-4d2f-a06d-e78d355ee53b" />

9. Steps to form Contacts and Interconnects: Firstly etched thin oxide in HF solution and deposit titanium on wafer surface using sputtering. Sputtering is a process where the high charged Ar ions are bombarded onto the substrate and used to eject the atoms of susbtrate and deposit onto the susbtrate. Then wafer is heater at about 650-700 C in N2 ambient for 60s. This form low resistance TiSi2 which is used for local interconnnect. TiN used only for communication. Mask 11 is used and TiN is etched. RCA cleaning is also used which consists of a solution of de-ionized water, 5 parts of ammonium hydroxide and 1 part of hydrogen peroxide.
<img width="769" height="477" alt="Screenshot 2025-11-10 204629" src="https://github.com/user-attachments/assets/41cb73cf-90da-47a5-968c-1d54dd94296c" />
<img width="1243" height="543" alt="Screenshot 2025-11-10 204755" src="https://github.com/user-attachmen
<img width="1485" height="717" alt="Screenshot 2025-11-10 205225" src="https://github.com/user-attachments/assets/f8215954-4472-4d49-9c69-e775a1900bf4" />
ts/assets/1e052f61-0b36-4901-bbb9-5cd04700d59a" />
<img width="1303" height="729" alt="Screenshot 2025-11-10 205249" src="https://github.com/user-attachments/assets/5ed39431-5276-4717-8832-366ecb9dd58b" />

11. Higher Metal layer formation: Deposit thick layer 1um of SiO2 doped with P or B known as phosphosilicate glass or borophosphosilicae glass deposited on the wafer surface. Chemical mechanical polishing (CMP) technique is used for planarizing the wafer surface.
Mask 12 is used and add 10nm TiN used because it has good adhesion for TiN and used as a barrier to bottom layer. Deposit W layer and do CMP. Now deposit Al layer and used mask13 for Al plasma etching.
<img width="1263" height="658" alt="Screenshot 2025-11-10 210308" src="https://github.com/user-attachments/assets/d6b33871-d6a5-408d-bde6-cdaaaa8e3771" />

For above metals again depoist SiO2 and do CMP. Mask 14 is used to create the contact holes.Again depoist thin TiN and W  as contacts. Again used mask 15 to define the 3rd layer. This layer is thicker than the bottom layers. Finally mask 16 is used to open the contact holes on this layer.
<img width="1227" height="845" alt="Screenshot 2025-11-10 210632" src="https://github.com/user-attachments/assets/044d253f-e6ad-4b62-bba5-5d24295a4fe5" />
<img width="1275" height="1025" alt="Screenshot 2025-11-10 210728" src="https://github.com/user-attachments/assets/5e5c45b7-c852-4ff9-87d9-e3a45415afb8" />

* Lab Introduction to Sky130 basic layout and LEF using inverter

given the inverter where the gate of pmos and nmos are connected to gate and the the drain is connv=ceted to the output. Metal 1 layer is the first local interconnect layer which is of purple color and the metal 2 layer is pink color. Nmwell is the solid dash line and the N diffuisin area is of green line and P-diffusion area is of brown color, whereas polysisilicon is of red color.
<img width="456" height="586" alt="unnamed" src="https://github.com/user-attachments/assets/a90d37de-052b-4115-aa4b-dd55c1228a5f" />
<img width="516" height="752" alt="unnamed" src="https://github.com/user-attachments/assets/ae3e0957-a35b-4493-9e1c-ee95448f7b45" />
<img width="717" height="763" alt="unnamed" src="https://github.com/user-attachments/assets/62c3137a-48a1-45fa-8f18-10c0e17026c4" />
<img width="427" height="705" alt="unnamed" src="https://github.com/user-attachments/assets/cf6e691d-0d72-4bb7-a27d-6aa468456ba2" />



* Lab steps to create standard cell layout and extract spice netlist

<img width="516" height="752" alt="unnamed" src="https://github.com/user-attachments/assets/1dca6a6d-1161-4424-ae61-745ceeef1cc0" />

Extraction file: 
<img width="722" height="222" alt="unnamed" src="https://github.com/user-attachments/assets/79be00d4-841d-483d-838c-f7fae68cbc1f" />
<img width="671" height="129" alt="unnamed" src="https://github.com/user-attachments/assets/200c8a9d-3674-469a-b63e-8a2bc2e33f94" />
<img width="730" height="444" alt="unnamed" src="https://github.com/user-attachments/assets/a5ff67ee-2c41-4ac4-80d5-ceadbaff29cd" />

* Lab steps to create final SPICE deck using sky130 tech
Edit the extracted spice file by adding:
 .include ./libs/pshort.lib and .include ./libs/nshort.lib command.

And then set the supply voltage "VDD" to 3.3v by VDD VPWR 0 3.3V command. and similarly set the value of VSS also.

Now, we need to specify the input files. by Va A VGND PULSE(0V 3.3V 0 0.1ns 2ns 4ns).

Also add the command for the analysis like, .tran 1n 20n, .control , run,.endc,.end.
<img width="744" height="477" alt="unnamed" src="https://github.com/user-attachments/assets/f8a18d46-461b-40f1-ba83-88c394a08c7e" />

 After this see the ngspice and plot y vs time a. 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8416d8b0-3b39-49b1-bcda-7371e89a0d71" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8a6bfb63-6d4b-4971-8f9d-b7d9c1f07a8a" />

Now if we increase the C3 value from 0.024ff to 2ff the graph will look like this, graph become more smoother.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/38f64735-bdba-49f1-a7ce-c6e85ad1766d" />

* Lab steps to characterize inverter using sky130 model files

We need to calcualte the 4 parameters:

- Rise time: It is time taken to the output waveform to 20% value to 80% value.
<img width="306" height="86" alt="image" src="https://github.com/user-attachments/assets/a8daba1e-99c0-48b4-881e-6fcfe81919d5" />
so, rise time= (2.2489 - 2.1819)e-09 = 66.92 psec.

- Fall time: It is the time take by output for transition from 80% to 20%.
<img width="301" height="52" alt="image" src="https://github.com/user-attachments/assets/e8a5ab94-c6ce-4a5f-9c57-b0815b098b37" />

Hence the fall time= (4.09512 - 4.05264)e-09 = 42.51 psec.

-Propagation delay: It is the time difference between the 50% of input and 50% of the output.
<img width="282" height="57" alt="image" src="https://github.com/user-attachments/assets/2ffc78fc-090a-4d6b-ae36-901ed69300e9" />
so, propogation delay =(2.2106 - 2.15012)e-09 = 60.48 psec.

-Cell fall delay: It is time for output falling to 50% and input is rising to 50%.
<img width="276" height="52" alt="image" src="https://github.com/user-attachments/assets/2f83b37a-5fc7-4162-8857-750a37289594" />
so, cell fall delay =(4.07735 - 4.04988)e-09 = 27.47 psec.

* Lab introduction to Magic tool options and DRC rules
To know more about the Magic DRC we can go to the website:- http://opencircuitdesign.com/magic/Technologyfiles/TheMagicTechnologyFileManual/DrcSection

Link to Google_Skywaters Design Rules: - https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

For reference , we can use the github repo of Google-Skywater: - https://github.com/google/skywater-pdk

* Lab introduction to Sky130 pdk's and steps to download labs
Follow the steps:

First go to the home directory.

-To download the lab files for performing DRC corrections:

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

-To extract the lab files from the downloaded file:

tar xfz drc_tests.tgz

Then go inside the lab folder drc_tests.

To list all the directories, we can use the command ls -al.

To view the .magicrc file, we can use the command gvim .magicrc. This file serves as the startup script for magic and tells it where to find the technology file. The technology file is already available locally in the same directory, so we can make changes to it if needed.

To start the magic tool with better graphics, we can use the command magic -d XR &.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/10ea3278-77d1-4f3b-af2b-d08f3043891f" />

Content of .magicrc file by using command vi .magicrc
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3b7499f1-55ed-43d3-b246-fa5f7b84644d" />

* Lab introduction to Magic and steps to load Sky130 tech-rules
Use the command magic -d XR : to open the magic tool. Open the met3.mag file from the file menu. we will see different layouts with different DRC values, called rule numbers.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2c8a7766-3b1f-4f06-987e-37a5c2b5228c" />
These rule number we can found at Google-Skywater documentation. Now we will select the any layout area and check drc why in tckon.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/870a880a-f7b6-4d8b-9352-4ab135612739" />
Next, select a blank area and hover the mouse pointer over the metal3 contact icon. Press the p button and type 'pek' in the tkcon. Then execute the command cif see VIA2 in the tkcon tab.

we will see a bunch of black squares appear inside the area.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/37f0df39-678d-4459-9484-af92d178bb9d" />

* Lab exercise to fix poly.9 error in Sky130 tech-file
Now, we will open the poly.mag file in the magic tool with the helo of the command load poly.mag in the tkcon terminal. consider the rule poly.9 then check the website for that particular rule. To find the error, we can look at the sky130A.tech file which is present in the drc_tests directory. we can open this file with the text editor of Linux itself.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f48dad29-a6ca-4f1a-9609-82c9a11df056" />

Search for 'poly.9' in the sky130A.tech file. It appears in both the POLY and uhrpoly sections, where the rules are not set properly. Add a change in both sections. After making changes to the sky130A.tech file, click on Save and close the editor file.

Next, execute the command tech load sky130A.tech in the tkcon terminal. Then, run the drc

*  Lab exercise to implement poly resistor spacing to diff and tap

To correctly implement poly resistor spacing, we will need to make changes to the sky130A.tech file again.
Now will execute in Tkon after saving.
To check for errors, we can make a copy of the poly.9 model from the poly.mag file in the magic window.

To find the description of a DRC error, we can select the area with the error in the magic window and then run the command drc why in the tkcon terminal.

This will give a description of the error.

* Lab challenge exercise to describe DRC error as geometrical construct
Now we will make some changes in sky130A.tech file which are as follows:
To find the nwell.6 model error, open the nwell.mag file in the magic tool. In the figure, the deep nwell is shown in yellow stripes and the nwell is shown in dotted green pattern.
This error can be seen at the site as well.

* Lab challenge to find missing or incorrect rules and fix them
Now we will open the magic tool and execute the commands drc style drc(full) and drc check.

### DAY 4: Pre-layout timing analysis and importance of good clock tree. Timing modelling using delay tables.

*Introduction to delay table
Power Aware CTS:- If we make enable pin at logic '1' in the AND gate, then clock will propagate and if we make it 'logic 0' it will block the clock. Similarly in 'OR' gate if we make enable as 'logic 0' it will propagate and on making it 'logic 1' it will block the clock.

So the advantage of this blocking period is that we can save lot of power in clock tree.
<img width="1680" height="596" alt="Screenshot 2025-11-10 212031" src="https://github.com/user-attachments/assets/c01dcd38-6bec-494c-9ba4-8da8b8f66606" />

In the table we get the delay by the intersection of the input slew and the output load.
<img width="782" height="199" alt="Screenshot 2025-11-11 204229" src="https://github.com/user-attachments/assets/511cba58-4d28-490f-8655-37ee1e25f931" />

* Timing analysis with the Ideal clock using OpenSTA
- Setup timing analysis and introduction to flip flop setup time

<img width="586" height="429" alt="Screenshot 2025-11-11 062236" src="https://github.com/user-attachments/assets/d9341565-f671-46a2-a614-b7f91c69e38a" />

<img width="1729" height="1005" alt="Screenshot 2025-11-10 223545" src="https://github.com/user-attachments/assets/a1e4a08c-557d-42bc-b101-00d34285303f" />

finite time S is required before clock edge for D to rech Qm.
<img width="1386" height="394" alt="Screenshot 2025-11-11 054913" src="https://github.com/user-attachments/assets/38b4129e-ce5f-4655-bfe0-833c858b1d64" />

- Jitter is the temporary variations of clock period.
<img width="1739" height="910" alt="Screenshot 2025-11-11 055102" src="https://github.com/user-attachments/assets/2419af3b-6aed-4c9c-955a-e03ecfa39140" />

Ideally the slew is considered to be zero. It is the difference between the arrival time of clock at different points.

<img width="1434" height="336" alt="Screenshot 2025-11-11 055525" src="https://github.com/user-attachments/assets/31d4bb9b-b3ca-41cd-92b1-7fd313e1c365" />

* Clock Tree Synthesis (CTS): CTS is done using the Clock tree structure that should meet the ideal skew condition. Usually midpoint strategy is used to find the the almost slew condition.

<img width="1316" height="926" alt="Screenshot 2025-11-11 055725" src="https://github.com/user-attachments/assets/c95ed882-9ff6-41b3-928a-35f083a2c4a5" />

CTS has the RC circuit which becmoses worse as the wirelength increases. Best way is to used buffers in the long wires. 
<img width="1310" height="761" alt="Screenshot 2025-11-11 055919" src="https://github.com/user-attachments/assets/052fbaae-051e-45cc-a320-d51014841efc" />

Clock net shielding is also used to prevent the glitches as the coupling capacitance may cause the glitch and provide the inaccurate data results in inaccurate functionality.In shielding either the wires are connected to GND or VDD. Crosstalk also added the additional delay.
<img width="1294" height="857" alt="Screenshot 2025-11-11 061114" src="https://github.com/user-attachments/assets/0448fdc7-5a56-47ab-bb1c-a8c8f23f794e" />
<img width="1806" height="927" alt="Screenshot 2025-11-11 060913" src="https://github.com/user-attachments/assets/33998585-1d94-41b3-a6c7-eaa44f8db642" />

* Setup timing analysis for real clocks: Real clocks only the added the delays of the wires or buffers used. 
<img width="1574" height="906" alt="Screenshot 2025-11-11 061307" src="https://github.com/user-attachments/assets/14a61eec-f3c1-47bd-8909-378b9b5896c2" />

<img width="1500" height="212" alt="Screenshot 2025-11-11 061742" src="https://github.com/user-attachments/assets/e278894d-f48c-43ed-ab0f-eb7b613dec95" />

Slack is defined as the difference between the data required time and data arrival time. If slack is negative the violation occurs and if slack is positive or zero then we get the expected results.

* Hold Timing analysis: For hold time the condition is : 
<img width="1129" height="184" alt="Screenshot 2025-11-11 062901" src="https://github.com/user-attachments/assets/96419c35-e213-4d91-aafa-939632c9ba26" />

Here the jitter and the uncertainity remains same as of setuo analysis. Here slack is defined as the difference between the data arrival time and the data required time.
<img width="1745" height="926" alt="Screenshot 2025-11-11 063426" src="https://github.com/user-attachments/assets/dc6bddbc-c5f8-4867-bc17-5c619c9a6849" />

* Lab steps to convert grid info to track info
Now, we need to extract the '.lef' file from the '.mag' file to place it into the picorv32a flow.

There are certain guidelines to follow while making standard cells:

-The input and output ports must lie on the intersection of the vertical and horizontal tracks.

-The width of the standard cell should be an odd multiple of the track pitch, and the height should be an odd multiple of the track vertical pitch.

Now we can open the track file from pdk/sky130/libs.tech /openlane/sky130_fd_sc_hd/track.info to get more information on this.

The track is used during the routing stage and is essentially a trace of metal layers such as metal 1, metal 2, etc.

PNR is automated, so we need to specify where we want the routes to go. This specification is given by tracks. Each of the tracks is placed at (0.23, 0.46)um horizontally and (0.17, 0.34)um vertically for li1, metal 1, and metal 2 layers.

In the layout, the ports are on the li1 layer. To ensure that the ports are on the intersection of the tracks, we will need to convert the grid into the tracks.
To do this, we can first open the tracks file and then open the tkcon window and type the help grid command.
Then again will write command according to the track file required.
Now we can see that, the ports has been placed at the intersection of the tracks. But between the boundaries, 3 boxes are covered. so our second requirment also satisfies here.

*Lab steps to convert magic layout to std cell LEF

Now, we will need to decide on the port name and its values. we can set the values for different ports, and for the power and ground port, we will need to make changes in the 'attach to layer' as Metal1.,After these parameters are set once, we are ready to extract the lef file from the mag.

Now, we open this file in the magic by the command:
magic -T sky130A.tech sky130_vsdinv.mag &

To extract the lef file we have to write the command in the tckon window as given below,
lef write
so it will create a lef file and we can check it in the vsdstdcellsdesign folder by using command ls -ltr

*Introduction to timing libs and steps to include new cell in synthesis

Now that the .lef file has been created, the next step is to plug this file into picorv32a. Before that, we will need to move the files to the src folder where all the design files are available at one location.
To do this, we can copy the file using the cp command.
this is how the library file looks like. We have different library files named as typical,slow ,fast. Now we will copy it to the src folder
Here We need to modify the config.tcl file of picorv32a directory,So open the config.tcl file of picorv32a directory.

OPENLANE :- Now we will go to the open lane directory and execute the docker command.

Will Execute the following commands in a line

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      

add_lefs -src $lefs

run_synthesis

* Lab steps to configure synthesis settings to fix slack and include vsdinv

We will try to modify the parameters of our cell by referring the README.md file in the configuration folder in openlane directory

The README.md file contains information about the parameters of the cell.
We will give the following commmands in the terminal in openlane directory

prep -design picorv32a -tag 01-04_12-54 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

echo $::env(SYNTH_STRATEGY)

set ::env(SYNTH_STRATEGY) "DELAY 3"

echo $::env(SYNTH_BUFFERING)

echo $::env(SYNTH_SIZING)

set ::env(SYNTH_SIZING) 1

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis

prep -design picorv32a -tag 01-04_12-54 -overwrite is used to overwrite the existing files with previous values of simulations.

After synthesis, we have observed that the slack is nagative.

-wns(worst negative slack)= -23.89
-tns(total negative slack)= -711.59.

Now run_synthesis we will see chip area has incresed and the value of slack has reduced.
Since synthesis of the picorv32a is successful, so we will run the floorplan using command run_floorplan. Since, we are getting the error so first again we have to do the synthesis using the commands mentioned earlier and then we will use following commands to do the floorplan,

init_floorplan

place_io

tap_decap_or


so now we are good to run the placement using command run_placement
Here placement is succesfull now without any error. so,We will run the expand command in the tkcon window

*Lab steps to configure OpenSTA for post-synth timing analysis

We have do STA on the picorv32a design which had timing violations.First we will run the synthesis using the following commands in openlane directory

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

set ::env(SYNTH_SIZING) 1

run_synthesis
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/08f47393-252d-477f-9888-1ba263e5c55b" />
Now we have to make a new pre_sta.conf file. We can do this by vim editor or in simple text editor also.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ea87d139-cce4-4dd5-8619-0a8531c1f25a" />
Now we will create a my_base.sdc file which will have the definitions of environment variables.

Now, we also need to create my_base.sdc file having the data shown in below image in openlane/designs/picorv32a/src directory
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5c303ff7-e246-44be-ad67-005cfa76fd01" />
Now will go to the openlane directory in a new terminal and execute the sta pre_sta.conf command.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d37f6a65-ad1c-4fda-bd85-3ba3bc725773" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7375c244-855f-4ec4-9754-da0e7dd4e1b3" />

<img width="1920" height="1080" alt="319902308-146e218e-a4a5-4f37-9ca2-088d74eb5d99" src="https://github.com/user-attachments/assets/0c18f7c6-25eb-46ec-afd6-d1831a17b5be" />

* Lab steps to optimize synthesis to reduce setup violations
Now we will change the FANOUT parameter and again do the synthesis,

prep -design picorv32a -tag 02-04_05-27 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

set ::env(SYNTH_SIZING) 1

set ::env(SYNTH_MAX_FANOUT) 4

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/93e66725-9209-41fd-801b-4f68c316347c" />
Now, run the sta pre_sta.conf command in a new terminal in openlane directory itself,
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e77a09ea-f735-419e-a0e3-d27d98118d3d" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/96873054-c761-4c51-b482-e74b7e838f99" />

* Lab steps to do basic timing ECO
OR gate which has a drive strength of 2 is driving 4 fanout.
<img width="923" height="151" alt="image" src="https://github.com/user-attachments/assets/ff260ca4-c545-48e3-bf62-6ecf9d97ff18" />
So we have to replace this OR Gate with another OR Gate having Drive strength of 4 by executing the commands given below,

-To Reports all the connections to a net

report_net -connections _11672_

-To Check the command syntax

help replace_cell

-To Replace the cell

replace_cell _14510_ sky130_fd_sc_hd__or3_4

-To Generate the custom timing report

report_checks -fields {net cap slew input_pins} -digits 4

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9544791f-a8e9-4342-810e-937c8a87edbe" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cdfff422-9628-4d0f-80de-7928d8ec6747" />
Now we can see theslack has been reduced from -23.89 to -23.51

<img width="906" height="133" alt="image" src="https://github.com/user-attachments/assets/72af0043-67f5-439f-b326-21c161f6892d" />
In above case also OR gate which has a drive strength of 2 is driving 4 fanout.

So we have to place this OR Gate with another OR Gate having Drive strength of 4 by following these commands

-To Reports all the connections to a net

report_net -connections _11675_

-To Replace the cell

replace_cell _14514_ sky130_fd_sc_hd__or3_4

-To Generate the custom timing report

report_checks -fields {net cap slew input_pins} -digits 4

*Lab steps to run CTS using Triton

Now we need to replace the old netlist with newly generated netlist which has generated after reducing the slack. And then we will run floorplan , placement and CTS.
So, we need to make a copy of this old netlist and then we will add the newly generated netlist to be used in our openlane flow for further process.

So we will make the copy by following commands.

-To go to the following location

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/02-04_05-27/results/synthesis/

-To List the contents

ls -ltr

-To copy the netlist with particular name

cp picorv32a.synthesis.v picorv32a.synthesis_old.v

-To List the contents

ls -ltr

Now we will do synthesis again then floorplan , placement and cts in the openlane directory itself by the following commands,

   prep -design picorv32a -tag 02-04_05-27 -overwrite
   
   set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
   
   add_lefs -src $lefs
   
   set ::env(SYNTH_STRATEGY) "DELAY 3"
   
   set ::env(SYNTH_SIZING) 1
   
   run_synthesis
   
   init_floorplan
   
   place_io
   
   tap_decap_or
   
   run_placement

    # Incase getting error will use this command
   
   unset ::env(LIB_CTS)

   run_cts
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4e3b135a-febb-4c12-83ee-9bdab015a48b" />

* Lab steps to verify CTS runs
OPENROAD To create a database in OPENROAD using LEF and TMP files, we can use the following commands:

- First, make sure we are in the directory where the LEF and TMP files are located.

- Then, enter the following command to start the OPENROAD tool,

openroad

- Once you are in the OPENROAD tool, enter the following command to create the database,

To Read lef file

read_lef /openLANE_flow/designs/picorv32a/runs/02-04_05-27/tmp/merged.lef

To Read def file

read_def /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/cts/picorv32a.cts.def

To Create an OpenROAD database file named pico_cts.db

write_db pico_cts.db

Now we can see this database file is present in openlane directory.

* Lab steps to analyze timing with real clocks using OpenSTA
Now we can execute the following commands,

-To load the created db file in Openroad

read_db pico_cts.db

-To read the netlist post CTS

read_verilog /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/synthesis/picorv32a.synthesis_cts.v

-To read the library for design

read_liberty $::env(LIB_SYNTH_COMPLETE)

-To link the design and library

link_design picorv32a

-To read the custom sdc we have created

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

-To setting all clocks as propagated clocks

set_propagated_clock [all_clocks]

-To Generate the custom timing report

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

-To exit from Openlane flow

exit

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7f8130b7-e3d6-49da-a73f-e67f1102703c" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/62155698-b635-4743-ac28-59daf50d70e3" />

* Lab steps to execute OpenSTA with right timing libraries and CTS assignment
-To remove sky130_fd_sc_hd__clkbuf_1 from the list

set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

- To check the current value of CTS_CLK_BUFFER_LIST

echo $::env(CTS_CLK_BUFFER_LIST)

- To check the current value of CURRENT_DEF

echo $::env(CURRENT_DEF)

To set def as placement def

set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/placement/picorv32a.placement.def

To run cts

run_cts

To check the current value of CTS_CLK_BUFFER_LIST

echo $::env(CTS_CLK_BUFFER_LIST)

* Lab steps to observe impact of bigger CTS buffers on setup and hold timing
Now we will follow the same commands we have used earlier to run OPENROAD,

openroad

read_lef /openLANE_flow/designs/picorv32a/runs/02-04_05-27/tmp/merged.lef

read_def /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/cts/picorv32a.cts.def

write_db pico_cts1.db

read_db pico_cts.db

read_verilog /openLANE_flow/designs/picorv32a/runs/02-04_05-27/results/synthesis/picorv32a.synthesis_cts.v

read_liberty $::env(LIB_SYNTH_COMPLETE)

link_design picorv32a

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

set_propagated_clock [all_clocks]

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

report_clock_skew -hold

report_clock_skew -setup

exit
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dd53e2c5-7260-47e5-a28d-54918542209d" />

### DAY 5: Final steps for RTL to GDS using Triton Route and OpenSTA
Lee's algorithm is used for routing. Routing is the physical connection between the components. It is the first algorithm for routing and uses the grid. It workds by finding the vertical and horizontal grid of source and label adjacent grid with the next integer. It continues till it reach the target point.it finds the shortest path and avoids the zig zags. It limitation is it consumes more power and memory. 

<img width="1114" height="912" alt="Screenshot 2025-11-11 065759" src="https://github.com/user-attachments/assets/c1af0197-6c34-4156-93ce-41996639ebe1" />

* DRC (Design rule check): Basic design rules involves the wire width, wire pitch and wire spacing.
<img width="541" height="291" alt="Screenshot 2025-11-11 070432" src="https://github.com/user-attachments/assets/3788020f-1acf-4a57-a4f0-281263d70a39" />
<img width="537" height="300" alt="Screenshot 2025-11-11 070440" src="https://github.com/user-attachments/assets/316a7887-7e2b-4785-927d-8ddf56b25c75" />
<img width="552" height="288" alt="Screenshot 2025-11-11 070535" src="https://github.com/user-attachments/assets/7ae3288a-8e3e-4500-b93e-0527443cf9cb" />

DRC violation occurs if there is any short. So to avoid this different metal layer is used.Now new rules is to be check like via width etc.

<img width="535" height="429" alt="Screenshot 2025-11-11 070647" src="https://github.com/user-attachments/assets/e00e6c14-a140-4cbc-b658-28b9f255ee95" />
<img width="447" height="378" alt="Screenshot 2025-11-11 070905" src="https://github.com/user-attachments/assets/8c6c0f8a-3b28-4f1e-abae-c96e4b01a481" />
<img width="393" height="304" alt="Screenshot 2025-11-11 070945" src="https://github.com/user-attachments/assets/e28d0adc-e200-4b1f-b00d-0f2ce0a276d0" />

* Lab steps to build power distribution network

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a -tag 30-03)20-42

echo $::env(CURRENT_DEF)

So, till here we have done CTS and now we are going to do the routing. but before routing we have to generate the PDN(power distribution network)file by using the command.

gen_pdn
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cd7fde3e-e5df-4002-8666-b674313895d1" />
It seems like the net VGND displays the total number of nodes on the grid matrix, indicating that it has been successfully created.

The chip receives power from the VDD and GND pads, which then travels through the tracks and ultimately reaches the cells to power them.

* Lab steps from power straps to std cell power
<img width="837" height="537" alt="image" src="https://github.com/user-attachments/assets/c4a4e8f9-58a0-4983-ad4f-a8e82c958799" />
Here green color is representing the chip, and yellow, red and blue boxes are the I/O pins,power and ground pads respectively.

Power is transfered to the rings from the pads through the black dots shown in the image on the cross section points of the ring and pads.

We have vertical and horizontal tracks which ensures that the power is being transfered from the ring to chip this is shown by the red and blue color. This is how power planing works in physical design of any device.

Basics of global and detail routing and configure TritonRoute
The final step of physical design is Routing.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/57d84543-000c-47dd-a047-a4fcdad71f96" />
The usage of the def command in the image above is to indicate that the latest completed step was the generation of PDN.

The resulting file 17-pdn.def contains the information from cts.def as well as the power distribution network. By executing specific commands, we can determine the type of global and detailed routing that will be performed.

Routing process is done by using the command

run_routing

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9ccbd965-1275-4f90-9218-4c2b95f4613d" />

Final generated layout is: 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/126607f5-a2d2-49fc-ab4f-1eb0fcd19fba" />

* Triton Route feature: It performs the initial detail route. 
- Honors pre-processed route guides (obtained after fast route) i.e attempts attempts as much as possible to route within route guides. Assume each guides for each net satisfy the inter guide connectivity. It works on proposed MILP based panel routing scheme with intra layer parallel and inter layer sequential routing framework.

-Requirements of preprocessed guides

          Should have unit width

          Should be in preferred direction
<img width="1346" height="410" alt="Screenshot 2025-11-11 072220" src="https://github.com/user-attachments/assets/fdd3832c-66a7-4805-9b7e-a2afbc99a59d" />

- Inter guide connectivity: Two guides are connected if

              They are on the same metal layer with touching edges.

              They are on neighbouring metal layers with a non-zero vertically overlapped area.

Each unconnected terminal i.e, pin of a standerd-cell instance should have its pin shape overlapped by a route guide.


In this figure we can see the 4 layers of metal. each of these layers are devided in to the "--" lines. lets focus on metal 2 layer. here we assume the routing direction vertical. These "--" lines are called pannels. each pannels assigns the routing guides. here we can see the blue arrows. here routing is heppenes in the even index. it means that intra layer parallel routing. first it is happens in the even index and the it will heppen in the odd index. but it is heppening in the parallel in this perticular layer.
<img width="1336" height="467" alt="Screenshot 2025-11-11 073459" src="https://github.com/user-attachments/assets/97ee9cb5-7683-4b70-9880-7b3997dfc956" />

TritonRoute method to handle connectivity
INPUTS:-LEF
OUTPUTS:-detailed routing solution with optimized wore-length and via count
CONSTRAINTS:-Route guide honouring, connectivity constraonts and design rukes
Now we have to defined the space where detailed routing take spaced.

Handling connectivity:-

Access point(Ap):- An on-gride point on the metal layer of the route guide, and is used to connect to lower-layer segments, upper-layer segments, pins or IO ports.

Access point cluster (APC):- A union of all access points derived from same lower-layer segment,upper-layer guide, a pin or an IO port.
<img width="1205" height="411" alt="Screenshot 2025-11-11 073914" src="https://github.com/user-attachments/assets/42280ddc-bd05-407b-92c2-d54bd23bfdeb" />

Routing topology algorithm and final files list post-route. The algorithm requires the determination of the cost associated with each APC and the calculation of the minimum spanning tree between the APCs to find the optimal points between two APCs. The next step involves post-routing STA analysis, which requires the extraction of parasitic effects (SPEF).Since OpenLANE does not have a SPEF extraction tool, this process needs to be done outside of OpenLANE. he resulting .spef file can be located in the routing folder under the results folder. This is the final generated layout.
<img width="564" height="291" alt="Screenshot 2025-11-11 075108" src="https://github.com/user-attachments/assets/fa126a8f-becb-4f02-873a-f80978622003" />
### Acknowledgement
I'm very thankful to VSD team for their RISC-V tapeout program.
