SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado 2023.1.

APPARATUS REQUIRED: vivado 2023.1.

LOGIC DIAGRAM

SR FLIPFLOP

image

JK FLIPFLOP

image

T FLIPFLOP

image

D FLIPFLOP

image

COUNTER

image

PROCEDURE:

Open Vivado: Launch Xilinx Vivado software on your computer.

Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design. VERILOG CODE Dflipflop

module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
OUTPUT

image

image JKflipflop

module JK_flipflop (q, q_bar, j,k, clk, reset);  
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  // always@(posedge clk or negedge reset) // for asynchronous reset
  always@(posedge clk) begin // for synchronous reset
    if(!reset)
           q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
OUTPUT

image

image Mod10Counter

module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
OUTPUT

image

image Ripplecarrycounter

module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
OUTPUT

image

image SRflipflop

module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
output

image

image T flipflop

module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
OUTPUT

image

image Updowncounter

module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
output

image

image

RESULT Simulate And Synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN is Successfully Verified using Vivado Software.
