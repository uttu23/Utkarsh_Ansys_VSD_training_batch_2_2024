### Day 1 -Inception of open-source EDA, OpenLANE and sky130 PDK
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


### Day 2 - Good floorplan vs bad floorplan and introduction to library cells


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

**Layout design step**

- In Layout Design First step is to get the function implemented through the MOS transistor through a set of PMOS and NMOS transistor and the second step is to get the PMOS network graph and the nNMOS network graph out of the design that has been implemented.
![image](https://github.com/user-attachments/assets/00cc530f-372e-48c1-8f87-3da62cb309a5)

After getting the network graphs next step is to obtain the Euler's path. Eule's path is basically the path which is traced only once.

![image](https://github.com/user-attachments/assets/f482da90-2f04-421b-8d62-064623e10449)

Next step is to draw stick diagram based on the Euler's path. This stick diagram is derived out of the circuit diagram.

![image](https://github.com/user-attachments/assets/5f286e4c-19c4-4008-a62f-acfb5a1482d2)

Next step is to convert this stick diagram into a typical Layout, into a proper layout and then get the proper rule we have discissed earlier. Once we get the particular layout then we have the cell width, cell length and all the specifications will be there like drain current, pin locations and so on.

![image](https://github.com/user-attachments/assets/cb9ceeee-7b51-48dc-9891-e358a57efb32)

Next and Final step is to extract the parasitics of that particular layout and charaterize it in terms od timing. So before that the output of the layout design will be GDSll. Once you get the extracted spice netlist then we characterize it. Characterization helps in getting timing, noise and power information.


**How to characterize the timing attributes for a cell?**

- First, we need to write the spice deck for timing characterization and then we have to do the transient run so that we can find the input transition, output transition and cell delay

![image](https://github.com/user-attachments/assets/2ca20de1-fec2-4464-af7d-f138f90186a6)

![WhatsApp Image 2024-09-16 at 13 41 40](https://github.com/user-attachments/assets/c7f49cde-ca17-4f75-a104-e314472bcac3)


![image](https://github.com/user-attachments/assets/ff98036a-3372-4784-b3de-471e68549ccc)

![image](https://github.com/user-attachments/assets/6b5d6b2d-f401-4163-aca8-9ab91823571f)

![image](https://github.com/user-attachments/assets/e6b910b0-1b4e-46f7-b06c-d65dbcc17baf)

![image](https://github.com/user-attachments/assets/c9b32185-fe2e-4926-8c2c-dcce9ebdbfa7)

![image](https://github.com/user-attachments/assets/eba7438b-03b0-4d09-afbc-301c253bf552)

![image](https://github.com/user-attachments/assets/31914b99-1d1b-40ba-b5af-f484dc708157)

![image](https://github.com/user-attachments/assets/b4e4b4b6-b421-4dea-8084-5cc66e45268e)

![image](https://github.com/user-attachments/assets/a10cd7bd-0fab-4e58-86cb-bd1f5706ee28)

![image](https://github.com/user-attachments/assets/106c6d6f-7889-46cf-bdd0-672a4e7e1479)

![image](https://github.com/user-attachments/assets/eeee6d18-555f-4987-a1dc-6f290a2275c3)

![image](https://github.com/user-attachments/assets/7bfa6d78-34ef-4858-97bd-c3bbdf9390c6)

![image](https://github.com/user-attachments/assets/a7838333-30ff-4c41-883b-427d0be75a89)

### Day 3 - Design library cell using Magic Layout and ngspice characterization

**Lab steps to git clone vsdstdcelldesign**

- To get the clone, copy the clone address from reporetery and paste in openlane terminal after the command **_git clone_**. this will create the folder called "vsdstdcelldesign" in openlane directory.
- Using command "magic -T sky130A.tech sky130_inv.mag &" we can see the layout of inverter for which we will be doing characterization and in layout file we see all the layers like diffusion, polysilicon and and also we can check whether layers present are DRC legal or not.

![image](https://github.com/user-attachments/assets/0a523b1a-2c60-40f7-9717-d166f08f423c)

- Then we got to learn about how fabrication is done using mask 16 method and finally CMOS looks like
![image](https://github.com/user-attachments/assets/beedf3ad-b297-4756-ac6b-b0a8b9e24f10)

- Now from existing layout of inverter we need extract the spice deck and for that we can use the command **ext2spice cthresh 0 rthresh 0** and then again **ext2spice** and then we can check in current working directory .spice file would be created
![image](https://github.com/user-attachments/assets/bc1d1a3a-2e8a-424b-8c58-98f65d397100)


**Snapshot of final lef created -** 
![image](https://github.com/user-attachments/assets/fc73b6f7-0feb-4228-9fe3-492fb3419bd7)

- Now in the existing spice file we need to make some changes like including proper model files and applying input voltage. Final spice file
![image](https://github.com/user-attachments/assets/84bf75a9-e5bc-4c48-aac8-597af83a294d)

### Day 4 - Pre-layout timing analysis and importance of good clock tree

**Concept of delay table**

- for each CELL we have separate delay table with varying input slew vs output load and reason why we have such table is that input slew and load depends upon many factors like interconnect capacitance etc. So, designer comes up with this idea of 2d table for delay. From the below image we can map the delay according to slew and load value.

![image](https://github.com/user-attachments/assets/3fa21b41-fea5-4fbd-a173-980b1fd952e9)

![WhatsApp Image 2024-09-16 at 13 42 12](https://github.com/user-attachments/assets/0bb11959-bd37-470c-a4a3-6b3fd3e9f84c)

**Clock Tree Synthesis**

- For clock tree synthesis it's important that we maintain 0 skew between first stage flop and 2nd stage flop and if do simple like below image then arrival time for clock will be different between ff1 and ff2 and there will be skew of **Tff2 - Tff1**
![WhatsApp Image 2024-09-16 at 19 24 36](https://github.com/user-attachments/assets/3fee5033-7f2d-49fd-a42b-75216ee93717)

![image](https://github.com/user-attachments/assets/f480fd9d-bd09-4b1d-b984-e2cae02845c7)


- To overcome this issue designer comes up with great idea of **_H-Tree_**, in this method we first identify all the clock paths and then we select the mid point such that distance of that point to all flops will be equal in order to make arrival time of clock same for each flops.

![image](https://github.com/user-attachments/assets/c49c3a5e-afa3-46f1-97a9-6893934e6879)

- for CTS we use repeaters, and it is used for clock feeding so that there is not much distortion in launch signal and repeaters should have equal rise and fall time

- For improving the slack related issue we generally replace cell with different sizes of cell. So, that we can improve drive strength.

**Day 5 -Final step for RTL2GDS using tritinRoute and openSTA**

- **Routing: -** It is finding the best shortest possible connection between two end points with one point being the source and other point being the target and with a smaller number of twist and turns.


- **Maze-Routing (Lee's Algorithm): -** Therse should not be zig-zag lines of connections most of the connections should be in L shape or in Z shape. So according to algorithm first it creates some grids and grids are routing at the backend. It's called as routing grid. There are some numbers of grids on this routing having some dimensions. SO here we are having two points one is 'Source' and the other is 'Target'. With the help of this routing grid algorithm has to find out the best possible way between them.

**Process of routing is divided into two steps -**

1. Fast Route 
2. Detailed Route

![image](https://github.com/user-attachments/assets/556a0f04-dbef-4c46-bc5d-812e8036dbd3)

- In the Global route, the routing region is divided into the rectangular grids cells as shown in the figure above. And it is represented as cores 3D routing graph. Global route is done by FAST route engine. The detailed route is done by TritonRoute engine. A,B,C,D are four pins which we want to connect through routing. and this whole image of A,B,C,D shows the net.
