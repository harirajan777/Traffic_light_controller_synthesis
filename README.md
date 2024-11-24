# Traffic_light_controller_Synthesis

## Aim:

Synthesize Traffic Light Controller design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### Step 2 : Creating Source Code
Verilog code: 

'timescale 1 ns / 1 ps

module TrafficLight(input elk, //LED_NS represent the North-South LEDs

input rst, //LED_WE represent the West-East LEDs          

output reg [2:0] LED_NS, LED_WE);

/*Let 100 = Red

010 = Yellow                         

001 = Green

We have 6 different states, defining them below*/

parameter SO = 6'b000001, //When NS is green and EW is red 

S1 = 6'b000010, //When NS is yellow and EW is red

S2 = 6'b000100, //When NS is red and EW is red

S3 = 6'b001000, //When NS is red and EW is green

S4 = 6'b010000, //When NS is red and EW is yellow 

SS = 6'b100000; //When NS is red and EW is red

//Then the cycle repeats 

reg [5:0] state;

reg [3:0] count;

//Defining transition of states 

always@(posedge elk or posedge rst)

begin

if(rst) begin //Active HIGH reset 

state < = SO;

count < = O;

end 

else

begin 

case(state)

SO: begin

if(count == 4'd14) 

begin count < = O; 

state < = S1; 

end 

else 

begin

count < = count + 1; state < = SO; end end 
S1: begin

if(count == 4'd2) begin count < = O; 

state < = S2; end 

else begin

count<= count+ 1; state<= S1; end end

S2: begin

if(count == 4'd2) begin count < = O; 

state < = S3; end 

else begin

count < = count + 1; state < = S2; end end 

S3: begin

if(count == 4'd14) begin count < = O; 

state < = S4; end

else begin

count < = count + 1; state < = S3; end end 

S4: begin

if(count == 4'd2) begin count < = 0; 

state < = S5; end 

else begin

count < = count + 1; state < = S4; end end

S5: begin

if(count == 4'd2) begin count < = 0; 

state < = SO; end 

else begin

count < = count + 1; 

state < = S5; end end 

end case

end 

end

/* 100 = Red

010 = Yellow                         

001 = Green  */

//Output of LEDs// 

always@(*)

begin case(state)

SO: begin LED_NS = 3'b001; LED_WE = 3'b100; end

S1: begin LED_NS = 3'b010; LED_WE = 3'b100; end 

S2: begin LED_NS = 3'b100; LED_WE = 3'b100; end 

S3: begin LED_NS = 3'b100; LED_WE = 3'b001; end 

S4: begin LED_NS = 3'b100; LED_WE = 3'b010; end 

S5: begin LED_NS = 3'b100; LED_WE = 3'b100; end 

endcase

end

endmodule

### Step 3 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

### Step 4 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

Synthesis RTL Schematic :
![Screenshot 2024-11-23 163947](https://github.com/user-attachments/assets/286400d9-dd38-42ba-bba7-d75674fe02f1)

Area report:
![Screenshot 2024-11-23 164014](https://github.com/user-attachments/assets/02af0fe4-cfc2-4a14-a519-a1a76c215bf0)

Power Report:
![Screenshot 2024-11-23 164023](https://github.com/user-attachments/assets/07773af9-8f9a-4461-894d-2b55fc3d6dc4)

Result:

The generic netlist of Traffic Light Controller has been created, and area, power reports have been tabulated and generated using Genus.
