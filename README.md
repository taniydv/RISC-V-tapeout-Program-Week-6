# RISC-V-tapeout-Program-Week-6
Lets's Forwarding to the RISC-V , Week 6 is the Physical design workshop where we learn the interactive flow from RTL to GDS.

### VDI IMAGE
Firstly download th zipped file of openlane : https://vsd-labs.sgpl.cdn.digitaloceanspaces.com/vsd-labs/openlane.zip

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
