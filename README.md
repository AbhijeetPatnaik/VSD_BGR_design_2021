# Bandgap IP Design using Sky130 technology node

![workshop-flyer](Workshop-Flyer.png)

2-day hands on lab-based workshop on Analog Bandgap IP design using SKY 130, an open source 130nm PDK made available by collaboration between Google and Sky Water Technology Foundry. Workshop covers BGR are design from scratch to post layout simulation. On Day1 the course provides profound background on the theory of BGR, BGR’s description, application, implementation and need. Day 2 provide hands on experience in BGR design using ngspice, magic and netgen. After the course one will be able to understand concept of BGR, how CTAT and PTAT blocks are designed to get remove temperature dependency and implement solution to generate constant voltage as per the required specs.


## INDEX
   * [Part 1: Introduction to BGR](-##-Part-1:-Introduction-to-BGR)
   * [Part 2: Tools and PDK setup](-##-Part-2:-Tools-and-PDK-setup)
   * [Part 3: Design spec and data analysis](-##-Part-3:-Design-spec-and-data-analysis)
   * [Part 4: CTAT voltage generation circuit] (#Part 4: CTAT voltage generation circuit)
   * [Part 5: PTAT voltage generation circuit] (#Part 5: PTAT voltage generation circuit)
   * [Part 6: Biased current mirror circuit] (#Part 6: Biased current mirror circuit)
   * [Part 7: Reference voltage branch circuit] (#Part 7: Reference voltage branch circuit)
   * [Part 8: Start-up circuit] (#Part 8: Start-up circuit)
   * [Part 9: complete BGR circuit] (#Part 9: complete BGR circuit)
   * [Part 10: Layout of components] (#Part 10: Layout of components)
   * [Part 11: Top level extraction and LVS] (#Part 11: Top level extraction and LVS)
 * [Conclusion and Opinion] (#Conclusion and Opinion)
 * [References] (#References)
 
 
 
 
 
 ## Part 1: Introduction to BGR
 
 BGR is a temperature independent voltage reference widely used in integrated circuits. It produces a constant voltage regardless of power supply and variation in temperature.
 ![1](images/1.jpg) 
 
 **Why BGR?**
 
 There is a need for a device to provide a constant voltage independent of variation in power supply and temperature. A battery drops voltage over time. A typical power supply is noisy or has ripples and IC using Zener cannot be used due to high thermal noise and unavailability of lower voltage Zener’s.

**Solution**
 + A Bandgap reference which can be integrated in bulk CMOS, Bi-CMOS or Bipolar technologies without the use of external components.

**Applications of BGR**
+ Low dropout regulators (LDO)
+ DC-to-DC buck converters
+ Analog-to-Digital Converter (ADC)
+ Digital-to-Analog Converter (DAC)


###### BGR Principle

All devices inherently either have positive temperature coefficient or negative temperature coefficient. The operation principle of BGR circuits is to sum a voltage with negative temperature coefficient with another one with positive temperature coefficient. The two-temperature coefficient are designed so as to cancel each other out so that overall resultant is temperature independent. Generally, constant current supplied into semiconductor diode behave as CTAT i.e., complement to absolute temp. So, we need to design a PTAT i.e., proportional to absolute temp (VT=KT/Q) which can cancel out the CTAT nature i.e., with rise in temp.
![2](images/2.jpg) 

**Types of BGR**

Based on architecture there are two times
1. Self-biased current mirror: Stable and simple design but has low PSRR and needs start-up circuit.
2. Using operational amplifier

Based on application BGR is characterised into 4 types
 1.	Low-voltage BGR
 2.	Low-power BGR
 3.	High-PSRR and low noise BGR
 4.	Curvature compensated BGR



## Part 2: Tools and PDK setup

Tools used:
    +	Ngspice: It is used for the transistor level circuit simulation and design.
    +	Magic: It is used for layout design and parasitic extraction

Both Ngspice and Magic are open-source tools which need to be downloaded and installed to the work environment.   
    
Development Flow and tool used:
 ![3](images/3.jpg) 
 
Next, we need we have to clone the google skywater pdk. On the terminal type git clone https://github.com/google/skywater-pdk-libs-sky130_fd_pr.git or Git clone https://github.com/silicon-vlsi-org/eda-technology

![4](images/4.jpg) 

Once all tools and pdk are set up ensure all tools are working properly.

+	Checking all model file.    
	![5](images/5.jpg)      
+ Checking Magic Layout generator. 
![6](images/6.jpg)   
+ 	Checking Netgen (used to check LVS
![7](images/7.jpg)





## Part 3: Design spec and data analysis
First thing before getting into design is to define the specifications. The device needs to be operated with in the specifications. For BGR below mentioned are the general specifications.
