# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

 <img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/b5f95c0d-1fd6-4c3c-9a35-11eb9c86cba3" />

#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
```
module alu_32bit_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;	//AND Operation
3'b001:y=a|b;	//OR Operation
3'b010:y=~(a&b);//NAND Operation
3'b011:y=~(a|b);//NOR Operation
3'b100:y=a+b;	//Addition
3'b101:y=a-b;	//Subtraction
3'b110:y=a*b;   //Multiply
3'b111:y=a^b;	// XOR Operation
default:y=32'bx;
endcase 
end 
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_32bit_tb_case; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_32bit_case DUT(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00100001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#150 $finish; 
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using ifelseif Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;	               //AND Operation 
else if (f==3'b001)
y=a|b;	              //OR Operation
else if (f==3'b010)
y=~(a&b);	      //NAND Operation
else if (f==3'b011)
y=~(a|b);	      //NOR Operation
else if (f==3'b100)
y=~(a^b);	      //XOR Operation
 else if (f==3'b101)
y=a+b;                //Addition
 else if (f==3'b110)
y=a-b;	              //Subtraction 
else if (f==3'b111)
y=a*b;	              //Multiply 
else
y=32'bx; 
end 
endmodule
```
#### Test Bench :
```
module alu_ifelseif_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; b=32'h00100001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#100 $finish; 
endmodule
```
Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below
<img width="1919" height="1075" alt="Screenshot 2025-10-14 102448" src="https://github.com/user-attachments/assets/1a720d3e-7a7b-4a43-8d2c-ffe97a016909" />
<img width="1890" height="1053" alt="Screenshot 2025-10-14 104939" src="https://github.com/user-attachments/assets/68439d26-304f-437e-a5cb-a5b5bee0a45d" />



#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.


Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
<img width="1918" height="1077" alt="Screenshot 2025-10-14 102520" src="https://github.com/user-attachments/assets/81f3706a-c2ee-4aee-80de-a77e2e7f6696" />
<img width="1919" height="1077" alt="Screenshot 2025-10-14 105007" src="https://github.com/user-attachments/assets/2fcd1aac-a8ec-48c1-bfc9-4f6637d926fb" />





#### Fig 3: Nclaunch Window

#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation
<img width="1918" height="1076" alt="Screenshot 2025-10-14 102457" src="https://github.com/user-attachments/assets/d3fce806-1021-4adc-86bf-40ae1989e540" />
<img width="1918" height="1058" alt="Screenshot 2025-10-14 104945" src="https://github.com/user-attachments/assets/60ca9e0e-6062-486c-83c3-ab51adfed63e" />






#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.
<img width="1919" height="1079" alt="Screenshot 2025-10-14 102658" src="https://github.com/user-attachments/assets/be36feca-6e7b-4f0e-9a14-e49cb22627ce" />
<img width="1919" height="1074" alt="Screenshot 2025-10-14 105109" src="https://github.com/user-attachments/assets/02a55324-64c2-4eb6-8969-723170d0f9af" />


#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options\


#### Fig 6: Design Browser window for simulation
<img width="1919" height="1077" alt="Screenshot 2025-10-14 102857" src="https://github.com/user-attachments/assets/59e6a658-2db8-4ad2-a220-41e83daecea3" />
<img width="1917" height="1076" alt="Screenshot 2025-10-14 105327" src="https://github.com/user-attachments/assets/0109a728-4d76-4729-9087-c0d44b455320" />


#### Fig 7: Simulation Waveform Window
Synthesis requires three files as follows,

◦ Liberty Files (.lib)
◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
#### For case statement
<img width="1919" height="1079" alt="Screenshot 2025-10-14 105427" src="https://github.com/user-attachments/assets/52a5cf35-ef08-4db7-99a5-52a94ade68f9" />

#### For ifelseif statement
<img width="1919" height="1079" alt="Screenshot 2025-10-14 103514" src="https://github.com/user-attachments/assets/ad3d609a-85ba-4d38-89c6-ea7b63f9e39a" />

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
<img width="1919" height="1076" alt="Screenshot 2025-10-14 103814" src="https://github.com/user-attachments/assets/5a051c53-1a0e-4113-ba9b-96dc79e6f4e7" />
<img width="1919" height="1079" alt="Screenshot 2025-10-14 105809" src="https://github.com/user-attachments/assets/f5e32106-c218-472c-8477-337b81c5df23" />



#### Fig 9: Area report of case and ifelseif construct
<img width="1461" height="609" alt="Screenshot 2025-10-14 103853" src="https://github.com/user-attachments/assets/bdfdd6bf-e5b3-4f56-97a5-ad3d12e4827a" />
<img width="1571" height="569" alt="Screenshot 2025-10-14 105842" src="https://github.com/user-attachments/assets/8474b4ba-2581-435a-8f10-eb3da0bc4ec8" />


#### Fig 10: Power Report of case and ifelseif construct
<img width="1560" height="699" alt="Screenshot 2025-10-14 103909" src="https://github.com/user-attachments/assets/dee1d245-5b60-4032-a9ce-5dfe2e363bdc" />
<img width="1442" height="565" alt="Screenshot 2025-10-14 105858" src="https://github.com/user-attachments/assets/48737155-fa03-4974-a998-38c0a01fc3d6" />


#### Fig 11: Timing Report of case and ifelseif construct
<img width="1554" height="809" alt="Screenshot 2025-10-14 104023" src="https://github.com/user-attachments/assets/7a8994e1-b9ce-4d39-97c0-92a90918307b" />
<img width="1531" height="535" alt="Screenshot 2025-10-14 105921" src="https://github.com/user-attachments/assets/4daecfe5-6fb6-488f-bbb8-7986538845c5" />


#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct
<img width="1317" height="631" alt="image" src="https://github.com/user-attachments/assets/c9a529bc-b3e4-4737-8729-d5aad84707d5" />

## Result
The 32-bit ALU was successfully implemented using both case and if-elseif constructs. From synthesis, the if-elseif ALU showed lower area (9913.876 µm²) and fewer cells (1242) than the case ALU. Power analysis also showed slightly lower power for the if-elseif design. Both designs passed functional simulation and produced correct outputs. Thus, the if-elseif ALU performed better in area and power in our experiment.
