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
