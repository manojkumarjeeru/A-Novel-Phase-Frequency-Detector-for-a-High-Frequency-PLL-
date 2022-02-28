# A Novel Phase Frequency Detector for a High Frequency PLL
In this project I have implemented new phase frequency detector (PFD) which use only 10 transistors, whereas a conventional PFD uses 54 transistors. Prototype has been designed in Synopsys Custom Compiler  and implemented using 28nm technology with a supply voltage of 1.05V .The reset process has been completely removed in this design thereby eliminating the dead zone and speeding up the acquisition process reducing the delay in circuit. The design has been proposed for high speed, low power and low jitter applications. 

# Table of Contents 
1.[Introduction](#Introduction) 
2.[Circuit Design and Details](#Circuit-Design-and-Details) 
3.[Circuit Operation](#Circuit-Operation) 
4.[Simulation Waveforms](#Simulation-Waveforms) 
5.[Conclution](#Conclution) 
6.[References](#References) 
7.[Acknowledgement](#Acknowledgement) 
8.[Author](#Author) 

## Introduction 
PLL circuits have a wide range of uses in modern communications, including
radios, telephones, cellular devices, Computers, as well as other devices. In mobile or
wireless communications, PLLs have many uses like synchronisation, clock synthesis,
and reducing jitter (Variation from its ideal position).

The power consumption in the PFD contributes to a significant part of the total power consumption of a PLL.
Therefore overall power consumption in a PLL can be reduced by minimizing the power consumption in PFD. The
main challenge in the design of PFD is to obtain very high operating frequency with minimal power dissipation. In this paper a novel PFD architecture is
proposed which is completely free from dead zone, dissipates very low power and operates at high frequency is given

## Circuit Design and Details 
![hack_4](https://user-images.githubusercontent.com/72538560/156032830-b93dff2e-d9d4-4770-bda5-49a0c96dcb31.png)
The Circuit Design consists of Two D-Flip Flops without reset .The design  design concentrates on eliminating reset delay so that the dead zones are completely
removed.The reset path is eliminated by adding pass transistor logic.Also, The design uses only 10 transistors which reduces power consumpumtion and overall area of the PLL Circuit compared to conventional PLL.

## Circuit Operation 
Initially the CLKref and CLKvco signals are at logic zero which are provided as clocks to D flip-flops. At the rising edge of CLKref, N7, N8 and N12 turns on and the UP signal goes to logic high. At the
rising edge of CLKvco, N9, N10 and N11 turn on forcing DN to go high. When both UP and DN are high, the logic
levels at points R and S in Fig. 3 are pulled down to logic zero making UP and DN to go to logic zero without any
delay for reset. 

## Simulation Waveforms 
### 1.Write Operation 
As we have discussed earlier when WL=1,then the write operation is possible and the Q gets the BL value and Qb gets the inverted value of Q.And when WL=0,the data stored in the memory element doesn't change because of the access transistors are in inactive state. ![write operation](https://user-images.githubusercontent.com/99113992/152926807-6d204d6f-d516-4b4b-bc15-90d63d32310e.PNG) ### 2.READ Operation When RE=1 and REB=0, then the READ operation will takes place with the Transmission gate is in active state and the the data present in the memory element(Q) is passed through the inverter and then transimission gate to the RD terminal.Note that the RD terminal gets the inverted value of Q(i.e, Qb) because of the inverter, but if we want the Q to comeout at the RD terminal we need to connect that extra circuit to the Qb instead of Q. ![READ output](https://user-images.githubusercontent.com/99113992/152926529-253768c3-2502-4da1-b278-3e1437624971.PNG) Note that there is a small disturbance in the RD terminal during when the transmission gate is in off state(i.e, when RE=0 and REB=1), it's because when the transmission gate is in inactive condition there will be some leakage current since both of the nmos and pmos is in off state and moreover what we actually interested is during when transmission gate is in active state at which the READ Operation will takes place, So it doesn't matter to us when the transmission gate is in inactive state even if there is small disturbance in the output waveform. 

## Conclusion 
In 10T SRAM, since the inverter is directly connect with the memory element to make the READ operation independent of access transistors, we can actually reduce the read delay because now we don't need to wait for the access transistors to turn on for read operation.But the write operation still takes time because it still depends on Access transistors.In this section we are going to prove that the READ speed is increased by making the READ operation independent on Access Transistors. For measuring the read and write operation delay we simulated the same circuit, but by keeping the Timeperiod of input waveforms in nanometers we got the following results. ![compare read and write](https://user-images.githubusercontent.com/99113992/152933868-f7727778-3dd6-4ef7-bc85-453e18634cd9.png) From the figure, A = write 0 delay (i.e.,Time taken for BL=0 passes through the Access transistor to memory element(latch) and make Q=0) B = write 1 delay (i.e.,Time taken for BL=1 passes through the Access transistor to memory element(latch) and make Q=1) C = Read 0 delay (i.e.,Time taken for Q=0 passes through the inverter and transmission gate and make RD=1) D = Read 1 delay (i.e.,Time taken for Q=1 passes through the inverter and transmission gate and make RD=0) From the above waveform we can say that both the Read 0 and Read 1 delay is less than write 0 and write 1 respectively.Therefore, by making the read operation independent of Access transistors by adding the additional circuit for measuring READ operation we increased the READ Operation speed and hence reduced the leakage power.And through this we increase the read stability since we isolated the memory element from external noise. 

## References 
PN.V.Kiran, N.Saxena, "Parameter Analysis of different SRAM Cell Topologies and Design of 10T SRAM Cell at 45nm Technology with Improved Read Speed",International Journal of Hybrid Information Technology,Vol.9, No.2 (2016). 

## Acknowledgement 
Kunal Ghosh,Co-founder of VLSI System Design Corporation Pvt. Ltd. 

## Author 
Malli Chenchu Kiran, Final Year B.TECH, ECE, Indian Institute of Information Technology,Design and Manufacturing,(IIITDM) Kancheepuram Email: Kiran.malli789@gmail.com
