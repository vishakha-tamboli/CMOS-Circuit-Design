# CMOS-Circuit-Design and SPICE simulation using SKY130

### VirtualBox Setup


1. Install VirtualBox <br/>
   - Download and install VirtualBox from the official website: https://www.virtualbox.org/wiki/Downloads

2. Create a Virtual Machine <br/>
   - Open VirtualBox
   - Click New
   - Set the following:
   - 

   | Setting |  Value |
   |-------- |--------|
   |Type	   |Linux   |
   |Version  |  Ubuntu 18.04 Bionic Beaver (64-bit) |
   
   - Click Next

4. Allocate Memory <br/>

   - Assign RAM as needed (Recommended: 4096 MB)
   - Click Next

5. Attach CMOS VDI File
   - Select Use an existing virtual hard disk file
   - Click the folder icon
   - Browse and select the unzipped CMOS VDI file
   - Click Open → Next → Finish <br/>
  
   <img width="500" height="500" alt="Screenshot 2026-02-19 092517" src="https://github.com/user-attachments/assets/d2a58f1e-c8c5-491d-b434-b8cdb04c108d" />

5. Start the Virtual Machine <br/>
   - Select the created VM
   - Click Start


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
  
  
  when we increase Vgs,  the depletion region increase in both the cases. But, in second case as there is Vsb +ve, few charges from channel will be pulled towards   the source. <br/>
                              

  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/3932925f-0ae3-4710-b48d-48f3ca2b74ce" />  <br/>

  Because of this, the formation of surface inversion is slower in the second case. Therefore, an additional potential must be applied in the second case to         achieve inversion.

  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/39fc86c7-b6cb-4913-81c7-b2e8931d0f08" /> <br/>


  
  we see that (V_t) depends on the body-effect coefficient (\gamma), the Fermi potential (\phi_f), and the applied body bias (V_{SB}). When (V_{SB}) increases,      more depletion charge forms in the substrate, so a    higher gate voltage is required to create strong inversion and turn the device ON.

  The parameters such as Gamma comes from foundaries after simulation of which in SPICE we get the value for Vt (Threshold Voltage).
  

  <img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/f294e8af-d5e9-4937-9a81-0286b7a673c5" />  <br/>
 


  ## 4. Lecture-1   Resistive region of operation with small drain-source voltage

  MOSFET main operating regions are:

 - Cutoff Region

 - Linear/Resistive Region

 - Saturation Region

  ## Linear/Resistive Region - 

 we will see the "Resistive region"/"Linear Region" of operation by applying Drain-source voltage. If we keep on increasing the Gate-source voltage, the channel    width keeps on increasing.
 

 <img width="600" height="400" alt="Screenshot 2026-02-18 141437" src="https://github.com/user-attachments/assets/11e7e4f6-9632-4c1e-83b0-548751e68575" />  <br/> 
 
                                                                                                                                                                  
  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/33bbd97c-3bd1-415e-a632-85c6f3c3d70e" /> <br/>   

  
  This indicates that the net induced charge is proportional to (Vgs − Vt). Now, let us apply a very small Vds initially. Assume Vt = 0.45    V, and keep Vgs also      small at the beginning. -- 
  - the source is grounded and Drain is at some potential, so there will be a voltage gradient accross the channel.
  - Assume the effective channel length is L. Let the x-axis lie along the channel length and the y-axis be perpendicular to it.
  - Here, the y-axis represents the width of the transistor, while the x-axis corresponds to the voltage variation along the channel.
  - Let V(x) represent the voltage at any point x along the channel.
  - When Vds is applied, the voltage at each point along the x-axis changes with respect to Vgs − V(x), and this determines the current equation.
  - At x = 0: Vgs = 1, V(x) = 0  ⇒ (Vgs - V(x) = 1).<br/> 
    At x = Vds = 0.05  ⇒ (Vgs - V(x) = 0.95).
  - Induced charge is proportional to the effective channel voltage ( Vgs- V(x)).
    
                                                                                                                                                        
 <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/77a3cccc-7699-4145-a0a0-f864fedc6522" />  <br/>


 
 ## 5. Lecture-2  Drift current theory
 
 Induced charge at any point x in the channel depends on the effective gate voltage. <br/>
 
 <img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/170b037c-2adc-4538-966c-f208cf52ebbd" /> <br/>
 


 <img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/db226874-837a-4b45-a0a8-7d61c0ef1e50" /> <br/>

 -  εox is the oxide permittivity = 3.97εo = 3.510e-11 F/m
 -  tox is the oxide thickness,Comes from the technology node.


  <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/8bd995d0-5b39-4c03-bb17-34903979abcb" />  <br/>
  
   Here we will talk abour drift current , there is Drift current as there is potential difference across the channel. <br/>
   To observe the actual channel width, we need to look at the top view :
 
   <img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/a42f8647-4e9c-49ad-9e73-5e3e12bd5b7f" />
   


   ## 6. Lecture-3 Drain current model for linear region of operation

   -  Voltage varies along the channel length.

   -  This causes the carrier velocity to change along the channel.

   -  Carrier velocity depends on mobility and electric field

 
      <img width="300" height="500" alt="image" src="https://github.com/user-attachments/assets/620d51c2-1f0b-4934-b168-676bae9f03cc" />

  
   - dx limits: 0 → L - covers the entire channel length.
   - dV limits: 0 → (Vds) - voltage rises from source (0) to drain (Vds) along the channel. <br/>
   
     We integrate over these limits to calculate total current through the full channel.

     <img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/a3fc9ad7-25af-4d46-a84e-f387e71584aa" />
  - Current is not purely linear in Vds , The presence of the Vds^2/2 term makes ID non-linear with Vds, even in the so-called linear  region.
  - Instead of writing μnCox repeatedly, we define kn′ = μnCox. This is called process transconductance, since it depends only on fabrication technology.
  - Then we combine geometry (W/L) with kn′: kn = kn′(W/L). This simplifies the drain current equation.

    <img width="300" height="200" alt="Screenshot 2026-02-19 100345" src="https://github.com/user-attachments/assets/fc126ca7-830e-4abd-bf22-db41b8c1c554" />

    
    the equation is still nonlinear because the Vds^2/2 term is still present.

    <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/65cf2973-2189-47a3-a095-ca15d11acc23" />

    ## 7. Lecture-4  SPICE conclusion to resistive operation

     We want to study how Vds and Vgs affect the drain current. For this, we take different values of Vgs and Vds. When varying Vgs, the device stays in the linear region only if( Vgs - Vt​ )>= Vds.
     Vds can be sweeped from 0V to (Vgs-Vt)V to make the device work in linear region of operation.



    <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/837eb632-eb40-4a1b-a64b-dc09dd09583b" />

    ## 8. Lecture-5  Pinch-off region condition

    The chanel voltage is denoted with Vgs-Vds

    - There is  region of operation that occurs when the drain–source voltage becomes greater than ( Vgs - Vt​ ), known as the saturation region. Since the channel voltage is (Vgs - Vds), we now increase Vds.<br/>
      When Vgs-Vds is greater than Vt, there will be a conducting channel.
      


     <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/92294654-2873-4550-9df1-494fda66eac3" />
	 

    - Pinch-off condition is when Vgs-Vds=Vt
       When the pinch-off phenomenon begins, the channel starts to disappear. Initially, the channel vanishes from the drain side, forming a triangular shape.
      

     <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/c743df5a-66c9-4cb8-af39-33208772789c" />

	 


	 

	
	


     

	

    

    

    

  


    

    


     






	​

​

     



   

   




 

                                                                                                                                                                    







   
  
  
  




 
 

 


    


    

 

 
 
 

 

 


  




  

