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
- Linting improves **code quality, maintainability,Poratability and verification efficiency**.

### **Rules in Lint**
- Array Rules
	- out of index
	- all elements of array are not read
	- all elements of array are not set
- Case rules 
	- missing default 
	- not all cases are specified
	- **leads to latch inference**
- Lint Reset rules 
	- both edges are used within same design unit
	- Synchronous and Asynchronous reset conflict 
- Lint clock rules 
	- reports if both edges of clock are used in same module
- Usage rules
	- All elements of memory are not used
	- Unused variables 
	- Macros/parameter defined but not used
	- **Output is never set**
- Assign rules 
	- **Truncation of extra bits**
	- Blocking should not be used in sequential blocks
	- Non blocking assignment in combinational block
- Function Task rules 
	- Function Task decleared but not used
	- Recurssion is not used 
	- task which contains event controlled are not synthesizable
- Instance Rules
	- port width mismatch
	- Mixing of By name and By order is not allowed 
	- Inputs are not driven or not connected
	- Synthesis Rules
	- Wait and Time declearation
	- Real variables are not synthesizable
	- case equality and not equality (===) (!==) are not synthesizable
	- `Inital` is not synthesizable
	- `While/repeat` without proper conditions are not synthesizable
- Expression rules 
	- `X Z and ?` (dont care) may lead to Synthesis and simulation mismatch
- Multiple Drivers
	- Signal has multiple drivers 
	- Diffrent bits of same bus are driven by multiple block
- Event Rules
	- Mixing combinational and sequential style in a block
	
- **combinational Loops** 
- Signal is read inside a combinational block but not mentioned in sensitivity list
- signal in included in sensitivity list but not elements are used

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

