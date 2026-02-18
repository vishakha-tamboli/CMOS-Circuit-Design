# CMOS-Circuit-Design and SPICE simulation using SKY130

## Day 1 - Basics of NMOS drain current (Id) vs drain-to-source voltage(Vds) <br/>
## 0. Lecture-1   Why do we need SPICE simulations?

Circuit design involves arranging transistors  and resistors to create logic gates (AND, OR, NOT, NAND, NOR, XOR), which are then combined in a particular fashion to form complex, functional digital circuits like microprocessors. <br/>
Example : 
- CMOS Inverter circuit made of using  <br/>
          - One PMOS (Pull-Up Network, PUN) transistor  <br/>
          - One NMOS (Pull-Down Network, PDN) transistor <br/>

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/f12d74f1-962a-4077-b284-4f136eeab583" /> <br/>
 this circuit performs invertor operation:

  Input = 0 → PMOS ON, NMOS OFF → Output = VDD (1)

  Input = 1 → PMOS OFF, NMOS ON → Output = 0


### SPICE Simulation 
 Use to test and analyze electronic circuits on a computer before building them physically.

  NMOS and PMOS transistor Characteristics curve :

 - By modifying the structure of the Pull-Down Network (PDN) and Pull-Up Network (PUN), different CMOS logic circuits can be implemented.

 - Applying a range of input voltage values to the circuit allows us to study its electrical behavior.

 - From this analysis, the corresponding current–voltage (I–V) characteristics curve of the circuit is obtained.

 - The I–V graph shows how the circuit responds to different input conditions and operating regions.
  
  <img width="500" height="300" alt="Screenshot 2026-02-17 110459" src="https://github.com/user-attachments/assets/aa3f370e-8b04-4df1-9ae1-b71e41a74247" />  <br/>
 
  
  

SPICE numerically solves the circuit at each input step considering both PMOS and NMOS operation.

By merging these responses, the overall CMOS inverter waveform is generated. SPICE gives a delay curve for NMOS/PMOS.This curve shows how delay changes with W/L :

 <img width="500" height="200" alt="Screenshot 2026-02-17 111235" src="https://github.com/user-attachments/assets/27dd897c-17fd-4dc6-b0e5-304be216a6db" />

 ### Why we need SPICE simulation ?
 Let's take an example of buffer circuit :<br/>
- The circuit shown below includes buffers added to drive various capacitive loads at the output.
- Delay is evaluated for different input slew values and output load capacitances.
- These delay tables are later used by Static Timing Analysis (STA) tools for chip timing verification.
 
 
 <img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/580ff9b8-ec9c-4ba9-8cda-0b43158ef715" />

 1. Where does the delay table of a cell actually come from? <br/>
    SPICE is the Source of cell delay,it simulates real device physics to give the true transistor-level delay.
    

 2. We learned delay models, but are the models accurate?<br/>
    Delay models are approximate SPICE gives accurate results to build delay tables.

 3. How do you verify STA results are correct?<br/>
    To check STA correctness, we compare STA delay with SPICE delay. <br/>



 ## 1. Lecture-2    Introduction to basic element in Circuit design – NMOS
 ### NMOS structure : 

- 4 terminal Device

- Consists of P-Substrate

- Isolation Region (SiO2)

- n+ Diffusion Region

- Gate Oxide

- Poly-Si or metal gate

- G – Gate

- S – Source

- D – Drain

- B – Body

 <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/ae7298a9-9096-41dc-8ace-e13aaa7b9e25" />  <br/>  

 
 

  ## 2. Lecture-3   Strong inversion and threshold voltage
   
 Initially -  
- Vgs = 0

- Drain, Source, Bulk connected to GND

- Substrate-Source (B-S) and Substrate-Drain (B-D) form p-n junction diode

- Both junctions are ‘off’ due to 0V bias

- Hence, S-D resistance is ‘high’

after - 

- Apply +ve Vgs voltage

 <img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/d76c1ebc-d734-4a2c-b6d9-db48ea69f849" /> <br/>  
 
 
- Increase gate voltage ‘Vgs’
  
- When a sufficiently positive gate-to-source voltage (Vgs) is applied, electrons accumulate near the gate oxide.

  
 ### Strong inversion - 
  The surface under the gate changes from p-type to n-type, forming an inversion layer.This phenomenon is called ‘strong inversion’. <br/> 
  
 <img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/85ae483b-047e-44d9-b0e5-321dc044f7cc" /> <br/> 
 
 ### Threshold Voltage - 
  The ‘Vgs’ voltage at which ‘strong inversion’ occurs is called threshold voltage (Vt).
  

 Further, increase ‘Vgs’

- No Change in depletion layer width

- Electrons from heavily doped ‘n+’ source region are drawn in region under gate ‘G’

- Continuous n-channel formation from S-D, whose conductivity is modulated by ‘Vgs’.

when we change the potential of Body terminal.There will be increase in depletion region between source and body terminal.
 

 <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/5c67337a-9a60-4b19-8bdf-65f6ac4c241c" /> <br/>
 


 
  ## 3. Lecture-4   Threshold voltage with positive substrate potential
  
  
  when we increase Vgs,  the depletion region increase in both the cases. But, in second case as there is Vsb +ve, few charges from channel will be pulled towards the source. <br/>
                              

  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/3932925f-0ae3-4710-b48d-48f3ca2b74ce" />  <br/>

  Because of this, the formation of surface inversion is slower in the second case. Therefore, an additional potential must be applied in the second case to achieve inversion.

  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/39fc86c7-b6cb-4913-81c7-b2e8931d0f08" /> <br/>


The threshold voltage (V_t)  increases when the source–body voltage (V_{SB}) is positive. This effect is called the **body effect**.
]
we see that (V_t) depends on the body-effect coefficient (\gamma), the Fermi potential (\phi_f), and the applied body bias (V_{SB}). When (V_{SB}) increases, more depletion charge forms in the substrate, so a higher gate voltage is required to create strong inversion and turn the device ON.

The parameters such as Gamma comes from foundaries after simulation of which in SPICE we get the value for Vt (Threshold Voltage).
  

 <img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/f294e8af-d5e9-4937-9a81-0286b7a673c5" />  <br/>
 


  ## 4. Lecture-1   Resistive region of operation with small drain-source voltage
  
  




 
 

 


    


    

 

 
 
 

 

 


  




  

