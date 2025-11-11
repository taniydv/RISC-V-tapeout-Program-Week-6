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

* 
