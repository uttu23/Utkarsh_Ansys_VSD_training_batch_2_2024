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


