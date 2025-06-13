---
title: From Fermion Leakage to Decoherence
layout: default
---

<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# From Fermion Leakage to Decoherence  
### A Lattice Interpretation of Warped Extra Dimensions

We reinterpret the leakage of brane-localized fermions into a warped extra dimension as coherent amplitude diffusion into a discrete lattice of possibility nodes, \(\Phi_n\). By replacing the geometric fifth coordinate \(y\) with a site index \(n\), we recast the 5D Dirac equation as a tight-binding model. This relabeling maintains unitarity while eliminating the need for physical extra geometry.

---

## 1. Framework Summary

- In RS models, bulk fermions “leak” off the brane into a warped 5D bulk.
- We propose: replace the fifth dimension \(y\) with a discrete index \(n\) labeling nodes in a coherence lattice \(\Phi_n(x)\).
- The probability current \(J^y\) becomes \(\partial_n \Pi_n(x)\): amplitude migration across non-geometric degrees of freedom.

---

## 2. Three-Site Quiver Model

We model a 3-site lattice:  
- Site 0 ≡ brane  
- Sites 1–2 ≡ coherence nodes

With hopping \(k\) and mass \(M\), the Hamiltonian is:

$$
H = \begin{pmatrix} M & k & 0 \\\\ k & 0 & k \\\\ 0 & k & 0 \end{pmatrix}
$$

We compute the ground state of \(H\) and track off-brane amplitude as a function of \(M\).

### Result:
- \(M \lesssim 0.5k\): mode remains brane-localized
- \(M \sim k\): rapid leakage into lattice
- \(M \gg k\): full delocalization

---

## 3. Leakage Phase Diagram

We sweep over bulk mass \(M \in [0, 4]\) and hopping strength \(k \in [0, 2]\).  
Color indicates probability in lattice sites 1 + 2.

| Region        | Behavior               | RS Analog                         |
|---------------|------------------------|------------------------------------|
| Dark wedge    | Bound brane mode       | Localized chiral fermion           |
| Gradient band | Leakage transition     | KK mixing onset                    |
| Yellow zone   | Full delocalization    | Zero-mode dissolves into bulk      |

![Leakage Phase Diagram](images/leakage_plot.png)

---

## 4. Decoherence Rate \(\Gamma(M, k)\)

We compute the effective decoherence rate for a brane-local probe coupled to \(\Phi_1, \Phi_2\):

$$
\Gamma(M, k) \propto g_1^2 |\psi_1|^2 + g_2^2 |\psi_2|^2
$$

with \(g_1 = 1\), \(g_2 = 0.8\), and \(\Lambda_{1,2} = 1\).

- Low \(\Gamma\): amplitude remains on brane
- High \(\Gamma\): decoherence induced by off-brane leakage

![Decoherence Rate](images/decoherence_map.png)

---

## 5. Next Directions

| Step               | Adds                                |
|--------------------|--------------------------------------|
| Real-time animation | Amplitude drift as \(M\) increases |
| 5–7 site lattice    | KK tower and mode repulsion         |
| Experimental fit    | Match decoherence to real systems   |

---

## 6. Source Code (Wolfram Language)

```wolfram
leakageProb[M_, k_] := Module[{H, evals, vecs, psi, p1, p2},
  H = {{M, k, 0}, {k, 0, k}, {0, k, 0}};
  {evals, vecs} = Eigensystem[H];
  psi = Normalize[vecs[[ First@Ordering[Abs[evals]] ]]];
  p1 = Abs[psi[[2]]]^2; p2 = Abs[psi[[3]]]^2;
  Return[p1 + 0.64 p2];
];
