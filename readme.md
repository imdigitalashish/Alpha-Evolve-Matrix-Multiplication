# Exploring and Verifying Advanced Matrix Multiplication Algorithms

This repository contains Python implementations and verifications of various matrix multiplication algorithms, with a special focus on novel algorithms discovered by systems like Google DeepMind's AlphaEvolve. Our goal is to understand, implement, and benchmark these cutting-edge techniques against classical and established fast matrix multiplication methods.

## Introduction

Matrix multiplication is a fundamental operation in countless scientific and engineering domains. While the classical algorithm for $N \times N$ matrices takes $O(N^3)$ operations, algorithms like Strassen's (1969) showed that a lower asymptotic complexity is achievable ($O(N^{\log_2 7}) \approx O(N^{2.807})$). The search for the true exponent of matrix multiplication, $\omega$, and for practically faster algorithms for specific matrix sizes, remains an active area of research.

Recent advances in AI, particularly from Google DeepMind, have led to the discovery of new, efficient tensor decompositions for matrix multiplication. This repository explores some of these findings.

## Algorithms Implemented

1.  **Classical Matrix Multiplication:**
    *   Standard $O(N^3)$ algorithm (implicitly used by `numpy.dot` or `@` for dense matrices when no specialized libraries are in play, though NumPy often uses highly optimized BLAS libraries).

2.  **Strassen's Algorithm:**
    *   Implementation for $2 \times 2$ matrices (7 scalar multiplications).
    *   Recursive implementation for $4 \times 4$ matrices (using $7 \times 7 = 49$ scalar multiplications).

3.  **AlphaEvolve Algorithms (from DeepMind's AlphaEvolve Results):**
    *   **Rank-48 Decomposition for $\langle 4,4,4 \rangle$ over $0.5\mathbb{C}$:**
        *   This algorithm multiplies two $4 \times 4$ matrices using **48 scalar multiplications**, with coefficients involving complex numbers whose real and imaginary parts are multiples of 0.5. This is an improvement over the recursive Strassen approach (49 multiplications) and the classical approach (64 multiplications) for this specific size.
    *   *(Potentially add more algorithms from the notebook as you implement them, e.g., for $\langle 2,4,5 \rangle$, $\langle 3,3,3 \rangle$, etc.)*

## Code Structure

*   `matmul_algorithms.py` (or similar name): Contains the Python functions for the different matrix multiplication algorithms.
    *   `strassen2x2()`
    *   `strassen4x4_recursive()`
    *   `alphaevolve4x4_matmul()`
    *   Data for AlphaEvolve decompositions (e.g., `decomposition_444`).
*   `verify_algorithms.py` (or similar name): Script to test the implementations against NumPy's standard matrix multiplication and to verify the tensor decompositions themselves.
*   `README.md`: This file.

## Verification

The correctness of the implemented algorithms is verified by:
1.  Comparing their output against the results obtained from NumPy's highly optimized matrix multiplication (`@` operator) for various random input matrices.
2.  For tensor-decomposition-based algorithms, a verification function (adapted from DeepMind's `mathematical_results.ipynb`) is used to confirm that the provided factor matrices correctly reconstruct the standard matrix multiplication tensor.

## Results

Our verification confirms:
*   Strassen's recursive algorithm for $4 \times 4$ matrices indeed uses 49 scalar multiplications and produces correct results.
*   The AlphaEvolve algorithm for $\langle 4,4,4 \rangle$ (using `decomposition_444`) correctly multiplies $4 \times 4$ matrices using **48 scalar multiplications**.

This work highlights the potential of AI-driven discovery in finding novel, efficient algorithms for fundamental mathematical problems.



## Future Work

*   Implement and verify other tensor decompositions presented in the AlphaEvolve results.
*   Explore the practical performance implications of these algorithms, especially when applied recursively.
*   Investigate the numerical stability of algorithms involving non-integer or complex coefficients.

## Author

*   Ashish @imdigitalashish on twitter, discord, literally everywhere

## Acknowledgements

*   The tensor decompositions for AlphaEvolve algorithms are sourced from the "Mathematical Results for AlphaEvolve" notebook by Google DeepMind.
    *   [AlphaEvolve Results GitHub](https://github.com/google-deepmind/alphaevolve_results)
    *   [Mathematical Results Notebook](https://colab.research.google.com/github/google-deepmind/alphaevolve_results/blob/master/mathematical_results.ipynb)