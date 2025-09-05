# Shortest-Path-Map-Tool
SPMweb is a webserver for the Shortest Path Map (SPM) tool, which identifies key conformationally-relevant positions in enzymes. It helps in computational enzyme design by pinpointing distal positions connected to the active site. Freely available for academia.

🧬 SPM-PyMOL: Local Shortest Path Map (SPM) Generator

This repository provides a command-line and Jupyter-friendly Python implementation of the Shortest Path Map (SPM) method for analyzing protein dynamics from molecular dynamics (MD) simulations.

It reproduces the core ideas of the SPMweb tool (Bocchinfuso et al., 2017)
 in a local, scriptable workflow, and extends it with direct PyMOL visualization scripts.

✨ Features

SPM network construction

Builds residue–residue communication networks from distance and cross-correlation matrices.

Supports .npy (NumPy) and .dat (whitespace text) matrix formats.

Threshold control

Distance cutoff (-t) defines which residue pairs are connected.

Significance cutoff (-s) filters edges by their contribution to shortest paths.

Network analysis

Normalizes edge usage in shortest paths.

Computes per-residue importance scores.

PyMOL visualization

Exports .pml script in the SPMweb style:

Residues shown as spheres (scaled by importance).

Edges shown as sticks (scaled by significance).

Color coding: blue = positive correlations, red = negative correlations.

Groups all edges into a PATH_<pdb> object for easy toggling.

Outputs

spm_edges.tsv — list of significant edges (with correlation sign).

spm_nodes.tsv — ranked residue importance scores.

spm.pml — PyMOL script for network visualization.
