# Unintended Reset in VHDL Counter

This repository demonstrates a common, yet subtle bug in VHDL code: an unintended reset condition within a counter implemented using a process and a rising_edge clock sensitive statement.  The original code (`buggy_counter.vhd`) incorrectly handles the state transition at the maximum count.  The corrected code (`fixed_counter.vhd`) demonstrates the proper solution.

## Bug Description

The `buggy_counter` VHDL code implements a simple 4-bit counter. However, the logic within the process's `rising_edge(clk)` section is flawed. If the `internal_count` reaches 15, the `if` statement resets the counter to 0, this is correct. But if any other condition occurs within the process, due to the lack of `else` statement, the counter will also reset unexpectedly. This leads to an incorrect counting behavior.

## Solution

The `fixed_counter` VHDL code addresses the issue by adding an `else` statement to the `if` condition within the `rising_edge(clk)` section. This ensures that the counter increments normally when the counter does not equal to 15, preventing unintended resets and ensuring a correct counting sequence.

## How to Reproduce

1. Simulate both VHDL files (`buggy_counter.vhd` and `fixed_counter.vhd`) using your preferred VHDL simulator (e.g., ModelSim, GHDL).
2. Observe the output signals of both counters under different clock cycles and reset conditions. The buggy counter will exhibit unexpected resets that are not present in the corrected counter.