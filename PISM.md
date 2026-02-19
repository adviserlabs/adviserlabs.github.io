<img width="50%" alt="Adviser Logo" src="https://github.com/user-attachments/assets/cfcfd483-98f4-48c7-9e6f-f07f0b5e196c" />

&nbsp;

[Home](README.md) [Documentation](https://github.com/adviserlabs/docs) [Icepack](Icepack) [PISM](PISM)

***

As an example of one of the many use cases for Adviser, we describe how we can simplify a computational glaciology research workflow with [PISM](https://www.pism.io).
At a high level:

```
# Set up and run a PISM simulation with automatic instance selection
> adviser run --setup "./setup_pism.sh" "./run_pism.sh"
# Run ML training using specific HW capabilities without naming instance types
> adviser run "python train.py" --gpu 1 --ram 32
# Scaled PISM run for 4-node MPI environment on AWS
> adviser run --setup "./setup_pism.sh" "./run_pism.sh --np 96" --cloud aws --num-nodes 4 --instance-type hpc7a.12xlarge
```

## Adviser-PISM Integration

PISM is a hybrid shallow-ice/shallow-shelf (SIA+SSA) glaciology model used widely in cryospheric modeling and sea-level applications.
Installing PISM reproducibly is notoriously challenging due to its multilayered dependency tree spanning build tools (CMake), scientific libraries (MPI, PETSc, NetCDF, FFTW, GSL, UDUNITS), and a separate Python environment with its own requirements.
The stack is also fragile: PISM’s own documentation warns that if multiple MPI implementations coexist, PETSc can "get confused" and fail, recommending users uninstall all but one MPI library—a destructive step that is impractical on shared systems or complex local environments.
The Adviser–PISM integration encapsulates the full build and execution procedure into a compact workflow, enabling new users to run validated PISM configurations without manual environment and installation management.

## Greenland Workflow & Visualizations

We use Adviser to run a Greenland-scale ice-sheet spin-up simulation derived from the [PISM manual](https://www.pism.io/docs/manual/std-greenland/index.html).
The simulation is initialized via PISM’s bootstrapping procedure and run under MPI parallelism from 10kyr BP to present (year−10000 to 0) using 10km horizontal grid spacing, constant-climate surface forcing, and PISM’s SIA+SSA dynamics model.
To demonstrate Adviser’s parameter injection capability, we override the default pseudo-plastic sliding law exponent from 𝑞= 0.25 to 𝑞= 0.5, simulating more linear sliding behavior and producing a present-day state suitable for subsequent experiments.
The diagnostic visualization output of surface velocity magnitude velsurf_mag is shown below, validating that Adviser can execute a full ice-sheet spin-up workflow and produce domain-standard model fields at scale.

<picture>
  <!-- For mobile devices -->
  <source width="100%" media="(max-width: 600px)" srcset="https://github.com/user-attachments/assets/c6c17686-c8f1-43ec-99a1-3ba3792947ef">
  
  <!-- For tablets or medium screens -->
  <source width="75%" media="(max-width: 1200px)" srcset="https://github.com/user-attachments/assets/c6c17686-c8f1-43ec-99a1-3ba3792947ef">
  
  <!-- Default/fallback for desktop -->
  <img width="50%" alt="Surface Velocity Magnitude" src="https://github.com/user-attachments/assets/c6c17686-c8f1-43ec-99a1-3ba3792947ef" />
</picture>

