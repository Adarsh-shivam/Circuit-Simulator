**Circuit Simulation with Sympy, NumPy & Matplotlib in Google Colab**
A Python-based supernode and nodal analysis tool that runs interactively in Google Colab. Enter your circuit data via prompts and obtain frequency- and time-domain node voltages and branch currents, with optional plots.

---

## 🚀 Features

* **Supernodal & Nodal Analysis**: Automatically builds system equations for circuits with resistors, capacitors, inductors, current sources, and voltage sources.
* **Initial Conditions**: Supports initial inductor currents and capacitor voltages.
* **Symbolic Frequency‑Domain**: Uses Sympy to derive Laplace‑domain equations.
* **Time‑Domain Response**: Computes inverse Laplace transforms for node voltages and branch currents.
* **Interactive Plots**: Optionally plot currents and voltages versus time using Matplotlib.
* **Zero‑Setup**: Runs entirely in Google Colab, no local environment configuration required.

---

## 📥 Getting Started

1. **Open in Google Colab**
   Click the **Open in Colab** badge (or go to [colab.research.google.com](https://colab.research.google.com) and upload the `*.ipynb`).
2. **Run All Cells**

   * The notebook will prompt for the number of nodes and each element in sequence.
   * Enter values interactively in the Colab input fields.

---

## ⚙️ Input Prompts & Workflow

1. **Number of Nodes**
   Enter the total number of circuit nodes (integer).
2. **Resistors**

   * **How many?** Enter count.
   * For each: specify terminal nodes and resistance (Ω).
3. **Inductors**

   * **How many?** Enter count.
   * For each: terminal nodes, inductance (H), and initial current (A) if any.
4. **Capacitors**

   * **How many?** Enter count.
   * For each: terminal nodes, capacitance (F), and initial voltage (V) if any.
5. **Current Sources**

   * **How many?** Enter count.
   * For each: value (A), positive and negative node.
6. **Voltage Sources & Supernodes**

   * **How many sources?** Enter count.
   * For each: positive node, negative node, DC value (V).
   * Specify which node is ground.

> **Note**: Node numbering starts at 1. Ground node voltage is fixed to 0.

---

## 📊 Results & Interpretation

* **Frequency‑Domain Solution**: Displays symbolic node voltages in the Laplace domain (functions of `s`).
* **Time‑Domain Solution**: Inverse Laplace transform gives node voltages vs. time (with `DiracDelta` for initial impulses).
* **Branch Currents Matrix**: After solving, a matrix of currents between every pair of nodes (symbolic in `s`).

---

## 🔍 Query Specific Branch Currents or Voltages

After computing global solutions, the notebook enters an interactive loop:

```text
Do you want to see specific Branch Current or voltage? yes=1, no=0:
```

* Enter `1` to query a branch; provide:

  * First node, second node
  * Element type: resistor=0, inductor=1, capacitor=2, voltage source=3
* The script computes the symbolic current or voltage, shows its time‑domain form, and asks whether to plot.

---

## 📈 Plotting

* **Current Plot**: If chosen, plots current `i(t)` vs. `t` over

  $0, 2π$.
* **Voltage Plot**: Plots voltage `v(t)` vs. `t` over the same interval.

---

## 🛠️ Customization & Extension

* Modify the input sequence to add more elements or sources.
* Extend support to AC sinusoidal sources by replacing constant voltages with `sp.sin(…)` or `sp.exp(…)` before Laplace transform.
* Adjust time sampling range or resolution by editing the `np.linspace` parameters.

---

## 🎓 How It Works (at a Glance)

1. **Admittance Matrix** built from resistors, inductors (1/(L s)), and capacitors (C s).
2. **Current Vector** assembled from independent sources and initial conditions.
3. **Equation System**:

   * Nodal equations for non‑supernode nodes.
   * Supernode equations from voltage sources.
4. **Solve Symbolically** for node voltages.
5. **Compute Branch Currents** via `I = Y (V_i - V_j)` or in supernode special case.
6. **Inverse Laplace** for all symbolic results.

---

## 📄 License

This project is released under the MIT License. Feel free to copy, modify, and distribute.
