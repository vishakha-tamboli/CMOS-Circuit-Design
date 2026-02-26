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


 - A transistor operates only when the magnitude of gate-to-source voltage exceeds the threshold voltage, i.e., ( |Vgs| > Vt ).

- The modulus sign is used because ( Vgs ) is positive for NMOS and negative for PMOS devices.

- When ( |Vgs| ) is less than ( Vt ), the device remains in the OFF (cutoff) region.

- The device turns ON and allows current to flow only when ( |Vgs}| ) becomes greater than the threshold voltage.


<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/ad8e7c2f-f959-4009-881a-9b8d72fbdb6b" />


Now will see CMOS( Complementary MOSFET)

When Vin is high and equal to Vdd


- For the PMOS (upper transistor), the gate-to-source voltage is determined by ( Vin ) and ( Vdd ), since the source of PMOS is connected to ( Vdd ).

- For the NMOS (lower transistor), the gate-to-source voltage is determined by ( V_{in} ) and ( Vss ) (ground), as its source is connected to ( Vss ).

- Thus, in a CMOS inverter, ( Vin ) controls both transistors by forming ( Vgs ) with ( Vdd ) for PMOS and with ( Vss ) for NMOS.



<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/a2ecbe0c-9cf0-4646-a443-e10ca3002793" />


 ## 22. Lecture-2  Introduction to standard MOS voltage current parameters

 When Vin is low and equal to ov 

 - When a high voltage is applied at ( Vdd ) and ( V_in ) is kept low, the PMOS source is at ( Vdd ) and the gate is at a lower potential.

- This makes ( Vgs ) negative, and for the PMOS to turn ON, ( Vgs ) must be more negative than its threshold voltage (i.e., ( Vgs < V_t ), where ( Vt ) is negative).

- Under this condition, the PMOS transistor turns ON and allows current to flow from source to drain.





 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/2897ce77-b051-4491-935e-4e9801984de0" />  <br/> 

 When ( Vin = Vdd ), a conduction path exists between ( Vout ) and ( Vss ), causing the load capacitor ( C(load) ) to discharge.



 <img width="600" height="200" alt="image" src="https://github.com/user-attachments/assets/5a27dfb2-86da-49a2-aa12-e9ec70b10f7d" />  <br/> 


 <img width="300" height="500" alt="image" src="https://github.com/user-attachments/assets/82cd9a2d-e3f9-40b5-9cff-479e5ef693e3" />  <br/> 
 

 When ( Vin = 0 ), a conduction path forms between ( Vdd ) and ( Vout ), causing the load capacitor ( C(load) ) to charge, and ( Vout ) rises to ( Vdd ).



 <img width="600" height="200" alt="image" src="https://github.com/user-attachments/assets/51136925-941e-471c-9532-85a0e6e7cd9b" />   <br/> 


 <img width="300" height="500" alt="image" src="https://github.com/user-attachments/assets/e4f22e63-c15e-413b-ab4a-f2dab2a2aa52" />   <br/> 

 Let us give the naming convention of the CMOS

 - G = Gate

- S = Source

- D = Drain

- ( Vgs ) = Gate-to-Source voltage

- ( Vds ) = Drain-to-Source voltage

- ( Vgsn ) = Gate-to-Source voltage of NMOS

- ( Vgsp ) = Gate-to-Source voltage of PMOS

- ( Vdsn ) = Drain-to-Source voltage of NMOS

- ( Vdsp ) = Drain-to-Source voltage of PMOS

- ( Idsn ) = Drain-to-Source current through NMOS

- ( Idsp ) = Drain-to-Source current through PMOS

- ( Rn ) = Equivalent resistance of NMOS

- ( Rp ) = Equivalent resistance of PMOS

- ( C_L ) = Load capacitance

- ( Vdd ) = Supply voltage

- ( Vss ) = Ground (reference) voltage

- ( Vin ) = Input voltage

- ( Vout ) = Output voltage


<img width="700" height="600" alt="Screenshot 2026-02-25 010212" src="https://github.com/user-attachments/assets/e711eaf9-927b-4787-9840-763663aa7b2a" />



 ## 23. Lecture-3  PMOS/NMOS drain current v/s drain voltage



- ( Vgsn = Vin - Vss = Vin )
- ( Vdsn = Vout )
- ( Vgsp = Vin - Vdd )
- ( Vdsp = Vout - Vdd )

 <img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/3f9671b3-3a13-4ee9-82d6-12fbccfcba26" />  <br/> 


 <img width="100" height="60" alt="image" src="https://github.com/user-attachments/assets/574ffeb8-729c-4f0b-bb31-d448a8b573e6" />

 - As ( Vgsn ) increases (for NMOS) and as the magnitude of ( Vgsp ) increases, i.e., becomes more negative (for PMOS), the corresponding drain current increases in magnitude.

- For small ( Vdsn ) (NMOS) and small ( |Vdsp}| ) (PMOS), the devices operate in the linear (ohmic) region.

- For larger ( Vdsn ) (NMOS) and larger ( |Vddsp| ) (PMOS), both devices enter the saturation region where the drain current becomes nearly constant.


 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/2ae5b85f-0fc4-40bc-bf0d-90e8d906452e" />



  ## 24. Lecture-4  Step1 – Convert PMOS gate-source-voltage to Vin




  - In a CMOS inverter, only Vin and Vout are externally measurable. Internal node voltages of NMOS and PMOS cannot be directly observed, so the Voltage Transfer Characteristics (VTC) and delay analysis must be expressed only in terms of ( Vin ) and ( Vout ).

- To derive the VTC of a static CMOS inverter, assume:

  - Long channel devices
  - ( Vdd = 2V )

 For the PMOS transistor:

  - ( Vgsp = Vin - Vdd )
  - Since ( Vdd = 2V ),
    [
    Vgsp = Vin - 2
    ]
  - Rearranging,
    [
    Vin = Vgsp + Vdd
    ]

- Fixing ( Vgsp ) values and converting them into corresponding ( Vin ):

  | ( Vgsp ) (V) | ( Vin = Vgsp + 2 ) (V) |
  | --------------- | ---------------------------- |
  | 0               | 2                            |
  | -0.5            | 1.5                          |
  | -1              | 1                            |
  | -1.5            | 0.5                          |
  | -2              | 0                            |

- To express PMOS characteristics in the same reference as NMOS:

  - Use ( Vgsp = Vin - Vdd )
  - Use ( Idsp} = - Idsn )

- This transformation allows:

  - PMOS and NMOS characteristics to be plotted using the same variables.
  - Direct comparison and superposition of currents.
  - Determination of the operating point where ( Idn = Idp ).

- By sweeping ( Vin) from 0 to ( Vdd), and equating NMOS and PMOS drain currents, we obtain:

  - The Voltage Transfer Characteristic (VTC)
  - From the VTC, switching threshold and delay behavior can be analyzed.

- Thus, although internal voltages exist inside the inverter, from a user’s perspective only ( Vin ) and ( Vout ) define the inverter behavior and its delay characteristics.

- <img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/b524f829-bd5b-4f62-bfff-19f8ac0f87e3" />






- Rewrite ( Vgsp ) in terms of input voltage:
  [
  V_gsp = Vin - Vdd
  ]
  so PMOS characteristics are expressed using ( Vin ).

- Use current relation:
  [
  Idsp} = - Idsn
  ]
  ensuring equal magnitude and opposite direction for current continuity.

- This converts the PMOS transfer curve into the same variables as NMOS, enabling direct comparison.

- While plotting, corresponding ( Vin ) values (from ( Vin = Vgsp + Vdd )) are used, and PMOS current is represented in terms of ( Idsn ).


  ## 25. Lecture-5  L5 Step2 & Step3 – Convert PMOS and NMOS drain-source-voltage to vout

- The transfer characteristics are initially expressed in terms of ( Vdsp ), which is an internal PMOS voltage and cannot be directly observed.

- To convert it into measurable external variables, we use the circuit relation:
  [
  Vout = Vdd + Vdsp
  ]
  Therefore,
  [
  Vdsp = Vout - Vdd
  ]

- For ( Vdd = 2V ), as ( Vdsp ) varies from −2V to 0V, the corresponding ( Vout ) varies from 0V to 2V.


 <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/4cb69904-86ff-4bce-96f9-2517abbc7b7a" />

- Thus, substituting ( Vdsp ) in terms of ( Vout ) allows the PMOS characteristics to be completely expressed using the external node voltages ( Vin ) and ( Vout ).

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/9ef9472e-99c5-4004-970a-e15e9e5cca37" />


- When ( Vout = 2V ) (with ( Vdd = 2V )), ( Vdsp = 0V ). There is no voltage drop across the PMOS, so the current becomes zero. The load capacitor ( C_L ) is fully charged, representing the steady-state HIGH output condition of the CMOS inverter.

- When ( Vout = 0V ), the magnitude of ( Vdsp ) becomes 2V. The output capacitor ( C_L ) is fully discharged, and depending on ( Vin ), current can flow to charge the node back to HIGH through the PMOS.

- These conditions are valid when PMOS and NMOS operate together as a CMOS inverter, ensuring proper charging and discharging of the output node.

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/6d97d0de-a465-44f3-bc67-fa36d618e1d4" />




* For NMOS, ( V_{GSn} = V_{in} ) and ( V_{DSn} = V_{out} ).

* Since both are external node voltages, the NMOS current equations are directly written in terms of ( V_{in} ) and ( V_{out} ).

* Hence, the NMOS load curve can be plotted directly without any voltage transformation.

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/fb9f5d3c-cbea-48bc-affe-2e81511c8e8b" />


  ## 26. Lecture-6  L5  Step4 – Merge PMOS – NMOS load curves and plot VTC



  <img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/17faa5ca-21a2-46d9-8b06-3751ef0cc8bf" />  <br/>
  
	- To obtain the CMOS Voltage Transfer Characteristics (VTC), the NMOS and PMOS load curves are superimposed.

- For each value of ( Vin ), the operating point is found where the drain currents of NMOS and PMOS are equal in magnitude and opposite in direction.

- The common intersection points of these curves give the relationship between ( Vin ) and ( Vout ), forming the VTC.



<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/fa2c6ace-cdaf-4f20-8450-91de6734f761" />  <br/> 

- Since ( Vdd = 2V ), both ( Vin ) and ( Vout ) vary within the range 0V to 2V.

- ( Vin = 0V ) → ( Vout = 2V ); NMOS is in cutoff and PMOS is in linear region.

- ( Vin = 0.5V ) → ( 1.5V < Vout < 2V ); NMOS is in saturation and PMOS is in linear region.

- ( Vin = 1V ) → ( 0.5V < Vout < 1.5V ); both NMOS and PMOS operate in saturation.

- ( Vin = 1.5V ) → ( 0V < Vout < 0.5V ); NMOS is in linear region and PMOS is in saturation.

- ( Vin = 2V ) → ( Vout = 0V ); NMOS is in linear region and PMOS is in cutoff.



<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/9490a893-6c0d-4c9a-ae44-11f978db7166" />

## Day 3 - CMOS Switching threshold and dynamic simulations


## Voltage transfer characteristics – SPICE simulations


## 27. Lecture-1   SPICE deck creation for CMOS inverter

- To simulate the VTC, we first create a SPICE deck, which contains the circuit connectivity information (netlist).

- The netlist defines the device connections (including substrate terminals), where M1 is the PMOS and M2 is the NMOS.

- It also specifies the input stimulus, technology/model parameters, and the output nodes to be probed for measurement.

- <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/194a79a2-d19d-422d-9d22-cdc1bda20e3b" />  <br/> 

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/5273f57b-2ae5-48ca-a358-4079b43bedfa" />



- The SPICE deck defines the circuit connectivity (netlist) of the CMOS inverter.

- M1 (PMOS) is connected as: `M1 out in vdd vdd pmos W=0.375u L=0.25u`.

- M2 (NMOS) is connected as: `M2 out in 0 0 nmos W=0.375u L=0.25u`.

- It specifies device dimensions, terminal connections (drain, gate, source, body), and supply nodes required for VTC simulation.






<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/a42151f2-7c68-40d8-b54d-f4490c1156d0" />


## 28. Lecture-2  SPICE simulation for CMOS inverter

 The SPICE deck defines the connectivity (netlist) of the CMOS inverter along with supply and device parameters for simulation.

- M2 (NMOS) is defined as: `M2 out in 0 0 nmos W=0.375u L=0.25u`, where drain is connected to output, gate to input, and both source and body to ground.

- It clearly specifies device dimensions (W/L), terminal order (D, G, S, B), and required nodes for VTC analysis.



<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/8e60501c-414f-46ed-8843-71a5f95ff526" />



The DC sweep of the CMOS inverter is performed using the included model file (such as the `.include 250nm_cmos_models.mod`), which provides the NMOS and PMOS technology parameters. Based on this model file, the VTC curve is obtained, showing a sharp transition from high to low output, confirming correct device modeling and inverter operation.



<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/09425543-be68-4877-abb1-c9eeb6475abf" />


 A DC sweep command is used to vary the input voltage from 0 V to 2.5 V with a step size of 0.05 V to obtain the VTC.

 Only the input voltage is swept, and the corresponding output voltage is measured to analyze inverter behavior.

 The simulation is performed with Wn = Wp = 0.375 µm and Ln = Lp = 0.25 µm, giving an aspect ratio (W/L) of 1.5 for both NMOS and PMOS devices.


 <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/54513972-e7d7-4c7a-8049-cd821dbf3b37" />



 The following graph shows the VTC obtained with Wn = 0.375 µm, Wp = 0.9375 µm, and Ln = Lp = 0.25 µm (Wn/Ln = 1.5, Wp/Lp = 2.5). Since the PMOS is 2.5× wider than the NMOS, the switching point shifts due to the stronger pull-up network, affecting the inverter’s transition behavior.


<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/604e8242-d59b-4dac-8160-d036cf0a3725" />


## 29. Lecture-3  Labs Sky130 SPICE simulation for CMOS


- A CMOS inverter is designed using PFET and NFET, with the PMOS having a W/L ratio about 2.33× higher than the NMOS to balance strengths.

- Vin is swept from 0 V to 1.8 V in steps of 0.01 V, and the corresponding Vout is recorded to obtain the VTC.

- After running ngspice, the VTC is plotted using the command: `plot out vs in`.


<img width="500" height="500 " alt="image" src="https://github.com/user-attachments/assets/e1e9ff53-9398-4705-b427-f25e49c34347" />



- The switching threshold (Vm) is the point on the VTC where Vin = Vout. Zoom into the region where the curves appear equal by right-clicking and selecting the area.

- Click near the intersection point; the terminal shows (x0, y0). Since Vin = Vout at Vm, x0 ≈ y0 = Vm.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/68ddd0a7-9855-410b-a355-a5a3fe19a5f6" />

For a W/L ratio of 2.3, the switching threshold (Vm) is approximately 0.876 V, observed at the point where Vin = Vout on the VTC curve.


<img width="645" height="393" alt="image" src="https://github.com/user-attachments/assets/4001f862-bb22-464b-888a-a24b0bc5f7a4" />


Transient analysis is used to measure propagation delays at the 50% output level (0.9 V for 1.8 V supply). The delay is calculated as the time difference between input and output at this midpoint.

Rise delay = 2.482 ns − 2.15 ns = 0.333 ns, and the fall delay is obtained similarly during the falling transition.

From the transient waveform, the fall delay measured at the 50% level (0.9 V) is calculated as:

Fall Delay = 4.334 ns − 4.050 ns = 0.285 ns



## Static behaviour evaluation-CMOS inverter robustness-Switching Threshold

## 30. Lecture-1  Switching Threshold, Vm


<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/2b9c8134-0796-4a8a-9901-a422ef82bcb1" />



- When CMOS inverters with different (W/L) ratios are compared, the overall VTC shape remains almost unchanged, but the switching threshold (Vm) shifts, showing the robustness of the CMOS inverter.

- The switching threshold (Vm) is the point where Vin = Vout. It can be found by drawing a 45° diagonal line on the VTC curve; the intersection gives Vm.

- Vm for (Wp/Lp) = 1.5 ≈ 0.98 V

- Vm for (Wp/Lp) = 3.75 ≈ 1.2 V

- At Vm, both NMOS and PMOS conduct simultaneously as their gate-source voltages are near the threshold region.

- Static behavior analysis includes switching threshold, noise margin, power supply variation, and device variation, indicating stable inverter performance.

<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/365195c4-12af-4483-9800-cb2144f4ec8b" />

From the VTC plot at the switching point (Vm), a few key observations can be noted:

- At Vm, Vin = Vout, hence for both transistors, Vgs = Vds.

- The drain currents of PMOS and NMOS are equal in magnitude but opposite in direction, i.e., IdsP = −IdsN.

- Therefore, the net current at the output node is zero (IdsP + IdsN = 0), indicating equilibrium at the switching threshold.


## 31. Lecture-2 Analytical expression of Vm as a function of (W/L)p and (W/L)n


<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/aca240df-dd24-4fa7-89c2-c49f74fdc937" />

- The channel length modulation term (1 + λVds) is neglected because λ is very small, and including it complicates manual calculations without significantly affecting the result.

- At the switching threshold (Vm), the condition IdsP + IdsN = 0 is applied, meaning the PMOS and NMOS currents are equal in magnitude and opposite in direction.

- Using the saturation current equations (without the λ term) for both transistors, the currents are equated to solve for Vm.

- This simplification allows easier analytical estimation of the switching threshold voltage.

We know the equations for IdsN and IdsP 

<img width="400" height="150" alt="image" src="https://github.com/user-attachments/assets/3c392cfb-739f-49fd-bba4-6bf69369d602" />

Solving the above equation for Vm


<img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/ef42feb1-267b-4439-8bd0-c64a77e96c3c" />





## 32. Lecture-3  Analytical expression of (W/L)p and (W/L)n as a function of Vm

Alternatively, the PMOS-to-NMOS sizing ratio can be determined analytically to achieve a desired switching threshold voltage (Vm).

 <img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/9bae4736-2f78-488d-a43d-42a896e659e2" /> <br/> 

 <img width="600" height="100" alt="image" src="https://github.com/user-attachments/assets/7b174023-2dd3-421c-8d1d-46e6e4c9e66a" /> <br/> 

 <img width="600" height="100" alt="image" src="https://github.com/user-attachments/assets/7cf0336c-e570-4dfa-aa67-21bf4e4e9330" /> <br/> 

 <img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/4a7d06cd-9592-4441-8fb3-be7a0d801c2d" /> <br/>  

 Expanding Kp and Kn

 <img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/33fe1bb1-b94c-4dfc-8bd3-747e38508936" /> <br/>


 
 
 <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/e589b824-8196-48ae-8407-83ef6d2b40ea" />

 On the right-hand side, all parameters are constants obtained from the model file except Vm. Once Vm is specified, the required W/L ratios can be calculated.

This helps determine how much larger the PMOS W/L must be compared to NMOS for a given Vm. Next, we analyze CMOS behavior for different PMOS and NMOS sizing ratios.



 <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/63a35216-3554-46dd-aa40-7aa21ec6c366" />


 ## 33. Lecture-4  Static and dynamic simulation of CMOS inverter

 `Vin in 0 0 pulse 0 2.5 0 10p 10p 1n 2n`

This pulse source is applied as the input to the CMOS inverter to perform transient analysis and observe the dynamic switching behavior.

 `Vin in 0 0 pulse 0 2.5 0 10p 10p 1n 2n`


 <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/27e0a0a1-e22f-45cb-9cda-d99601e57e84" /> <br/>


  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/619b7422-5115-4198-89ab-e0980ae04cec" /> <br/>

 To calculate the rise delay, the measurement is taken at the 50% level of the output waveform (i.e., at half of VDD). The rise delay is the time difference between the input and output signals when both cross this 50% voltage level during the rising transition.
  

  


  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/6a879d94-13b6-47a4-982c-a072c8731c41" />

  From the waveform markers shown, the two time points at the 50% level are approximately 1.01446 ns and 1.16477 ns.

The rise delay is calculated as the difference between these values:

Rise delay ≈ 1.16477 ns − 1.01446 ns ≈ 0.150 ns.



  <img width="522" height="407" alt="image" src="https://github.com/user-attachments/assets/767d4d02-a588-4cfb-9944-bb60a819d519" />


  To calculate the fall delay, observe the waveform at the 50% voltage level (half of VDD) during the falling transition. The fall delay is the time difference between when the input and output signals cross this 50% level while the output is transitioning from high to low.


  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/8226cebe-95bc-46cb-a1ff-e7007952afab" />


From the waveform markers, the two time points at the 50% level are approximately 2.00486 ns and 2.07653 ns.

The fall delay is calculated by taking the difference:

Fall delay ≈ 2.07653 ns − 2.00486 ns ≈ 0.072 ns.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/b16c75c7-a931-491c-a0cf-5564252165d5" /> <br/>


<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/af4a156c-a3d6-432e-bcae-cb5bbe0a10d0" /> <br/>



 ## 34. Lecture-5  Static and dynamic simulation of CMOS inverter with increased PMOS width


 SPICE simulations will be performed with a larger PMOS width, and the results will be compared with the previous configuration.


 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/3fa92bda-d3ff-4138-b47f-6a3b8d397544" /> <br/>


 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/861478e1-5cdd-40fd-860a-49989451ded7" /> <br/>

 <img width="700" height="500 " alt="image" src="https://github.com/user-attachments/assets/b766c969-eab1-469c-bf65-40d843a04890" />  <br/>

 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/5b8e1563-da7f-4a51-aa98-c6b333e5eeed" />  <br/>

 this is observed that as , The rise delay decreases as the PMOS width (Wp/Lp) increases. This is because a wider PMOS provides stronger pull-up capability, reducing the time required to charge the output capacitor.

With a larger device area, more current is available to charge the load capacitance, resulting in a significantly faster rising transition.

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/d747d237-b39b-412b-b954-5a516a304127" />


 ## 35. Lecture-6  Applications of CMOS inverter in clock network and STA

 During fabrication, small variations in the dimensions of PMOS and NMOS devices may occur. However, the CMOS inverter is robust enough that these size variations do not cause significant changes in the switching threshold (Vm).

When (W/L)p is approximately twice (W/L)n, the rise and fall delays become nearly equal. By simulation, the exact sizing ratio can be determined to balance both delays, demonstrating the symmetrical behavior of the CMOS inverter.



 <img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/2e34683d-9b6c-4590-a968-b78d9fafe612" />

 The H-Tree clock network distributes the clock evenly across the chip to minimize skew, using buffers to drive large loads. Since Rₒₙ(PMOS) is about 2–2.5× higher than Rₒₙ(NMOS), proper sizing is needed to balance pull-up and pull-down strengths.

In clock buffers, rise and fall delays are designed to be equal to maintain symmetric transitions and avoid duty cycle distortion.
  



 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/c8f52ba2-5c45-4410-a799-12172e82cda1" />  <br/>

 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/15806bfd-97c9-41c7-bab8-4b0100962717" />  <br/>

 ## Day 4  CMOS Noise Margin Robustness Evaluation

 ## Static behaviour evaluation-CMOS inverter robustness-Noise Margin


 ## 36. Lecture-1   Introduction to noise margin

 Now we study the robustness of a CMOS inverter in terms of Noise Margin and how it is evaluated from its input–output characteristics.

Noise Margin is the measure of how much unwanted electrical noise a logic circuit can tolerate at its input without causing an incorrect output. It indicates the reliability of the inverter in the presence of disturbances.

In an ideal inverter, when the input is 0 the output is 1, and when the input is 1 the output is 0, with an infinite switching slope (instant transition). However, in a practical CMOS inverter, the transition is gradual, resulting in a finite slope. By observing the ideal and actual input–output characteristics (VTC), we can determine the noise margins and evaluate how robust the inverter is against noise.


  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/5b507d88-2c9a-4db3-a039-0b4af195a429" />

  In practical CMOS inverters, the switching slope is not infinite because parasitic resistances and capacitances introduce delay in the transition. As a result, the output changes gradually, leading to a finite slope in the VTC instead of an ideal abrupt transition.



  <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/395824cd-6f42-41c9-9768-6f530023a152" />  <br/>

  Now we observe that when the input voltage lies between 0 and (Vil) (maximum input low voltage), the output remains at (Voh) (output high voltage).

Similarly, when the input voltage is between (V_{IH}) (minimum input high voltage) and (Vdd), the output stays at (Vol) (output low voltage).


  <img width="500" height="100" alt="image" src="https://github.com/user-attachments/assets/68f06d06-51a1-4fa1-811d-ff86b07116c1" />  <br/>


  <img width="300" height="300 " alt="image" src="https://github.com/user-attachments/assets/1808084e-63b4-47fe-83aa-680cabc8801c" />  <br/>


   <img width="500" height="100" alt="image" src="https://github.com/user-attachments/assets/c16f45d1-ee77-45f8-9ec6-f7b756d22eb2" />  <br/>


   <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/ab33ed17-dc95-418b-873b-7e29779d95f9" />  <br/>


 ## 37. Lecture-2  Noise margin voltage parameters

 - In practical CMOS inverters, due to non-idealities, the VTC curve is gradual instead of ideal.

 - <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/eccefd39-025e-458f-8b92-f4c7c536008e" />


- When (0 < Vin < Vil), the output is in the high region: (Voh < Vout < Vdd).

- When the input is high (close to (Vdd)), the output is in the low region: (0 < Vout < Vol).

- The voltage levels satisfy: (Vol < Voh < Vdd) and (0 < Vol < Vil), ensuring proper operation of the next inverter stage.

- The slope in the transition region is approximately −1, meaning as input increases, output decreases.

- <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/bd66869c-6adc-4e2c-aaa2-13f2b6688587" />

 ## 38. Lecture-3 Noise margin equation and summary

 to derive the noise margin equations, we will plot the relevant voltage levels on the same scale for proper comparison and analysis.

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/21c8afac-ce62-4ab2-9488-d8d8366fb5ff" /> <br/>

 On the above scale:

- Noise Margin High (NH) – the voltage difference between (Vih) and (Voh).
- Noise Margin Low (NL) – the voltage difference between (Vil) and (Vol).

Any input voltage within these noise margins is interpreted correctly as logic 1 or 0 and is tolerable. Voltages outside this range fall in the undefined region, where the logic level can fluctuate between high and low.


 <img width="100" height="100" alt="image" src="https://github.com/user-attachments/assets/0cf6070f-2a53-4f4b-a722-3ecf06450bb3" /> <br/>

 <img width="580" height="336" alt="image" src="https://github.com/user-attachments/assets/b0be92fe-2287-4f07-9d6e-1857cc02a74f" /> <br/>


  ## 39. Lecture-4  Noise margin variation with respect to PMOS width

  We will evaluate the noise margin based on the PMOS width to demonstrate the robustness of a CMOS inverter.

First, we identify the points where the slope equals −1 and extend the tangent lines toward the x and y axes.




  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/4b870f60-e6b5-4aa5-a32c-3c435219f22a" /> <br/>


  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/0d639c84-df54-4b33-bf26-b9615a7026ad" /> <br/>

  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/1f6c2052-9d7d-4d7c-b2a7-98f17040e7cc" /> <br/>


  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/259db2c0-cd7a-48db-a832-07fd8688a2d8" /> <br/>


  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/83bbd90b-e1c0-45b6-a112-5c09c264e718" /> <br/>


- Increasing PMOS width raises the high noise margin (NH).
- Low noise margin (NL) remains fairly stable.
- Wider PMOS improves overall noise tolerance and robustness of the inverter.


  <img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/1ef67e6b-31b8-43b6-9219-50b5c841b925" />

  We can also identify the voltage ranges that define the "digital" and "analog" regions of the CMOS inverter.



<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/af6721f8-1bf6-4d04-a9ea-2edd8737cab5" /> <br/>


<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/b4b56812-7bf0-42ad-aabc-93c1fd2d2179" /> <br/>


 ## 40. Lecture-5  Noise margin variation with respect to PMOS width

 ploting Noise margins



 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/2a4a2698-aa08-426a-a219-89e91cbcdb5b" />

 We set the PMOS-to-NMOS W/L ratio to 2.77 and sweep (Vin) from 0 to 1.8 V in steps of 0.01 V.

 

  <img width="355" height="72" alt="image" src="https://github.com/user-attachments/assets/511dbca6-ebfb-4a15-8328-8aa3da0b15b3" />

  We consider the point where the slope equals −1. At this point, the x-axis values give (V_{IL}) and (V_{IH}), while the y-axis values give (V_{OH}) and (V_{OL}).

The noise margins are calculated as:

- (NH = Voh - Vih = 1.70952 - 0.98778 = 0.72) V
- (NL = Vil - Vol = 0.7733 - 0.09523 = 0.67807) V


 ## 41. Lecture-1  Smart SPICE simulation for power supply variations


 Another factor in evaluating the robustness of a CMOS inverter is **power supply scaling**. Reducing the gate length lowers the operating power, but the CMOS characteristics should remain largely unchanged under power scaling.

 
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/010c8cc4-1936-4b41-913e-f759cbf7d684" />

 MODEL Descriptions

v1 2.5 supply voltage
M1 in in vdd vdd pmos W=0.9375u L=0.25u
M2 out in 0 0 nmos W=0.375u L=0.25u

We will now plot the Voltage Transfer Characteristics (VTC) for the following supply voltages: VDD = 2.5V, 2V, 1.5V, 1V, and 0.5V.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/27e77f60-46d0-4b2e-9dfa-7b4db5cd6c8b" />

 ## 42. Lecture-2  Advantages and disadvantages using low supply voltage
 
- We will analyze the curves obtained from the simulation to understand the advantages and disadvantages of using a low supply voltage.

- The first parameter to evaluate is the gain at each supply voltage.

- The gain factor is defined as the ratio of the change in output voltage to the change in input voltage (ΔVout / ΔVin).


 <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/0be7a850-c72a-471f-8b2d-7de59ac9f97d" /> <br/>

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/ebb3d2a9-312d-4eb6-99d6-bc725249ac85" /> <br/>

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/af162822-d145-460b-a18f-26cf8715def2" /> <br/>

 gain at lower supply voltage


 <img width="600" height="200" alt="image" src="https://github.com/user-attachments/assets/432a599f-1ca0-4d01-9560-4b2aaad60233" /> <br/>


 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/21e8e4f8-e198-45cd-b965-2782474d5bf1" /> <br/>

 Energy at lower supply voltage (0.5v)

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/42bbe79b-13d3-4eb4-b19c-25b1d0c97559" /> <br/>

 <img width="600" height="200" alt="image" src="https://github.com/user-attachments/assets/f4b51e15-1eba-4065-8e92-7f17db312ac2" /> <br/>

 If we see the rise delay and fall delay

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/a3a02e31-549d-4dec-8c9d-5f5b753c7478" /> <br/>

 At the lower supply voltage(0.5v) , rise time not sufficient to charge output load capacitor 

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/17cd8024-e3d2-4a24-9578-0ae26e028bee" />

 Now we will see rise delay and fall delay at higher supply voltage(1v)

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/d3c65e24-f2d6-4ce7-acd3-22a7683aaff9" /> <br/>

 <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/4166852a-797a-4491-850a-bab694d6ee09" /> <br/>

 <img width="600" height="200" alt="image" src="https://github.com/user-attachments/assets/0a75ab71-90de-41ce-8735-f0ced9dd1853" />  <br/>
 
 ## 43. Lecture-3  Sky130 Supply Variation Labs

  now calculating the supply variation.

  The initial supply voltage is 1.8V, and it is reduced in steps of 0.2V, resulting in    a        total of 6 iterations.

  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/b6d848fb-9649-4f6d-885d-d4931dd9545f" />

  We will calculate the gain by selecting two points from the steep transition region of the VTC curve and using:

[
Gain = \frac{\Delta V_{out}}{\Delta V_{in}} = \frac{y_1 - y_0}{x_1 - x_0}
]

---

For VDD = 1.8V

Selected coordinates from the graph:

Point 1:
[
(x_0, y_0) = (1.05,V, 1.72,V)
]

Point 2:
[
(x_1, y_1) = (1.23,V, 0.35,V)
]

Calculation:

[
\Delta V_{out} = 0.35 - 1.72 = -1.37,V
]

[
\Delta V_{in} = 1.23 - 1.05 = 0.18,V
]

[
Gain = \frac{-1.37}{0.18} = -7.6229
]

[
|Gain| = 7.6229
]

---

For VDD = 0.8V

Selected coordinates from the graph:

Point 1:
[
(x_0, y_0) = (0.46,V, 0.78,V)
]

Point 2:
[
(x_1, y_1) = (0.55,V, 0.00,V)
]

Calculation:

[
\Delta V_{out} = 0.00 - 0.78 = -0.78,V
]

[
\Delta V_{in} = 0.55 - 0.46 = 0.0831,V
]

[
Gain = \frac{-0.78}{0.0831} = -9.3844
]


|Gain| = 9.3844



## Static behaviour evaluation-CMOS inverter robustness-Device variation

## 44. Lecture-1  Sources of variation – Etching process

We will study the sources of variation in the VTC characteristics of a CMOS inverter.

There are two main sources of device variation:

- Etching process variation
- Oxide thickness variation

The etching process is a very important fabrication step because it defines the physical structure of the CMOS inverter. It determines the gate length and width (the common area between polysilicon and diffusion). Any variation during etching can change these dimensions, which directly affects current, delay, and the VTC characteristics.

In the CMOS inverter layout:

- P-diffusion region is shown in green.
- Polysilicon (gate) is shown in red.
- Metal layer is shown in blue.
- N-diffusion region is shown in yellow.
- Contacts between layers are indicated by black crosses.

Variations in these regions due to fabrication processes impact the overall inverter performance.


<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/a1ec5ce6-0644-4988-b40f-3cdc06c815a7" />

When considering an inverter chain, the variations may differ from one inverter to another.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/bd6c912c-4902-4679-86dc-f75af1e71401" />  <br/>

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/c1919bd5-106f-4d3a-80cf-13f3bee01e0d" />  <br/>

The variation is greater at the edges or sides compared to the center.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/77c31f9e-3305-48fe-a86c-b4526fdacffe" />

Therefore the variation in L and W can change the drain current of CMOS inverter.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/f4da52bb-b7f6-446f-b2a8-e91031e71586" />











 






 


 


 



 




 


 









 










  







 



  


  



  



  








   







 






 


 








 








 



 



 

 
 





 























 




























  







 












 
























 




  




















  






    

 






 





 

 


  


 




 



 


  


 

 



  



 



 

















 

 



 






















 







 





 






  




  























 


 
























  


   


















 


  





 



 


   

 



   




  


  



  


    


  


 

 











 


  

  

  


  

  


 

   

 





   




 

 

 



 

 




 

 

 



  



 










   



 



 




   


   

   


   


   

   





   




	



	




      
    






	 

	 


      



	 


	 

	
	


     

	

    

    

    

  


    

    


     






	​

​

     



   

   




 

                                                                                                                                                                    







   
  
  
  




 
 

 


    


    

 

 
 
 

 

 


  




  

