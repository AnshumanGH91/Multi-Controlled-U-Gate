# Multi-Controlled U Gate in Qiskit

This project implements an **n-controlled U gate (CnU)** using **Qiskit**, based on only single-qubit gates and controlled-X (CX) gates. It is completed as part of the **Erdos Institute Quantum Computing Bootcamp** (Mini-Project #2).

---

## 📌 Problem Statement

Given:
- A unitary matrix `U ∈ U(2)`
- An integer `n > 0`

Construct a quantum circuit on `n+1` qubits (plus possible ancillas) that implements a multi-controlled-U gate `CⁿU`. The gate acts as follows:

CⁿU |x⟩ₙ |y⟩ =
|x⟩ₙ U|y⟩ if x = (1,1,...,1)
|x⟩ₙ |y⟩ otherwise


### ❗ Constraints:
- Only 1-qubit gates (U) and CX (CNOT) gates may be used.
- No classical control or measurements.
- Ancilla qubits are allowed if needed.

---

## 🧠 Approach

The implementation uses the **recursive decomposition** method from [Barenco et al., 1995](https://arxiv.org/abs/quant-ph/9503016), where multi-controlled gates are broken down using ancilla qubits and Toffoli (CCX) gates.

For `n > 2`:
- Ancilla qubits reduce the n-control condition to a single-control.
- The unitary `U` is then applied conditionally using a `CU` gate.
- Finally, the ancilla logic is uncomputed to preserve reversibility.

---

## 🧪 Benchmarking

We benchmarked the construction for small values of `n`:

| n (Control Qubits) | Ancilla Qubits Used | Total Qubits | Gate Depth | Total Gates |
|--------------------|---------------------|--------------|------------|-------------|
| 2                  | 0                   | 3            | *X*        | *X*         |
| 3                  | 1                   | 5            | *X*        | *X*         |
| 4                  | 2                   | 7            | *X*        | *X*         |
| 5                  | 3                   | 9            | *X*        | *X*         |

*Values marked 'X' can be filled in using `qiskit.transpile()`.*

### Sample Code:
```python
from qiskit import transpile
qc = multi_controlled_u(n=4, u_gate=UGate(np.pi, 0, np.pi))
tqc = transpile(qc, basis_gates=['u', 'cx'])
print("Depth:", tqc.depth())
print("Gate count:", tqc.count_ops())


Feel free to reach out with questions or suggestions!

Author: [Your Name]
Bootcamp: Erdos Institute Quantum Computing, 2025


---

## 🛠️ Want Help Generating This?

I can auto-generate a `README.md` file for your specific code and notebook content. Just upload your `.ipynb` here or confirm which details you want included.

Would you like me to create this README file for you based on your notebook?
