# CMOS-Circuit-Design

## Lecture - 1  

Circuit design involves arranging transistors  and resistors to create logic gates (AND, OR, NOT, NAND, NOR, XOR), which are then combined in a particular fashion to form complex, functional digital circuits like microprocessors. <br/>
Example : 
- CMOS Inverter circuit made of using  <br/>
          - One PMOS transistor  <br/>
          - One NMOS transistor <br/>

<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/f12d74f1-962a-4077-b284-4f136eeab583" />


### SPICE Simulation 
 Use to test and analyze electronic circuits on a computer before building them physically.

  NMOS and PMOS transistor Characteristics curve :
  
  <img width="500" height="300" alt="Screenshot 2026-02-17 110459" src="https://github.com/user-attachments/assets/aa3f370e-8b04-4df1-9ae1-b71e41a74247" />  <br/>
  
  

 SPICE gives a delay curve for NMOS/PMOS.This curve shows how delay changes with W/L :

 <img width="500" height="200" alt="Screenshot 2026-02-17 111235" src="https://github.com/user-attachments/assets/27dd897c-17fd-4dc6-b0e5-304be216a6db" />

 #### Why we need SPICE simulation ?
 Let's take an example of buffer circuit :<br/>
 
 <img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/580ff9b8-ec9c-4ba9-8cda-0b43158ef715" />

 1. Where does the delay table of a cell actually come from? <br/>
    SPICE is the Source of cell delay,it simulates real device physics to give the true transistor-level delay.
    

 2. We learned delay models, but are the models accurate?<br/>
    Delay models are approximate SPICE gives accurate results to build delay tables.

 3. How do you verify STA results are correct?<br/>
    To check STA correctness, we compare STA delay with SPICE delay.

 

 
 
 

 

 


  




  

