<img width="50%" alt="Adviser Logo" src="https://github.com/user-attachments/assets/cfcfd483-98f4-48c7-9e6f-f07f0b5e196c" />

&nbsp;

[Home](README.md) [Documentation](https://github.com/adviserlabs/docs) [Icepack](Icepack) [PISM](PISM)

***

As an example of one of the many use cases for Adviser, we describe how we can simplify a computational glaciology research workflow with [Icepack](https://icepack.github.io).

Icepack is a Python finite-element framework for glacier modeling built on [Firedrake](https://www.firedrakeproject.org).
Its workflows require complex environments (MPI, PETSc, platform-specific compilation) that make reproducible deployment nontrivial;
Adviser encapsulates these complexities within a reusable template enabling single-command launch.

## Pine Island Glacier Workflow

We use Adviser to simulate the Pine Island Glacier, a major West Antarctic outlet glacier studied for its sea-level rise contribution.
The simulation has two stages: an inversion step estimates physical parameters (e.g., basal friction) by fitting to observational velocity data, producing a calibrated initial state followed by a forward simulation then evolves glacier thickness and geometry over 200 years under prescribed surface mass balance and basal melt forcing, solving velocity diagnostically and updating thickness prognostically with floating/grounded regions determined dynamically via flotation criteria.
This workflow supports multiple glacier geometries (2017 and 2020 ice-shelf front configurations) and represents a non-trivial scientific workload with complex dependencies, multi-stage execution, and domain-specific outputs.
During execution, structured outputs and diagnostics are produced, including spatial fields and auto-generated visualizations; intermediate and final artifacts (parameter fields, state variables, logs) are written to disk with post-processing specifications that extract diagnostics without manual setup.
Diagnostic outputs are shown below: basal melt rate (𝑚/𝑦𝑟) in (a), floating versus grounded ice mask indicating grounding line geometry in (b), and ice thickness change rate (𝑚/𝑦𝑟) in (c).
These demonstrate Adviser successfully orchestrating a complex simulation-to-visualization pipeline for a realistic scientific workflow.

<picture>
  <!-- For mobile devices, tablets, or medium screens -->
  <source width="100%" media="(max-width: 1200px)" srcset="https://github.com/user-attachments/assets/ddf3c348-1e8b-435b-8e18-c4345c836f6f">
  
  <!-- Default/fallback for desktop -->
  <img width="50%" alt="Icepack Pine Island Glacier model" src="https://github.com/user-attachments/assets/ddf3c348-1e8b-435b-8e18-c4345c836f6f" />
</picture>
