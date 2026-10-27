# APB Protocol Controller in Verilog

![Verilog](https://img.shields.io/badge/HDL-Verilog-blue)
![Protocol](https://img.shields.io/badge/Protocol-APB-orange)
![FSM](https://img.shields.io/badge/Controller-3--State%20FSM-success)

A concise RTL implementation of an **AMBA APB (Advanced Peripheral Bus) protocol controller** written in Verilog HDL. The design models the standard three-phase APB transaction flow and includes simulation artifacts for functional verification and synthesis inspection.

## Overview

The APB controller manages peripheral transactions using a synchronous three-state finite-state machine:

```text
IDLE → SETUP → ACCESS
```

APB is designed for simple, low-bandwidth peripheral communication in systems-on-chip. This project demonstrates the controller-side signaling required to initiate and complete an APB transfer.

## FSM Operation

| State | `psel` | `penable` | Description |
| --- | ---: | ---: | --- |
| **IDLE** | `0` | `0` | No transfer is active. |
| **SETUP** | `1` | `0` | A transfer is selected and its control information is presented. |
| **ACCESS** | `1` | `1` | The transfer is active and completes when the slave asserts `pready`. |

## Interface Signals

| Signal | Direction | Description |
| --- | --- | --- |
| `clk` | Input | System clock. |
| `reset` | Input | Asynchronous reset. |
| `trans_req` | Input | Requests a new APB transaction. |
| `pready` | Input | Indicates that the APB slave is ready to complete the transfer. |
| `psel` | Output | Selects the APB peripheral. |
| `penable` | Output | Enables the access phase of the APB transfer. |

## Repository Contents

| File | Description |
| --- | --- |
| [`rtl code`](./rtl%20code) | Verilog RTL implementation of the APB controller. |
| [`testbench`](./testbench) | Testbench used to exercise the controller behavior. |
| [`apb waveform.png`](./apb%20waveform.png) | Simulation waveform showing the APB state and control signals. |
| [`apb rtl.png`](./apb%20rtl.png) | RTL schematic / synthesized design view. |
| [`667e76a2-87f3-47d0-b06f-ed3bb2eadbdb.jpg`](./667e76a2-87f3-47d0-b06f-ed3bb2eadbdb.jpg) | Additional project image. |

## Verification and Synthesis

The design has been:

- Simulated using the included testbench.
- Checked through the APB state transition sequence.
- Synthesized to inspect the resulting RTL structure and netlist representation.

## Tools Used

- **Verilog HDL** — RTL design and verification
- **EDA Playground** — Simulation environment
- **Yosys** — Synthesis and RTL inspection

## APB Transaction Flow

A typical transaction proceeds as follows:

1. `trans_req` is asserted while the controller is in `IDLE`.
2. The controller enters `SETUP` and asserts `psel`.
3. The controller enters `ACCESS` and asserts `penable`.
4. The transfer remains active until `pready` is asserted.
5. The controller returns to `IDLE` after the transfer completes.

## Learning Objectives

This project is useful for understanding:

- APB protocol timing and control signaling
- Finite-state-machine design in Verilog
- RTL simulation and waveform analysis
- Basic synthesis and hardware design verification

## License

No license has been specified for this repository yet. Add a license if you plan to distribute or reuse the design.
