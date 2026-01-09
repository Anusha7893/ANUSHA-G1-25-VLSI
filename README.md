# Vending Machine Controller

<p align="center">
  <img src="https://github.com/user-attachments/assets/18087b8d-5284-49dc-92e1-f39cc681c24d" width="500"/>
</p>
# Vending Machine Controller IP – UVM Verification Project

## 📌 Project Overview
This project implements and verifies a **Vending Machine Controller IP** based on the **SURE ProEd Vending Machine Controller Specification**.  
The IP is designed as a configurable digital controller for vending machines, supporting multiple items, currency handling, inventory tracking, and real-time dispense decisions.  
Functional verification is performed using **SystemVerilog** and **Universal Verification Methodology (UVM 1.2)** following industry-standard practices.

---

## 📄 Specification Reference
The design and verification strictly follow the **SURE ProEd Vending Machine Controller Specification**, which defines:
- Parameterized item support (up to **1024 items**)
- Multiple operating modes
- **APB-based configuration interface**
- Currency handling and dispense rules
- Latency and timing constraints

---
## 🧱 Verification Architecture

<p align="center">
  <img src="https://github.com/user-attachments/assets/edfd8d47-825d-452f-8e61-5da9d6b40f61"
 alt="UVM Verification Architecture" width="900"/>
</p>


## ⚙️ Key Features (As per Specification)
- **System clock:** 100 MHz  
- **Configuration clock (APB):** 50 MHz  
- **Operating Modes:** Reset, Configuration, Operation  
- **Item support:** Parameterized up to 1024 items  
- **Currency denominations:** 5, 10, 15, 20, 50, 100  
- **Active-low asynchronous reset**  
- **Latency:** Output decision within < 10 system clock cycles  
- **Inventory tracking:** Dispensed and available item counts  
- **Out-of-stock handling:** Immediate change return with empty-item indication  

---

## 🧱 High-Level Architecture
The Vending Machine Controller IP consists of the following major blocks:

### Input Control Block
- Handles item selection and currency inputs (asynchronous to system clock)

### Main FSM / Counter / Controller
- Controls mode transitions and vending logic

### Configuration (CFG) Block
- APB-based register and memory configuration

### Output Control Block
- Generates item dispense, quantity, and change outputs

The verification environment mirrors this architecture using modular UVM components.

---

## 🔄 Operating Modes

### Reset Mode
- All registers and memories reset to default values

### Configuration Mode
- Enabled using `cfg_mode`
- Item price, availability, and total item count configured via **APB**
- Dispensed item counters cleared

### Operation Mode
- Normal vending operation
- Supports item selection, quantity selection, currency insertion, dispensing, and change return

---

## 🔌 Interfaces Verified

### General Interface
- `clk` – 100 MHz system clock  
- `rstn` – Active-low reset  
- `cfg_mode` – Mode select  

### Currency Interface
- `currency_valid`  
- `currency_value`  

### Item Selection Interface
- `item_select_valid`  
- `item_select`  
- `no_of_items`  

### Configuration Interface (APB)
- `pclk`, `prstn`  
- `paddr`, `psel`, `pwrite`  
- `pwdata`, `prdata`, `pready`  

### Item Dispense Interface
- `item_dispense_valid`  
- `item_dispense`  
- `no_of_items`  
- `currency_change`  

---

## 🧪 Verification Methodology
- **UVM 1.2–based coverage-driven verification**
- Transaction-level modeling using SystemVerilog
- Constrained-random stimulus generation
- Modular agents for:
  - Configuration (APB)
  - Item selection
  - Currency insertion
- Scoreboard-based checking of expected vs actual DUT behavior
- Verification across normal, corner, and stress scenarios

---

## ✅ Test Case Coverage

### Reset & Mode Tests
- `reset_sanity_test`
- `mode_reset_to_config_test`
- `mode_config_to_operation_test`

### APB Configuration Tests
- `apb_write_readback_test`
- `apb_illegal_address_test`
- `boundary_max_items_test`

### Item Selection & Quantity Tests
- `operation_basic_test`
- `multi_item_select_test`
- `high_load_multiitem_test`

### Currency & Change Handling Tests
- `item_no_currency_test`
- `invalid_currency_test`
- `insufficient_balance_test`
- `change_return_test`

### Corner Case Tests
- `out_of_stock_test`
- `boundary_max_items_test`

Each test is mapped to specific functional and corner-case behaviors defined in the specification.

---

## 🛠 Tools & Technologies
- **SystemVerilog**
- **UVM 1.2**
- **APB Protocol**
- **EDA Playground**
- **VCS / QuestaSim (via EDA Playground)**

---

## 📊 Results
- All specification-defined features verified successfully
- Correct mode transitions and APB register behavior
- Accurate item dispense and change calculation
- Proper handling of out-of-stock and invalid transactions
- Stable operation under constrained-random testing
- Scoreboard validation passed for all scenarios

---

## 📚 Key Learnings
- End-to-end verification flow based on real industry specifications
- Practical experience with UVM agents, sequences, monitors, and scoreboards
- Handling asynchronous inputs and multi-clock domains
- Debugging corner cases and protocol-related issues
- Building reusable and scalable verification environments

---

## 🔮 Future Scope
- Assertion-Based Verification (SVA)
- Functional and Code Coverage Closure
- Formal Verification
- FPGA Prototyping
- SoC-Level Integration and Regression Testing

---

## 📌 Project Domain
**Integrated VLSI – Design & Verification using UVM**
