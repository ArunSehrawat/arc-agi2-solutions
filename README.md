# arc-agi2-solutions

Python programs that solve a subset of [ARC-AGI-2](https://github.com/arcprize/ARC-AGI-2) training tasks. Each program is a candidate transformation inferred from demonstration pairs — not necessarily the true underlying rule.

The official task JSON files are **not** shipped here. Clone [ARC-AGI-2](https://github.com/arcprize/ARC-AGI-2) next to this code (see Setup).

## Why this exists

A collection of **problem–program pairs** for inspection and for possible use in LLM fine-tuning or program-synthesis experiments. This repository is not a training framework and is not an ARC-AGI-2 solver that generalizes to held-out tasks.

## Coverage

| File | Solvers | Origin |
|------|---------|--------|
| `our_task_solutions.py` | 222 | Manually written for this repository (**our main contribution**) |
| `barc_task_solutions.py` | 158 | Converted [BARC seed](https://github.com/xu3kev/BARC/tree/master/seeds) programs |
| `llm_task_solutions.py` | 37 | Additional solvers for tasks not already covered |

34 task IDs appear in both `our_task_solutions.py` and `barc_task_solutions.py`. Across the three files there are **383 unique** training-task IDs (of 1000). All listed solvers match every official train and test pair. Remaining training tasks and all 120 public evaluation tasks are left unsolved rather than guessed.

## Contents

| File | Description |
|------|-------------|
| `our_task_solutions.py` | Manually written `solve_<task_id>` functions, plus `verify_solution_outputs` (**our main contribution**).|
| `barc_task_solutions.py` | Converted BARC seeds in the same `solve_<task_id>` format. |
| `llm_task_solutions.py` | Additional verified solvers in the same format. |
| `grid_utils.py` | Shared grid helpers used by `our_task_solutions.py` and `llm_task_solutions.py`. |
| `barc_common.py` | BARC grid helpers from [BARC `common.py`](https://github.com/xu3kev/BARC/tree/master/seeds). |
| `validate.py` | Checks every solver against official train and test pairs. |
| `validate_solutions.ipynb` | Same checks, with grid visualizations. |
| `LICENSE` | MIT License for original code in this repository. |
| `NOTICE` | Attribution for BARC conversions and ARC-AGI-2. |
| `CITATION.cff` | Citation metadata for this repository and related papers. |

Each solver looks like:

```python
def solve_<task_id>(input_grid):
    """Concepts and transformation steps inferred from the demonstrations."""
    input_grid = np.array(input_grid)
    ...
    return output_grid
```

## Setup

Python 3.9+, NumPy, SciPy, and Matplotlib:

```bash
pip install -r requirements.txt
git clone https://github.com/arcprize/ARC-AGI-2.git
```

The dataset clone must sit at `ARC-AGI-2/` in the repository root (that path is gitignored).

For the notebook only, also install Jupyter (`pip install notebook`).

## Usage

Call a solver on a grid (list of lists or NumPy array):

```python
from our_task_solutions import solve_c9e6f938

output_grid = solve_c9e6f938(input_grid)
```

Verify every solver from the repository root:

```bash
python validate.py
```

Or open `validate_solutions.ipynb` and run all cells.

BARC seeds that index grids as `[x, y]` (first axis horizontal) are wrapped with `_barc_xy` so they match official ARC `[row, col]` arrays. Alternate `_Kevin.py` seeds and ConceptARC examples from [BARC/seeds](https://github.com/xu3kev/BARC/tree/master/seeds) were not converted. Two BARC seed IDs (`0dfd9992`, `a3df8b1e`) are not in ARC-AGI-2 and were omitted.

## License

Original code in this repository is under the MIT License (see `LICENSE`).

`barc_task_solutions.py` and `barc_common.py` are conversions of BARC seed code. The BARC repository does not currently publish a LICENSE file; those files remain copyright of the BARC authors. See `NOTICE`.

ARC-AGI-2 task data is Apache-2.0 and is not redistributed here.

## References

- [ARC-AGI-2 dataset](https://github.com/arcprize/ARC-AGI-2) (Apache-2.0)
- François Chollet, [On the Measure of Intelligence](https://arxiv.org/abs/1911.01547)
- [BARC seeds](https://github.com/xu3kev/BARC/tree/master/seeds)
- Wen-Ding Li et al., [Combining Induction and Transduction for Abstract Reasoning](https://arxiv.org/abs/2411.02272)
