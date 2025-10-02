# 🏥 Hospital Inventory Optimization

This repository contains an **Project** that models and solves a **hospital inventory management problem** using **Operations Research techniques**.  
It determines optimal ordering quantities and schedules for multiple medical items while respecting budget, storage, and safety stock constraints.

---

## 📌 Features

- **Synthetic Data Generation**  
  Creates realistic seasonal and random demand for hospital items.

- **EOQ & ROP Calculation**  
  Computes **Economic Order Quantity (EOQ)** and **Reorder Point (ROP)** for each item.

- **Mixed Integer Programming (MIP)**  
  Optimises multi-period inventory decisions using **PuLP**.

- **Constraints Modeled**
  - Monthly budget limit (₹1,000,000)
  - Storage capacity
  - Safety stock requirements

- **Automated Output Files**
  - `synthetic_hospital_demand.csv` – daily usage logs
  - `synthetic_item_master.csv` – item parameters
  - `inventory_with_eoq_rop.csv` – EOQ/ROP & current stock
  - `mip_orders.csv` – monthly order schedule
  - `mip_inventories.csv` – end-of-month stock levels
  - `mip_objective_components.csv` – cost breakdown
  - `reorder_alerts.csv` – items below ROP

---

## 📊 Model Formulation

**Decision Variables**
- $x_{i,t}$ : units of item $i$ ordered in month $t$
- $I_{i,t}$ : inventory of item $i$ at the end of month $t$
- $y_{i,t}$ : binary variable, 1 if an order is placed

**Objective Function**
$$
\text{Minimise} \quad \sum_{i,t} c_i x_{i,t} + \sum_{i,t} S_i y_{i,t} + \sum_{i,t} h_i I_{i,t}
$$

**Constraints**
- **Inventory balance:** $I_{i,t} = I_{i,t-1} + x_{i,t} - d_{i,t}$
- **Budget:** $\sum_i c_i x_{i,t} \le B_t$
- **Storage:** $\sum_i s_i I_{i,t} \le \text{StorageCap}$
- **Safety stock:** $I_{i,t} \ge \text{ROP}_i$
- **Big-M order linking:** $x_{i,t} \le M_i y_{i,t}$

---

## 📈 Visualisation in Notebook
The notebook produces:
- Bar chart: total orders per month
- Line chart: inventory levels vs. ROP
- Storage utilisation trends
- Tabular reorder alerts

---

## 🚀 How to Run
```bash
# Install dependencies
pip install pandas numpy pulp matplotlib

# Run the notebook
jupyter notebook Hospital_Inventory_Management.ipynb
