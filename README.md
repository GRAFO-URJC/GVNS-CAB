# A general variable neighborhood search for the cyclic antibandwidth problem <a href="https://doi.org/10.1007/s10589-021-00334-y"><img src="https://upload.wikimedia.org/wikipedia/commons/1/11/DOI_logo.svg" alt="DOI" width="20"/></a>

<!-- Load Material Symbols Outlined for icons -->
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=mail" />

[![License](https://img.shields.io/badge/License-CC_BY--NC--ND-blue.svg)](LICENSE)
[![Code](https://img.shields.io/badge/Code-Java-orange.svg)]()

## Abstract

Graph Layout Problems refer to a family of optimization problems where the aim is to assign the vertices of an input graph to the vertices of a structured host graph, optimizing a certain objective function. In this paper, we tackle one of these problems, named Cyclic Antibandwidth Problem, where the objective is to maximize the minimum distance of all adjacent vertices, computed in a cycle host graph. Specifically, we propose a General Variable Neighborhood Search which combines an efficient Variable Neighborhood Descent with a novel destruction–reconstruction shaking procedure. Additionally, our proposal takes advantage of two new exploration strategies for this problem: a criterion for breaking the tie of solutions with the same objective function and an efficient evaluation of neighboring solutions. Furthermore, two new neighborhood reduction strategies are proposed. We conduct a thorough computational experience by comparing the algorithm proposed with the current state-of-the-art methods over a set of previously reported instances. The associated results show the merit of the introduced algorithm, emerging as the best performance method in those instances where the optima are unknown.

**Published in:** Computational Optimization and Applications (2022) 81:657–687

## Authors

- Sergio Cavero <sup>1,*</sup> <a href="mailto:sergio.cavero@urjc.es" aria-label="Sergio Cavero Email"><img src="https://upload.wikimedia.org/wikipedia/commons/b/b1/Email_Shiny_Icon.svg" alt="email" width="20" style="vertical-align:middle;"/></a> <a href="https://orcid.org/0000-0002-5258-5915"><img src="https://upload.wikimedia.org/wikipedia/commons/0/06/ORCID_iD.svg" alt="ORCID" width="20" style="vertical-align:middle;"/></a>
- Eduardo G. Pardo <sup>1</sup> <a href="mailto:eduardo.pardo@urjc.es" aria-label="Eduardo G. Pardo Email"><img src="https://upload.wikimedia.org/wikipedia/commons/b/b1/Email_Shiny_Icon.svg" alt="email" width="20" style="vertical-align:middle;"/></a> <a href="https://orcid.org/0000-0002-6247-5269"><img src="https://upload.wikimedia.org/wikipedia/commons/0/06/ORCID_iD.svg" alt="ORCID" width="20" style="vertical-align:middle;"/></a>
- Abraham Duarte <sup>1</sup> <a href="mailto:abraham.duarte@urjc.es" aria-label="Abraham Duarte Email"><img src="https://upload.wikimedia.org/wikipedia/commons/b/b1/Email_Shiny_Icon.svg" alt="email" width="20" style="vertical-align:middle;"/></a> <a href="https://orcid.org/0000-0002-4532-3124"><img src="https://upload.wikimedia.org/wikipedia/commons/0/06/ORCID_iD.svg" alt="ORCID" width="20" style="vertical-align:middle;"/></a>

### Affiliations

1. Universidad Rey Juan Carlos, Madrid, Spain — C. Tulipán, s/n, Móstoles, 28933, Madrid, Spain

<sup>*</sup>Corresponding author.

---

## Table of Contents

- [Repository Structure](#repository-structure)
- [Abstract](#abstract)
- [Authors](#authors)
- [Problem Description](#problem-description)
- [Datasets](#datasets)
- [Code Execution](#code-execution)
- [Requirements](#requirements)
- [Results](#results)
- [License](#license)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)
- [Contact](#contact)

---

## Repository Structure

```
.
├── code/
│   ├── GLP.jar           # Executable JAR file
│   ├── config.txt        # Configuration file
│   ├── instances/        # Problem instances
│   └── output/           # Generated results
├── instances/            # All available problem instances
│   ├── complete_binary_trees/
│   ├── cycles/
│   ├── toroidalmeshes/
│   ├── paths/
│   ├── grids/
│   ├── harwell_boeing/
│   ├── 3dmeshes/
│   ├── hypercubes/
│   ├── hamming/
│   ├── double_stars/
│   ├── random/
│   └── caterpillars/
├── results/
│   └── results.xlsx      # Experimental results
├── LICENSE               # License file
└── README.md             # This file
```

---

## Problem Description

The **Cyclic Antibandwidth Problem (CAB)** is a graph layout problem where the goal is to embed a candidate graph into a cycle host graph. The objective is to maximize the minimum distance between adjacent vertices when mapped onto the cycle.

### Formal Definition

Given:
- A candidate graph G = (V_G, E_G) with n vertices and m edges
- A host cycle graph C_n = (V_C, E_C) with n vertices

The problem seeks a bijective function φ: V_G → V_C that maximizes:

```
CAB(G, φ) = min_{(u,v)∈E_G} {p(φ(u), φ(v))}
```

where p represents the shortest path distance in the cycle between the mapped vertices.

### Complexity

The Cyclic Antibandwidth Problem has been proved to be **NP-Hard** for general graphs.

### Applications

The CAB problem has applications in:
- Multiprocessor scheduling
- Frequency assignment
- Graph drawing
- VLSI design
- Batch-processing workloads
- Network scheduling

---

## Datasets

The repository contains **295 problem instances** divided into two main categories:

### Instances with Known Optimum (132 instances)

| Dataset | Instances | Description |
|---------|-----------|-------------|
| Paths | 24 | Path graphs |
| Cycles | 24 | Cycle graphs |
| Grids | 23 | Two-dimensional meshes |
| Toroidal grids | 37 | Toroidal mesh graphs |
| Hamming graphs | 24 | Hamming graphs |

### Instances with Unknown Optimum (163 instances)

| Dataset | Instances | Description |
|---------|-----------|-------------|
| Three-dimensional meshes | 20 | 3D mesh graphs |
| Double stars | 20 | Double star graphs |
| Hypercubes | 7 | Hypercube graphs |
| Caterpillars | 40 | Caterpillar graphs |
| Complete binary trees | 24 | Complete binary tree graphs |
| Harwell-Boeing | 24 | Harwell-Boeing sparse matrix collection |
| Random connected graphs | 28 | Randomly generated connected graphs |

### Instance Format

Each instance is encoded as a plain text file representing a graph:
- The first line contains the number of vertices `n` and edges `m`
- Each subsequent line contains a pair of integers `u v` representing an edge between vertex `u` and vertex `v`
- Vertices are indexed from 0 to n-1

**Example:**
```
10 15
0 1
0 2
1 3
2 4
3 5
...
```

All instances can be downloaded at this repository but are also available at: [https://grafo.etsii.urjc.es/optsicom/cab/](https://grafo.etsii.urjc.es/optsicom/cab/).

---

## Code Execution

The algorithm is provided as an executable JAR file (`GLP.jar`) that can be run directly.

### Running the Program

```bash
java -jar GLP.jar
```

### Configuration

The program uses a `config.txt` file where you need to specify:
1. The instance folder you want to execute
2. The directory where results should be saved
3. The maximum time limit (in seconds)

**Example `config.txt`:**
```
instances/test/
output/
150
```

### Expected Output

When you run the program, you should see output similar to:
```
java -jar GLP.jar
instances/test/
output/
150
CGVNS-FB-IWP-S-SDC-TMAX=150-KMAX=0.01(min15)-MAX_TIME_GVNS=25-ts20250518185213
caterpillar_5_4.txt
15
```

An output folder will be created containing an Excel file with per-instance results.

---

## Requirements

- **Java**: Java 11 or higher
- **Memory**: Minimum 4GB RAM recommended for large instances
- **OS**: Cross-platform (Windows, Linux, macOS)

### System Requirements

- Intel Core i7 or equivalent processor (recommended)
- 16 GB RAM for optimal performance on large instances
- Approximately 100 MB disk space for instances and results

---

## Results

Experimental results are stored in the `results/` folder. The results include:
- Instance name
- Best solution found
- Solution quality metrics
- Execution time
- Algorithm parameters used

The main results file is available as `results/results.xlsx` containing comprehensive experimental data comparing our MS-GVNS algorithm with state-of-the-art methods.

### Performance Highlights

Our **Multistart General Variable Neighborhood Search (MS-GVNS)** achieved:

#### For Instances with Unknown Optimum:
- **Best overall method** among compared algorithms
- **127 best solutions** found out of 147 instances
- **Average deviation of 0.33%** from best-known solutions
- **Statistically significant improvements** confirmed by Friedman test (p < 0.001)

#### For Instances with Known Optimum:
- **40 optimal solutions** found out of 120 instances
- **Average deviation of 11.72%** from optimal values
- Competitive performance with state-of-the-art methods

### Algorithm Features

The MS-GVNS incorporates several advanced strategies:

1. **Novel constructive procedure** based on Breadth-First Search (BFS)
2. **Variable Neighborhood Descent (VND)** with two complementary neighborhoods:
   - Insert neighborhood (N₁)
   - Swap neighborhood (N₂)
3. **Advanced exploration strategies**:
   - Tiebreak criterion for flat landscapes (AE₁)
   - Efficient move calculation (AE₂)
4. **Neighborhood reduction techniques**:
   - Candidate vertices selection (R₁)
   - Candidate assignments optimization (R₂)
5. **Destruction-reconstruction shaking procedure**

### Comparison with State-of-the-Art

Our method significantly outperforms previous approaches:

| Method | Year | Average Quality | Best Solutions (Unknown Optimum) |
|--------|------|----------------|----------------------------------|
| MACAB | 2011 | Baseline | 49/147 |
| HABC | 2013 | Previous SOTA | 58/147 |
| **MS-GVNS** | **2022** | **Best** | **127/147** |

---

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)** License.

### License Summary

**You are free to:**
- **Share** — copy and redistribute the material in any medium or format

**Under the following terms:**
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use.
- **NonCommercial** — You may not use the material for commercial purposes.
- **NoDerivatives** — If you remix, transform, or build upon the material, you may not distribute the modified material.

**No additional restrictions** — You may not apply legal terms or technological measures that legally restrict others from doing anything the license permits.

### Notices

You do not have to comply with the license for elements of the material in the public domain or where your use is permitted by an applicable exception or limitation.

No warranties are given. The license may not give you all of the permissions necessary for your intended use. For example, other rights such as publicity, privacy, or moral rights may limit how you use the material.

For the full license text, see: [https://creativecommons.org/licenses/by-nc-nd/4.0/](https://creativecommons.org/licenses/by-nc-nd/4.0/)

**Alternative licenses:** If you require a different license for commercial or academic use, please contact the corresponding author.

---

## Citation

If you use this work in your research, please cite our paper:

### DOI

<https://doi.org/10.1007/s10589-021-00334-y>

### BibTeX

```bibtex
@article{Cavero2022,
  title={A general variable neighborhood search for the cyclic antibandwidth problem},
  author={Cavero, Sergio and Pardo, Eduardo G. and Duarte, Abraham},
  journal={Computational Optimization and Applications},
  volume={81},
  number={3},
  pages={657--687},
  year={2022},
  publisher={Springer Science+Business Media, LLC},
  doi={10.1007/s10589-021-00334-y}
}
```

### APA Format

Cavero, S., Pardo, E. G., & Duarte, A. (2022). A general variable neighborhood search for the cyclic antibandwidth problem. *Computational Optimization and Applications*, *81*(3), 657-687. https://doi.org/10.1007/s10589-021-00334-y

### IEEE Format

S. Cavero, E. G. Pardo, and A. Duarte, "A general variable neighborhood search for the cyclic antibandwidth problem," *Comput. Optim. Appl.*, vol. 81, no. 3, pp. 657-687, 2022, doi: 10.1007/s10589-021-00334-y.

### MLA Format

Cavero, Sergio, Eduardo G. Pardo, and Abraham Duarte. "A general variable neighborhood search for the cyclic antibandwidth problem." *Computational Optimization and Applications* 81.3 (2022): 657-687.

---

## Acknowledgments

This research has been partially supported by:

- **Ministerio de Ciencia, Innovación y Universidades** — Grant Ref. PGC2018-095322-B-C22
- **Ministerio de Ciencia, Innovación y Universidades** — Grant Ref. FPU19/04098 (PhD Fellowship)
- **Comunidad de Madrid and European Regional Development Fund** — Grant Ref. P2018/TCS-4566

### Special Thanks

We would like to thank:
- The reviewers for their valuable feedback and suggestions that improved the quality of this work
- The research community for providing benchmark instances and previous comparative results
- Universidad Rey Juan Carlos for providing computational resources
- The authors of previous state-of-the-art methods (MACAB and HABC) for making their results available for comparison

**Funding Declaration:** The funders had no role in study design, data collection and analysis, decision to publish, or preparation of the manuscript.

---

## Contact

For questions, issues, or collaborations, please contact:

- **Sergio Cavero** (Corresponding Author): [sergio.cavero@urjc.es](mailto:sergio.cavero@urjc.es)
- **Eduardo G. Pardo**: [eduardo.pardo@urjc.es](mailto:eduardo.pardo@urjc.es)
- **Abraham Duarte**: [abraham.duarte@urjc.es](mailto:abraham.duarte@urjc.es)

### Additional Resources

- **Project Website**: [https://grafo.etsii.urjc.es/optsicom/cab/](https://grafo.etsii.urjc.es/optsicom/cab/)
- **Research Group**: GRAFO - Grupo de Algoritmos para la Optimización
- **Institution**: Universidad Rey Juan Carlos, Madrid, Spain

---

## Keywords

Cyclic antibandwidth problem · Graph layout problem · Metaheuristics · Variable neighborhood search · Combinatorial optimization · NP-hard problems · Heuristic algorithms

---

## Publication Details

**Received:** 8 February 2021  
**Accepted:** 12 November 2021  
**Published online:** 17 January 2022  
**Published in print:** 2022

**Copyright:** © The Author(s), under exclusive licence to Springer Science+Business Media, LLC, part of Springer Nature 2021

---

## Related Problems

The Cyclic Antibandwidth Problem is related to several other graph layout problems:

- **Antibandwidth Maximization Problem (AMP)**: Similar objective but on a path graph instead of a cycle
- **Cyclic Bandwidth Problem**: Minimization variant of the CAB
- **Cyclic Cutwidth Minimization Problem**: Minimizes edge congestion in cyclic layouts
- **Bandwidth Minimization Problem (BMP)**: Classic problem on path graphs
- **Vertex Separation Problem**: Related to graph layout on paths

### Relationship with AMP

The relationship between CAB and AMP can be expressed as:

```
(1/2) × AMP(G) ≤ CAB(G) ≤ AMP(G)
```

This provides bounds that can be used to evaluate solution quality for certain graph classes.

---

*For more information about graph layout problems and optimization algorithms, visit our research group website at [https://grafo.etsii.urjc.es/](https://grafo.etsii.urjc.es/)*
