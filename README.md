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
![schemetic](https://user-images.githubusercontent.com/99113992/152672756-90464ca6-c8ab-463e-8705-fd436b57b6cb.PNG) The 10T SRAM circuit is shown in fig.1.This circuit avoids the read operation noise by isolating the memory part(latch) of the cell from external environment by disabling the access transistors during read operation and the memory read operation is done by additing additional circuit connected to the Q.By this process we can also improve the read operation speed of SRAM since we are not using access transistors for measuring memory read operation and hence the leakage current is decreased. 

## Circuit Operation 
There are three modes of operation of 10T SRAM: 1.Stand-by mode: When Wordline(WL) = 0 and Read enable(RE) = 0,then the memory part became isolated from external environment and the data present in it remains same. Therefore no read or write operation takes place. 2.Memory Read: When RE=1, then the Transmission gate is in active condition and the RDout gets the inverted value of Q(i.e, Qb) through the Transmission gates.And we off the access transistors during the memory read operation to reduce the leakage power. 3.Memory write: When WL=1, then the write operation is possible.If BL=0, then PM0 transistor will "ON" and Qb becomes 1 and Q becomes 0. Similarly if BL=1,then Q becomes 1 and Qb becomes 0. Since Memory write operation still uses the access transistors unlike Memory operation, the Memory write operation will be slower when compared to memory read operation. The main advantage of this 10T SRAM is that it doesn't require the precharge capacitors connected to a sense amplifier for memory read/write operation as that of 6T SRAM, because here the data stored in memory is directly passes through the inverter and transmision gates.And also the charging or discharging of RD happens only when the RD changes,i.e, there is no power is consumed or dissipated if the next data is same as that of previous value.Therefore, this design of 10T SRAM reduces the consumption of when consecutive readout values are same. 

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
