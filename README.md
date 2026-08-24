# Numerical Convergence of the Fluxonium Hamiltonian in a Harmonic-Oscillator Basis

Python code accompanying the study **"Analysis of Numerical Convergence of the Fluxonium Hamiltonian in a Harmonic-Oscillator Basis."**

This project examines the numerical convergence of the fluxonium Hamiltonian when it is represented and diagonalized in a truncated harmonic-oscillator basis. The analysis studies how basis-truncation error depends on basis cutoff, external magnetic flux, and excitation level.

## Overview

The fluxonium Hamiltonian is represented as

\[
\hat{H}
=
4E_C\hat{n}^2
+
\frac{1}{2}E_L\hat{\phi}^2
-
E_J\cos(\hat{\phi}-2\pi f),
\]

where

\[
f=\frac{\Phi_{\mathrm{ext}}}{\Phi_0}.
\]

Using the harmonic part of the circuit as the basis Hamiltonian gives

\[
\hat{H}_0
=
\sqrt{8E_CE_L}
\left(
\hat{a}^{\dagger}\hat{a}
+
\frac{1}{2}
\right),
\]

with phase operator

\[
\hat{\phi}
=
\left(\frac{2E_C}{E_L}\right)^{1/4}
(\hat{a}+\hat{a}^{\dagger}).
\]

The infinite harmonic-oscillator basis is truncated to a finite dimension \(N\), and the resulting Hamiltonian matrix is diagonalized numerically.

The main purpose of the project is to determine how large \(N\) must be before the calculated low-energy spectrum is numerically stable.

## Analysis

The notebook includes:

- construction and diagonalization of the fluxonium Hamiltonian;
- convergence of the \(0\rightarrow1\) transition frequency with basis cutoff;
- convergence across external magnetic flux;
- state-dependent convergence of \(E_k-E_0\);
- determination of the minimum persistently converged basis cutoff;
- validation against the analytically solvable \(E_J=0\) harmonic limit;
- comparison with the independent `scqubits` implementation;
- calculation of the low-lying fluxonium energy spectrum.

A reference calculation with

\[
N_{\mathrm{ref}}=200
\]

is used to estimate basis-truncation error. The default convergence threshold in the notebook is

\[
\epsilon < 10^{-3}\ \mathrm{GHz} = 1\ \mathrm{MHz}.
\]

Because the convergence error is not necessarily monotonic, the minimum cutoff is defined using **persistent convergence**: all subsequently tested cutoffs must remain below the specified tolerance.

The 1 MHz threshold is a numerical benchmark used for this analysis and should not be interpreted as a universal accuracy requirement for fluxonium calculations.

## Validation

Two independent checks are included.

### Harmonic limit

Setting \(E_J=0\) removes the nonlinear Josephson contribution. The Hamiltonian becomes an exactly solvable harmonic oscillator with relative eigenenergies

\[
E_k-E_0
=
k\sqrt{8E_CE_L}.
\]

The numerical results are compared directly with this analytical expression.

### Comparison with scqubits

The custom Hamiltonian implementation is also compared with the `Fluxonium` class from [`scqubits`](https://scqubits.readthedocs.io/).

Identical values of \(E_J\), \(E_C\), \(E_L\), external flux, and basis cutoff are supplied to both implementations, allowing the matrix construction and flux convention to be independently cross-checked.

## Repository Contents

```text
.
├── fluxonium_convergence_analysis_commented.ipynb
├── README.md
└── figures/
