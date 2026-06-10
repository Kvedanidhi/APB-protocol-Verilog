APB Protocol Controller — Verilog HDL
What is APB?
APB (Advanced Peripheral Bus) is part of ARM's AMBA bus architecture, widely used in SoC designs for connecting low-bandwidth peripherals. It defines a simple handshake mechanism between a bus master and peripheral slave.
What I Built
A Verilog RTL implementation of an APB controller with a 3-state Finite State Machine — verified through simulation and synthesised to gate-level netlist.
FSM Architecture
IDLE → SETUP → ACCESS

IDLE — psel=0, penable=0
SETUP — psel=1, penable=0 (transaction requested)
ACCESS — psel=1, penable=1 (data transfer in progress)

Signals
SignalDirectionDescriptionclkInputClockresetInputAsync resettrans_reqInputTransaction requestpreadyInputSlave ready signalpselOutputPeripheral selectpenableOutputEnable signal
Files

apb_controller.v — RTL design
apb_tb.v — Testbench
waveform.png — Simulation output
rtl_schematic.png — Synthesised netlist

Tools Used

Verilog HDL
EDA Playground
Yosys (synthesis)
