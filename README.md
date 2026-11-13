# The waiting time for a bridge pattern in simple random walk

Yitzchak Shmalo

Paper: [paper/main.pdf](paper/main.pdf) (source [paper/main.tex](paper/main.tex)).

Fix $\lambda\in\mathbb R$ and let $T_n$ be the first time at which the last $n$ steps of a simple symmetric random
walk form a bridge from $0$ to the level nearest $\lambda\sqrt n$ of the right parity. Pitman and Tang
(arXiv:1411.0041) showed that $E T_n$ is of order $n$ and asked for its exact asymptotics. The paper proves
$E T_n\sim\gamma_\lambda n$, where $\gamma_\lambda=1+E F_\lambda$ and $F_\lambda$ is the first time at which the
Slepian process $B(t+1)-B(t)$ hits $\lambda$. The constant is a convergent series of integrals of determinants of
heat kernels, from Shepp's formulas for the Slepian process, with an explicit bound on the remainder. Numerically
$\gamma_0\approx1.5439$ and $\gamma_1\approx2.4135$.

## Code

No step of the proof uses computation. Run from the repository root:

```sh
python3 code/exact_waiting.py                       # exact E T_n by the matching matrix and by the prefix automaton
c++ -O3 -std=c++17 code/simulate.cpp -o code/simulate
python3 code/run_simulations.py                     # Monte Carlo estimates of E T_n
python3 code/slepian_integrals.py                   # quasi-Monte Carlo values of the series for the constant
```

The outputs used in the paper are in `data/`: `exact_waiting.csv` (Table 1), `monte_carlo.csv` (Table 2),
`slepian_slabs.csv` and `slepian_constants.csv` (the values of $\gamma_0$ and $\gamma_1$ with their tail bounds).
The first two files also contain rows for first-passage patterns (family `FP`) and for Gaussian increments
(`gaussian` = 1), which the paper does not use. The Python scripts need NumPy, SciPy and SymPy.

## Funding

The research presented in this paper was supported by the European Research Council (ERC) under the European
Union's Horizon Europe research and innovation program (grant agreement No. 101041711), by the Simons Foundation
as part of the Collaboration on the Mathematical and Scientific Foundations of Deep Learning, by Heights Labs, by
Convex Nexus Capital, by the Israel Science Foundation (grant number 2258/19), and by the Israel Science Foundation
(ISF Grant 4101/25). Computational resources were provided in part by Google Cloud through its education credits
program (credit 530550103).

## License

MIT, see `LICENSE`.
