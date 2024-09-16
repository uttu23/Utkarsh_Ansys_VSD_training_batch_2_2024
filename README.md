**chip components**

1. Pads: Through which we can send the signal inside the chip.
2. Core: Place where all the logic gates are fixed.
3. Die: Present at the corner. it is the size of the entire chip.

**RTL to GDS flow**

- RTL -> Synthesis -> Floor planning and Power planning -> Placement -> Clock Tree Synthesis -> Route -> Sign Off

![image](https://github.com/user-attachments/assets/a1ca2826-6766-4e22-b891-77eb8acc6a95)

- Floorplanning -> Dimensions, Pin locations and rows are defined
- Placement -> Placing cells on floor planned rows. It is done in two steps 1) Global (not legal placement) 2) Detailed routing
- CTS -> To deliver a clock to all seq elements with minimum skew

**Antenna Rules Violation**
when metal wire segment is fabricated it can act as antenna. Reactive ion etching causes charge to accumulate on the wire. Transistor can get damaged due to this.
To overcome this issue we use bridging method.
![image](https://github.com/user-attachments/assets/81762328-3f72-4fe3-93b3-8905e2a1e8ea)
![image](https://github.com/user-attachments/assets/7a00b716-46ec-4371-b6c2-daeb51aca0a9)
![image](https://github.com/user-attachments/assets/4634fb3a-01ed-4c0f-b69f-052116238d06)

**Floorplan and Power planning**

- How to define width and height of chip?

![WhatsApp Image 2024-09-16 at 13 08 55](https://github.com/user-attachments/assets/a5342455-6b80-4b0c-91c3-4388e83a0389)

**How to define cell size?**

- height depends upon gap between power and ground rail
- Width depends upon the drive strength

**Review files after design prep and run synthesis**

- first run command 'run_synthesis' on interactive window

- After run gets completed we will get summary of total cells in the design 

![image](https://github.com/user-attachments/assets/a0776584-784a-4505-905c-bacd1c7ba713)

- Flop ratio = (total number for D flop/ total number of cells) = (1613/14876)

**Power Mesh**

- The phenomenon we have seen was causing the lowering of the supply voltage, this problem occurred because power has applied to one point only. The solution of the problem is using multiple power supply. So, every block will take charge from nearest power supply and similarly dump the charge to the nearer ground. this type of power supply is called mesh.

![image](https://github.com/user-attachments/assets/698aa86a-fc50-44f2-8dfc-e93123f40b71)

**Area of Chip**

- From generated DEF file we can see the area of design - 
![image](https://github.com/user-attachments/assets/d6f36754-b489-42c1-80c8-48efc3e8c774)

- Here we need to divide 660685 by 1000 units to get the value in um. Final area would be 660.685 x 671.405

- **How to characterize the timing attributes for a cell?**

- First, we need to write the spice deck for timing characterization and then we have to do the transient run so that we can find the input transition, output transition and cell delay

![image](https://github.com/user-attachments/assets/2ca20de1-fec2-4464-af7d-f138f90186a6)

![WhatsApp Image 2024-09-16 at 13 41 40](https://github.com/user-attachments/assets/c7f49cde-ca17-4f75-a104-e314472bcac3)

**Cell design and characterization flows**

**- Inputs for cell design flow**

1. In Cell Design Flow, Gates, flipflops, buffers are named as 'Standard Cells'. These standard cells are being placed in the section called as 'Library'.And in the library many other cells are available which have same functionality, but the size is different.

![image](https://github.com/user-attachments/assets/f1faab31-d57e-42fc-82b1-ebb3b04ef991)

If you lokk into one of the inverter from the library the cell design flowis as follows

The inverter has to represented in form of the shape, drive strength, power charracteristic and so on. Here cell design flow is devided into three parts.

1. Inputs
2. Design steps
3. Outputs

- **1)Inputs**:- Inputs required for cell design is PDKs, DRC and LVS rules SPICE models, library and user defined specs. In DRC& LVS rules tech file is provided which contains design rules and actual values. Rules can be converted in to code. SPICE MODEL tells about threshold voltage equation.
- 
![image](https://github.com/user-attachments/assets/42999612-c951-4dea-8ff4-ee548e8739c7)

- **2)design steps:**- Design involves three steps which are circuit design, layout design, characterization.

In circuitc Design there are two steps.

First step is to implement the function itself and second step is to model the PMOS nad NMOS transistor in such a fashion in order to meet the library.

- **3)Outputs** - The typical output what we get from the circuit design is CDL(circuit description language) file,GDSII,LEF,extracted spice netlist(.cir).
- 
![image](https://github.com/user-attachments/assets/b070a630-1a74-4d7c-99d9-d2949ba2bbe8)




