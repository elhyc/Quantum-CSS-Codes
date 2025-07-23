# Quantum Error Correcting Codes: CSS Codes

Quantum <b>C</b>(alderbank)-<b>S</b>(teane)-<b>S</b>(hor) codes are a class of <em>stabilizer codes</em>, whose stabilizer generators have nice properties. In particular, quantum CSS codes are stabilizer codes whose stabilizer generators can be expressed as Pauli strings containing only X and Z terms. One important simplification this gives us is that when performs syndrome measurements for these codes, one can measure X stabilizers and Z stabilizers independently from each other. This property allows us to implement syndrome recovery procedures in a simpler fashion. 


This repository contains a [Python source file](StabilizerCodesGottesman.py) and a  [Jupyter notebook](quantumCSS_examples.ipynb).

<ul> The python source file:</ul>
This python module contains a number of useful methods, applicable to the simulation of quantum CSS error correcting codes. The central method of interest in this file is the method <em>"CSS_code"</em>. 

This method takes as input:

1. a stabilizer generator matrix (for a CSS code)
2. code parameters $$n$$ and $$k$$, where the CSS code inputted is a $$[[n,k]]$$ stabilizer code
3. a physical error rate

The method then outputs:

1. a quantum circuit which prepares the logical all-zero state for the given CSS code (not necessarily in a fault-tolerant fashion)
2. applies a uniform Pauli error channel to the physical qubits, with physical error rate given by the inputted error rate
3. applies syndrome measurements and appropriate recovery procedures when needed
4. measures the final state of the physical data qubits onto a final measurement register. 


- The algorithm used for preparing the logical zero state is based on [Gottesman's algorithm](https://arxiv.org/abs/quant-ph/9705052).

- The python source file also contains a method that can prepare appropriate logical operators for a given quantum CSS code. Therefore, one can also prepare various logical states that are different from the logical all zero state.

- At the moment, the syndrome recovery procedure is very primitive, it will only reliably handle single X or Z errors. However, for specific quantum CSS codes, one can use the methods provided in the source file in conjunction with a more sophisicated syndrome recovery algorithm in a more specific context (for example, [Kitaev's toric code](https://github.com/elhyc/Kitaev-Toric-Code) or quantum color codes). 


<ul>The Jupyter notebook:</ul>

The Jupyter notebook presented in this repository contains demonstrations of the StabilizerCodesGottesman.py module. It demonstrates the error correcting procedure for three examples of quantum CSS codes: 1. the Steane code (a $$[[7,1,3]]$$-code), 2. The "merged Steane code" (a $$[[12,2,3]]$$-code) and 3. the $$[[15,7,3]]$$ quantum Hamming code. All of these examples have code distance of $3$, so it can be guaranteed to correct single $X$ and $Z$ errors, given the error model we are assuming here (i.e. everything is run ideally, Pauli error is only introduced at the specific stage between initial state preparation and syndrome measurement).
