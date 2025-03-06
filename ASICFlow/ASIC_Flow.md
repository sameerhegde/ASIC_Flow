# **ASIC Design Flow**

## **1. Specification**
- Gather system and functional requirements.
- Define performance, power, and area constraints.
- Document design specifications.

## **2. Microarchitecture**
- Develop block-level architecture based on specifications.
- Define data paths, control logic, and interfaces.
- Identify pipeline stages, memory hierarchy, and clock domains.

## **3. RTL Design & Integration**
- Implement design using **Verilog/VHDL**.
- Ensure modular and synthesizable coding.
- Integrate different IPs and modules into a top-level design.

## **4. Verification**
- Develop testbenches using **UVM/SystemVerilog**.
- Perform **simulation-based functional verification**.
- Check for corner cases and coverage metrics.

## **5. Design for Testability (DFT)**
- Insert **scan chains** for testability.
- Implement **BIST (Built-In Self-Test)**.
- Ensure high **fault coverage** for manufacturing testing.

## **6. Lint (Static Code Check)**

### **Introduction**
- **Linting** is a **static code analysis** technique used to check RTL (Verilog/VHDL) for errors before synthesis.
- It detects **syntax, semantic, and design rule violations** to ensure clean and synthesizable RTL.
- Linting improves **code quality, maintainability, portability, and verification efficiency**.

### **Rules in Lint**
- **Array Rules**
  - Out of index
  - All elements of array are not read
  - All elements of array are not set

- **Case Rules** 
  - Missing default 
  - Not all cases are specified
  - **Leads to latch inference**

- **Lint Reset Rules** 
  - Both edges are used within the same design unit
  - Synchronous and asynchronous reset conflict 

- **Lint Clock Rules** 
  - Reports if both edges of clock are used in the same module

- **Usage Rules**
  - All elements of memory are not used
  - Unused variables 
  - Macros/parameters defined but not used
  - **Output is never set**

- **Assign Rules** 
  - **Truncation of extra bits**
  - Blocking should not be used in sequential blocks
  - Non-blocking assignment in combinational block

- **Function Task Rules** 
  - Function/Task declared but not used
  - Recursion is not used 
  - Task which contains event control is not synthesizable

- **Instance Rules**
  - Port width mismatch
  - Mixing of By-name and By-order is not allowed 
  - Inputs are not driven or not connected

- **Synthesis Rules**
  - `Wait` and `Time` declaration
  - Real variables are not synthesizable
  - Case equality and inequality (`===`, `!==`) are not synthesizable
  - `Initial` is not synthesizable
  - `while/repeat/for` without proper conditions are not synthesizable

- **Expression Rules** 
  - `X`, `Z`, and `?` (don't care) may lead to synthesis and simulation mismatch

- **Multiple Drivers**
  - Signal has multiple drivers 
  - Different bits of the same bus are driven by multiple blocks

- **Event Rules**
  - Mixing combinational and sequential styles in a block

- **Combinational Loops** 
  - Signal is read inside a combinational block but not mentioned in the sensitivity list
  - Signal is included in the sensitivity list but no elements are used
  
### **Lint using Spyglass**
```c
	#include <stdio.h>
	void main(){
		printf("Hello, World");
	}
```
## **7. Clock Domain Crossing (CDC) Analysis**
- Identify signals crossing different clock domains.
- Ensure proper synchronization using **FIFO, handshaking, or synchronizers**.
- Use **CDC tools** like SpyGlass or Conformal.

## **8. Low Power Analysis**
- Apply **power optimization techniques** (clock gating, power gating, multi-Vt).
- Check **UPF (Unified Power Format)/CPF (Common Power Format)** consistency.
- Analyze **dynamic and static power consumption**.

## **9. Synthesis**
- Convert RTL code to **gate-level netlist** using tools like **Design Compiler or Genus**.
- Apply area, power, and timing optimizations.
- Generate **timing reports and constraints (SDC files)**.

## **10. Static Timing Analysis (STA)**
- Perform **timing verification** using tools like **PrimeTime**.
- Identify and fix **setup, hold, and clock skew violations**.
- Ensure **multi-corner and multi-mode timing closure**.
