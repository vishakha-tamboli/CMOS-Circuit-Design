# CMOS-Circuit-Design and SPICE simulation using SKY130

### VirtualBox Setup


1. Install VirtualBox <br/>
   - Download and install VirtualBox from the official website: https://www.virtualbox.org/wiki/Downloads

2. Create a Virtual Machine <br/>
   - Open VirtualBox
   - Click New
   - Set the following:
    

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

  Because of this, the formation of surface inversion is slower in the second case. Therefore, an additional potential must be applied in the second case to achieve inversion.

  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/39fc86c7-b6cb-4913-81c7-b2e8931d0f08" /> <br/>


  
  we see that (V_t) depends on the body-effect coefficient (\gamma), the Fermi potential (\phi_f), and the applied body bias (V_{SB}). When (V_{SB}) increases, more depletion charge forms in the substrate, so a    higher gate voltage is required to create strong inversion and turn the device ON.

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

  We want to study how Vds and Vgs affect the drain current. For this, we take different values of Vgs and Vds. When varying Vgs, the device stays in the            linear region only if( Vgs - Vt​ )>= Vds.
  Vds can be sweeped from 0V to (Vgs-Vt)V to make the device work in linear region of operation.



  <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/837eb632-eb40-4a1b-a64b-dc09dd09583b" />


  ## 8. Lecture-5  Pinch-off region condition

   The chanel voltage is denoted with Vgs-Vds.
  - There is  region of operation that occurs when the drain–source voltage becomes greater than ( Vgs - Vt​ ), known as the saturation region. Since the               channel  voltage is (Vgs - Vds), we now increase Vds.<br/>
    When Vgs-Vds is greater than Vt, there will be a conducting channel. <br/>
      


   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/92294654-2873-4550-9df1-494fda66eac3" /><br/>
	 
	 
  - Pinch-off condition starts when Vgs-Vds=Vt When the pinch-off phenomenon begins, the channel starts to disappear. Initially, the channel vanishes from the         drain side, forming a triangular shape.<br/>
   
      
   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/1c231569-e037-4eb6-aa1c-0af2473adc8e" /> <br/>
   
   
   - When  Vgs-Vds<Vt, the inversion layer vanishes near the drain, causing the channel to disappear at the drain side . <br/>
   
   
   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/f5c55421-ff86-4703-aa0d-94bded8ca128" /> <br/>


   ## 9. Lecture-6  Drain current model for saturation region of operation

   
   This condition is called the saturation region, where the device becomes saturated and no further increase in drain current occurs despite increasing the drain–source voltage. <br/>
   
  <img width="300" height="200" alt="Screenshot 2026-02-20 000206" src="https://github.com/user-attachments/assets/bba6c59e-03fa-4cda-8a63-627e0fc5c824"/> <br/>
  
    In the saturation region, the channel voltage remains fixed at (Vgs − Vt), and the drain current becomes independent of Vds. To obtain the drain current  equation in this region, Vds is replaced by (Vgs − Vt).
	
  <img width="700" height="500" alt="Screenshot 2026-02-19 235606" src="https://github.com/user-attachments/assets/57d42bb2-31cf-4963-898a-5ad0fe54cbc8" />

  - As Vds increases, the depletion region near the drain expands.
  - This expansion reduces the effective conductive channel length (channel becomes slightly shorter).
  - Because of this effect, the current is not perfectly constant in saturation (so it is not an ideal current source).
  - The small increase in current with Vds is called channel length modulation.
  - Due to channel length modulation, drain current slightly increases even in saturation.
  - A more accurate drain current equation including this effect is:
       
  <img width="200" height="50" alt="image" src="https://github.com/user-attachments/assets/eda1685e-e333-40f4-9b76-cf2b81029ca3" />

 
  - Here, λ (lambda) represents the channel length modulation parameter.



   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/5f9a7f30-1260-473f-b920-12eb5a383913" />  <br/>

	  
	  



   ## 10. Lecture-1  Basic SPICE setup
   
   - In SPICE simulation, we provide model parameters (device physics parameters like (V_{t0}), mobility, (k_n), (\lambda), etc.).

   - We also provide the netlist, which defines the circuit connections, transistor sizes (W/L), and input sources.
     
   - SPICE uses these parameters and equations internally to solve the circuit numerically.

   - It generates voltage and current waveforms at different nodes of the circuit.

   - From these waveforms (input and output transitions), we calculate the propagation delay of the device.

   - Hence, SPICE gives realistic delay values based on actual device physics and circuit conditions.


   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/83067699-6dbe-4b2e-afae-57650e5f3ce7" />



   ## 11. Lecture-2  Circuit description in SPICE syntax

   ##### Define Nodes

   A node is a point where two or more terminals are electrically connected. If two terminals of the same device are short-circuited, they form a single node         between them. In most cases, a node connects terminals of different devices.

   To identify nodes in a circuit, observe all the wires connecting components—each continuous wire represents one node. These node names are then used while         writing the SPICE netlist.




   <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/3a5007e6-a655-4c91-aa07-9f4941c8833c" />


   ##### MOSFET Syntax

   The order of writing is: Drain, Gate, Source, Substrate
   Mname Drain Gate Source Substrate Model W= L=

   <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/69830e49-9e7f-4006-b508-a99d0d91fa64" />


   ##### Resistor Syntax

   A resistor is connected between two nodes.

   Rname Node1 Node2 Value
   
   <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/f2174825-ee34-4cfd-a471-993cc9b0abce" />

   ##### Voltage Sources

   Voltage sources are written between a node and ground

   Vname PositiveNode NegativeNode Value

   <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/1cc7dce1-46ff-4232-9d50-d65390df7c85" />
   


   ## 12. Lecture-3  Define technology parameters


   ### Important Note About Model Name in SPICE
  - The model name given in the `.MODEL` statement must be exactly the same as the name used in the MOSFET instance line.

  - For example:

  ```
  .MODEL nmos NMOS ( ... )
  ```

  Then in the transistor line we must write:

  ```
  M1 vdd n1 0 0 nmos W=1.8u L=1.2u
  ```

 - The name **`nmos`** should match in both places.

 - If the names are different, SPICE will not recognize the model and the simulation will give an error.

  <img width="300" height="200" alt="Screenshot 2026-02-22 221226" src="https://github.com/user-attachments/assets/bf04c693-72a3-4788-9914-0e4d6d1ee9eb" />


 - The brackets in the `.MODEL` statement contain the technology parameters of the NMOS device.

 - Similarly, the PMOS model also includes its respective technology parameters inside its brackets.


 <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/37116cc4-8306-4a72-8d12-8188d4d73860" />


  Now, we save these model definitions into a `.mod` file and then include this packaged file in the top-level SPICE netlist for simulation.
  

  <img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/ce8e14f4-2adc-410e-ba41-605e40f1b0d8" />


 - The netlist defines the MOSFET (M1), resistor (R1), and voltage sources (Vdd, Vin) with their node connections and values.

 - The MOSFET uses a technology model file included through the `.LIB` statement.

 -  The model file contains the CMOS device parameters required for accurate simulation.
 -  For simulation, we sweep the values of  Vgs or Vds to obtain the device characteristics.


  ## 13. Lecture-4  First SPICE simulation
  
  Open VirtualBox and navigate to the required directory using the cd command.

  Clone the repository using:
  - git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git

  <img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/dd6dda73-3cc9-41c8-bab9-7b9171084958" />

  
<img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/3581a8ad-c957-4745-92a6-bd1459d872ae" />


 - Inside the sky130_fd_pr directory, you will find cells, models, and tech files. The cells foldercontains device structures like nfet and pfet, which will be used for simulations.

 - Within the nfet folder, multiple SPICE libraries are available for different process corners. From these, select a suitable typical (TT) corner library for simulation

    
 <img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/2ad8c948-01cd-4a23-8fb8-9a46b0736a82" />

 - We can observe all the model parameters that are required for the fabrication process.

 <img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/a8245523-1a47-4d47-b878-07038aec4fa7" />  <br/>
 

 <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/a5c88a30-393b-47d0-ac47-1ec1f9300192" /><br/>
 

 <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/55af8304-09cf-4643-ac43-cca80cdb3670" />

  Various predefined values of W (width) and L (length) are available in the library. For the simulation, we can choose any one of the listed W and L combinations provided.


 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/a5945537-0c3f-41d0-a285-52e20eb13438" />




- Navigate to the models directory and open the lib.spice file.

- Inside it, you will find the library files for both nfet and pfet devices.



 <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/53efbeeb-946e-45c2-ab2d-cca60c1ff35a" />
 
 - The file also contains different process corner libraries, such as Typical (TT), Slow-Fast (SF) and Fast-Fast (FF) corners.

 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/6cf2e101-a8ce-4028-b208-3ac1e4bf721e" />

 Inside design --> open day1 file.


 
 <img width="700" height="500" alt="Screenshot 2026-02-23 141443" src="https://github.com/user-attachments/assets/7a6ebc7b-24ae-497f-85fe-bc78397c6cee" />

 - Here,Vdd is swept from 0 V to 1.8 V with a step size of 0.1 V.

 - Vgs is varied from 0 V to 1.8 V with a step size of 0.2 V.

 - Now, we proceed to perform the SPICE simulations.

 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/6e6b9e5a-33d6-4028-8014-293460c5abde" /> <br/>

 <img width="200" height="50" alt="image" src="https://github.com/user-attachments/assets/b1d8d7f9-3fd4-4030-884c-7db92f84390a" /><br/>

 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/171875b8-4d82-4616-9dd2-dc7a6b0c0e9f" />

 - To check the value of Id at any specific point on the curve, left-click on the desired point.

 - The terminal window will display the corresponding coordinates as x0 and y0.

 - The y0 value represents the drain current Id in amperes.


  ## 14. Lecture-5  SPICE Lab with sky130 models

  
 - When you click on any point on the plotted curve, the corresponding values are displayed in the terminal window.

 - As shown in the image, the terminal displays x0 and y0 values for the selected point.
  
 - The y0  value represents the drain current (Id), and the x0 value represents the corresponding voltage at that point on the graph.


  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/f8ac9381-20c6-4901-840f-2747cceb5bc7" /> <br/>
  

  


  ## Day 2 - Velocity saturation and basics of CMOS inverter VTC  <br/>
  
  ## 1. SPICE simulation for lower nodes and velocity saturation effect


  ## 15. Lecture-1   SPICE simulation for lower nodes

 - In the graph, the region to the left of the curve (Vds = Vgs − Vt) represents the Linear (Triode) region, where the drain current increases almost linearly with Vds.

- The region to the right of the curve represents the Saturation region, where the current becomes nearly constant, with only a slight increase due to velocity saturation effects.

- The bottom region, where the current is almost zero, represents the Cut-off region.

- In these different regions, the MOSFET behaves completely differently in terms of current    conduction and operation.

- This behavior corresponds to a long channel device condition.


 <img width="700" height="500  " alt="image" src="https://github.com/user-attachments/assets/948fb57e-beef-4f7c-960c-c449e04cb519" />


 Now we will take lower node case 

 <img width="200" height="56" alt="image" src="https://github.com/user- attachments/assets/85a907c5-e27b-4dcb-a9df-997267c1964c" />

 For this will take new SPICE dec , but diffrence between this new and previos one is only that now W and L values are changed

  
  
 <img width="300 " height="200" alt="image" src="https://github.com/user-attachments/assets/7cd7e428-e848-489a-a491-44be92e8c9f8" />

 Difference between Small Node and Large Node MOSFET Output Characteristics

1. In the small node device, a slight step or abrupt increase in drain current is observed near the cutoff region, while the large node device shows a smoother transition.

2. In the saturation region, the spacing between the ( I_D ) curves is nearly the same in both graphs.

3. The drain current ( I_D ) magnitude is different for both devices; the large node device shows higher current compared to the small node device.







  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/34231483-6c77-4ab2-9020-0504ee44787d" />



 ## 16. Lecture-2   Drain current vs gate voltage for long and short channel device
 

 ##### Observation 1 :

 1. The graph shows that in saturation, the drain current ( I_D ) increases more rapidly as ( Vgs ) increases.

2. The spacing between successive ( I_D ) curves becomes larger at higher ( Vgs), indicating a nonlinear rise in current.

3. This behavior reflects the quadratic dependence of ( I_D ) on ( Vgs) for a long channel device.



 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/33ec6b3d-dbf6-4804-abcd-5c2cbc39c95f" />

 Small Node Device (W = 0.375µ, L = 0.25µ)

1. At ( Vds \approx 2.5,V ), ( I_D ) increases nonlinearly with ( Vgs ).
2. The curve spacing is uneven, indicating quadratic dependence.

 <img width="891" height="501" alt="image" src="https://github.com/user-attachments/assets/fcc5ee5f-e58c-4732-baa2-0f05c8948621" />

1. At ( Vds \approx 2.5,V ), ( I_D ) increases almost uniformly with ( Vgs ).
2. The equal spacing between curves indicates linear dependence due to velocity saturation.


<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/9c41fc47-a9f8-4177-bbe9-91575fc9e398" />


1. We plot the graph of ( I_D ) vs ( Vgs ) by sweeping ( Vgs ) while keeping ( Vds = 2.5,V ) constant (or by sweeping ( Vds) if required).

2. In the sweep syntax, the parameter written on the left-hand side is varied for every value of the parameter on the right-hand side.

3. For example, for each value of ( Vdd), ( Vin ) is swept.




<img width="303" height="174" alt="image" src="https://github.com/user-attachments/assets/ca847503-4a49-49ca-8c72-2a8e8f3d96ca" />

for long channel   w=1.8u and L=1.2u


<img width="700" height="500" alt="Screenshot 2026-02-24 113904" src="https://github.com/user-attachments/assets/06ba7166-e16a-4455-aabe-93872eb9b380" />  <br/>


<img width="700" height="500" alt="Screenshot 2026-02-24 113946" src="https://github.com/user-attachments/assets/616a5746-1c73-4a77-aee3-ac4e4f3aa858" />  <br/>


<img width="700" height="500" alt="Screenshot 2026-02-24 113959" src="https://github.com/user-attachments/assets/3b1ba7bb-78a9-429e-82b2-29bb1604fd8f" />  <br/>



for short channel  w= 0.375u and L=0.25u 


<img width="700" height="500" alt="Screenshot 2026-02-24 114202" src="https://github.com/user-attachments/assets/1755304b-dcc6-46ff-9597-b7465bcdadb0" />  <br/>

<img width="700" height="500" alt="Screenshot 2026-02-24 114219" src="https://github.com/user-attachments/assets/f6b25ac4-b006-4729-992d-240f986f7ff1" />  <br/>

<img width="700" height="500" alt="Screenshot 2026-02-24 114232" src="https://github.com/user-attachments/assets/59faf0af-9be4-476e-b00c-b0de725ce435" /> <br/>

<img width="500" height="500" alt="Screenshot 2026-02-24 114247" src="https://github.com/user-attachments/assets/eb1a5328-6739-4200-8477-cea94dc491ab" />  <br/>




 ## 17. Lecture-3   Velocity saturation at lower and higher electric fields


 1. As we have seen previously, the long channel device (W = 1.8µ, L = 1.2µ) shows a quadratic relationship between ( Id ) and ( Vgs ) in saturation.

2. The short channel device (W = 0.375µ, L = 0.25µ) shows an almost linear increase of ( Id) with ( Vgs ).

3. This linear behavior occurs due to the velocity saturation effect in short channel devices.

 
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/a63a9387-0e2d-4e6b-86ad-39ccc633016f" />

The graph shows that carrier velocity increases linearly with electric field at low fields (( v = \mu E )), but at high electric fields it reaches a saturation velocity (( v_{sat} )) due to velocity saturation effect.




<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/b9deee7f-97c2-4bb7-aa54-a82e707ba0f1" />  <br/>


<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/376d86b3-65ab-41d4-a1be-153a121fa2ad" />

To get the continuty point will eqate (E=Ec)


<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/178a647e-15d2-474f-8df8-e9ad69281669" />


We have rederived the drain current eqation using the boundary condition for electric field


<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/5d00d688-cabb-4065-9fb7-b41c443c8124" />  <br/>

the drain current eqation becomes complex


<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/dbcc2370-4c54-48ae-a83f-a73e6dac719a" />

To simlify this , lets come up with one model

operations regions for short and long channels 

there is only velocity saturation operation region get , changes whereas all operation remains same 


<img width="300" height="200 " alt="image" src="https://github.com/user-attachments/assets/7f43d634-ded4-46f7-b5ba-d22141025217" /> <br/>


<img width="655" height="324" alt="image" src="https://github.com/user-attachments/assets/d21d3a1c-115e-4ce0-949e-bba7286993bd" /> <br/>







 ## 18. Lecture-4  Velocity saturation drain current model




<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/cf8bd285-5b6d-4784-aeea-92317abb9083" />

- The yellow-marked term ( V_dsat ) represents the velocity saturation voltage, a technology-dependent parameter.

- It defines the drain voltage at which carrier velocity saturates and current no longer increases linearly with ( Vds ).

- In short-channel devices, ( V_dsat) limits the current before the classical pinch-off condition occurs.

For example

if Vgt = minimum value 


- When ( V_{gt} ) is the minimum value, it means it is the limiting term in the expression.

- This implies that ( Vds ) has increased sufficiently and is no longer the limiting factor.

- Hence, the device operates in saturation where current is mainly controlled by ( Vgt ), not     by further increase in ( Vds ), and true for both the channel (long and short )


<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/58cacdef-0c07-4bcd-bf70-01df00303723" />




if Vds = minimum value 


- Here, ( Vds )  is the minimum value among the terms.

- This means the drain voltage is the limiting factor in determining the drain current.

- The device operates in the linear (resistive) region, where current is mainly controlled by (   Vds ).




<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/bc239ef9-e9fa-411d-994b-6e697b32d9fd" />

if  V_dsat = minimum value 


- This expression represents the drain current model for a short channel node.

- Here, ( V_{min} = \min (Vgt, Vds, V_dsat) ), meaning the smallest of these voltages limits     the current.

- The term ( V_dsat ) accounts for short-channel effects, modifying the current behavior compared to long-channel devices.

- The factor ( (1 + \lambda Vds) ) includes channel length modulation effect.




<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/18cd44f8-d67b-49e0-b5c5-9235b9162590" />

Now will expand the eqation 


- Ideally, if W is kept constant and L is reduced, the drain current  Id should increase because <img width="50" height="30" alt="image" src="https://github.com/user-attachments/assets/f6f14445-1133-4c93-8747-b1d523284dc0" />


- However, in short channel devices, this increase is not proportional due to velocity saturation and other short-channel effects.

- As a result, the drain current does not increase as much as expected from the simple long-channel equation.



<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/7a393410-43ab-4ec6-ba5d-2ad40a241018" />




 ##### Observation 1 :


 - In long channel devices, saturation occurs at higher ( Vds} ), so the saturation region comes later.

- In short channel devices, saturation occurs at lower ( Vds ), so the device enters saturation earlier.

- As channel length decreases, the transition from linear to saturation region shifts toward smaller drain voltages.

- This early saturation in short channel devices is due to strong electric field effects.



<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/979ebd16-38b7-4123-983c-8098e4d8d326" />



 ## 19. Lecture-5 Labs Sky130 Id-Vgs 

Now we will perform the simulation for lower technology nodes using the Day 2 design file. 
 Id vs Vds

Open the file day2_nfet_idvds_L015_W039.spice.


<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/a52cbe9b-f1c7-4045-9e26-99447294b95d" />

 simulation is being done 
 for  w=0.39u and L=0.15u


 <img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/2792e0c2-a0a4-40b2-8804-c01f9a15b3b5" />  <br/>

 <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/165f5339-20f5-469d-8d14-098b4d4d2226" />  <br/>



- The plot shows  Id vs Vds for different values of  Vgs .

- For lower values of  Vgs , the drain current follows a quadratic dependence on  ( Vgs - Vt ).

- For higher values of ( Vgs ), the behavior becomes more linear due to velocity saturation in    short-channel devices.

- The peak current is approximately 197 µA. To observe the peak current at ( Vgs = 1.8 , V ),     simply left-click on the curve corresponding to ( Vgs = 1.8 , V ).


Open the file day2_nfet_idvgs_L015_W039.spice and perform DC simulation using ngspice.

Keep ( Vds = 1.8 , V ) and sweep  Vgs  from 0 V to 1.8 V with a step size of 0.1 V.


<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/9fa61539-d61e-47ec-a6c7-8bf140780b13" />  <br/>

<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/7e22cbff-7e02-4f5b-8dde-d1a0dc14039f" />



 ## 20. Lecture-6  Labs Sky130 Vt

 Now we will determine the threshold voltage ( Vt ) from the ( Id ) vs ( Vgs ) curve.

From the graph, ( Vt ) is identified as the point where the drain current starts increasing sharply for a small change in ( Vgs ).

To find it accurately, we draw a tangent to the curve in the steep region and note the intercept point.

<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/1531616a-5110-4127-abc0-0b886b1e85a4" /> <br/>

The threshold voltage( Vt  is approximately 0.76 V, as obtained from the tangent drawn to the  Id  vs  Vgs  curve.




  <img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/8c47e884-673d-46cb-a196-58d138540e4a" />  <br/> 



 ## CMOS voltage transfer characteristics (VTC)

 ## 21. Lecture-1   MOSFET as a switch

 



  



 



 

















 

 



 






















 







 





 






  




  























 


 
























  


   


















 


  





 



 


   

 



   




  


  



  


    


  


 

 











 


  

  

  


  

  


 

   

 





   




 

 

 



 

 




 

 

 



  



 










   



 



 




   


   

   


   


   

   





   




	



	




      
    






	 

	 


      



	 


	 

	
	


     

	

    

    

    

  


    

    


     






	​

​

     



   

   




 

                                                                                                                                                                    







   
  
  
  




 
 

 


    


    

 

 
 
 

 

 


  




  

