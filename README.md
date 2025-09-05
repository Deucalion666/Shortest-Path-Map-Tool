# 🧬 SPM-PyMOL: Local Shortest Path Map (SPM) Generator

**SPM-PyMOL** provides a command-line and Jupyter-friendly Python implementation of the **Shortest Path Map (SPM)** method for analyzing protein dynamics from molecular dynamics (MD) simulations.  
It reproduces the core ideas of the SPMweb tool locally and extends it with **direct PyMOL visualization scripts**.

---

## ✨ Features

### 🧩 SPM Network Construction
- Builds **residue–residue communication networks** from distance and cross-correlation matrices.
- Supports both **`.npy` (NumPy)** and **`.dat` (whitespace text)** matrix formats.

### 🎯 Threshold Control
| Parameter | Description | Default |
|-----------|-------------|---------|
| `-t` Distance cutoff | Defines which residue pairs are connected in the initial graph | 6 Å |
| `-s` Significance cutoff | Filters edges based on their contribution to shortest paths | 0.3 |

### 📊 Network Analysis
- **Normalizes edge usage** in shortest paths.
- Computes **per-residue importance scores**.

### 🔬 PyMOL Visualization
- Exports a **`.pml` script** in SPMweb style for visualization.
- **Residues** → spheres, scaled by importance score.
- **Edges** → sticks, scaled by significance.
- **Color coding:** `blue` = positive correlations, `red` = negative correlations.
- All edges grouped into a `PATH_<pdb>` object for easy toggling.

---

## 📂 Outputs

| File | Description |
|------|-------------|
| `spm_edges.tsv` | Tab-separated list of significant edges, including correlation sign |
| `spm_nodes.tsv` | Tab-separated list of residues ranked by importance score |
| `spm.pml` | PyMOL script for network visualization on the protein structure |

---

## 📖 Background on SPM

The **Shortest Path Map (SPM)** method simplifies a protein's **structure and dynamics** into a **weighted graph**:

- **Nodes:** residues  
- **Edges:** weighted by distance and correlation of residue movements during MD simulations  
- **Edge weight:**  

\[
\mathbf{l_{ij}} = -\log(|c_{ij}|)
\]

where \( c_{ij} \) is the correlation between **C\(_\alpha\)** displacements of residues \( i \) and \( j \).  

- Shortest paths are computed using **Dijkstra's algorithm**.  
- The resulting SPM highlights **critical residues** that are highly correlated and strongly impact conformational dynamics — useful for identifying **mutation hotspots in enzyme design**.

---

## 📝 Inputs Required by SPMweb
1. **Protein structure file:** `.pdb`  
2. **Distance matrix:** `.dat` or `.npy` from MD simulation  
3. **Correlation matrix:** `.dat` or `.npy` from MD simulation

---

## 🚀 Usage Example

```bash
python spm.py -d distance_matrix.npy -c correlation_matrix.npy -p structure.pdb -t 6 -s 0.3
