# High-Performance Computing (HPC) Cluster Deployments & Analysis

This repository documents my practical experience with High-Performance Computing (HPC) environments, specifically utilizing the SINES NUST supercomputing cluster. It showcases my ability to adapt parallel and distributed applications for execution on large-scale shared resources, analyze performance, and interpret results in a real-world HPC context.

## Key Learning Outcomes & Skills:

* **HPC Cluster Interaction:** `Remote access (SSH)`, `file transfer (SCP)`.
* **Compute Node Management & Profiling:** `Node discovery (ping, nproc, hostname)`, `CPU specification detailing (lscpu)`, `node status monitoring (UP, DOWN, UNAVAILABLE)`, `understanding node heterogeneity`.
* **Job Submission Systems:** Understanding `Sun Grid Engine (SGE)` or similar queueing concepts (`qsub`, `qstat`, `qdel`).
* **MPI Environment on HPC:** Compiling and running `MPI applications` on multi-node setups using `host files`.
* **Performance Analysis:** Collecting and presenting performance metrics (e.g., execution time, speedup, efficiency) for HPC-scale computations.
* **Data Visualization:** Generating `graphs` (Execution Time vs. P, Speedup vs. P) to illustrate performance characteristics and scalability.
* **Troubleshooting HPC Environments:** Addressing compilation, linking, and runtime issues on older GCC versions and specific hardware.
* **CMake Build System:** Configuring complex multi-target projects for HPC deployment.

## Projects & Reports:

### 1. SINES NUST HPC Cluster Exploration & Mapping
* **Description:** A detailed reconnaissance of the SINES HPC cluster, including identifying accessible compute nodes, their CPU specifications, and current operational status.
* **Skills Showcased:** `Shell scripting for node probing`, `system information retrieval (lscpu, nproc)`, `understanding cluster heterogeneity (CPU models, core counts)`, `inferring node utilization`.
* **Source:** `Project Proposal.docx` (Part I)
* **Details:**
    * `probe_nodes.sh`: Shell script used to automate node status checks.
    * Detailed table mapping node names to their status (UP, DOWN, UNAVAILABLE), core counts, and observed hostnames.
    * `lscpu` outputs for identified node types (e.g., 16-core Intel Xeon E5520, 24-core Intel Xeon 5600 series), highlighting CPU heterogeneity.
    * Discussion on inferred node utilization due to lack of direct scheduler access.

### 2. HPC MPI Hello World Deployment
* **Description:** Initial successful deployment and execution of a basic MPI program on the SINES NUST HPC cluster.
* **Skills Showcased:** `SSH access`, `SCP file transfer`, `basic MPI compilation (mpic++)`, `mpirun` with compute nodes.
* **Source:** `CS435 Lab 12 Manual - Distributed Computing with MPI.docx` (Task 1)
* **Details:** Screenshots of SSH login, `top` command for node usage verification, compilation, and `mpirun` output on `afrit.rcms.nust.edu.pk` cluster.

### 3. HPC Distributed Matrix Multiplication Deployment
* **Description:** Execution and analysis of the MPI-based distributed matrix multiplication on multiple compute nodes of the SINES NUST HPC.
* **Skills Showcased:** `Creating host files` for multi-node MPI execution, `scaling MPI applications` across physical machines, `observing distributed performance`.
* **Source:** `CS435 Lab 12 Manual - Distributed Computing with MPI.docx` (Task 2)
* **Details:**
    * `hostfile.txt`: Example host file content (`compute-0-0.local`, `compute-0-5.local`).
    * Screenshots of compilation and `mpirun --hostfile` execution, demonstrating matrix multiplication distributed across specified compute nodes.
    * Discussion on observed execution times.

### 4. HPC Parallel Laplace Solver: Performance Analysis & Deployment
* **Description:** Comprehensive implementation and performance analysis of a 2D Laplace solver using sequential, OpenMP, and MPI paradigms, specifically benchmarked on the SINES NUST HPC head node.
* **Skills Showcased:** `Numerical solver implementation (Jacobi iteration)`, `sequential, OpenMP, and MPI parallelization strategies`, `CMake for multi-target builds`, `performance benchmarking (omp_get_wtime, MPI_Wtime)`, `detailed scalability analysis (speedup, execution time graphs)`, `discussion of performance bottlenecks (shared memory contention, communication overheads)`.
* **Source:** `Project Proposal.docx` (Part II) and `PDP-Spring2025-Assignment-03-10032025.pdf` (Question 3).
* **Details:**
    * `laplace_sequential.cpp`: Reference sequential implementation.
    * `laplace_openmp.cpp`: OpenMP-parallelized version (using `#pragma omp parallel for collapse(2)`).
    * `laplace_mpi.cpp`: MPI-parallelized version (using row-wise domain decomposition and `MPI_Sendrecv` for halo exchange).
    * `CMakeLists.txt`: Configures building all three executables with correct OpenMP and MPI flags for the HPC environment.
    * **Extensive Performance Graphs:**
        * [cite_start]Execution Time vs. P (N=1000, 100 Epochs) [cite: 1237]
        * [cite_start]Speedup vs. P (N=1000, 100 Epochs) [cite: 1238]
        * [cite_start]Execution Time vs. P (N=2000, 100 Epochs) [cite: 1239]
        * [cite_start]Speedup vs. P (N=2000, 100 Epochs) [cite: 1240]
    * [cite_start]**Detailed Discussion of Results:** Analyzing trends, comparing OpenMP vs. MPI scaling, and identifying bottlenecks observed on the shared head node. [cite: 1242, 1243, 1244, 1245, 1246, 1247, 1248, 1249, 1250, 1251, 1252, 1253, 1254, 1255, 1256, 1257, 1258, 1259, 1260, 1261]
    * [cite_start]**Challenges and Solutions:** Documenting practical issues faced during development on HPC (e.g., GCC 4.4.7 compatibility, `vi` pasting, CMake errors) and their resolutions. [cite: 1263, 1264, 1265, 1266, 1267, 1268, 1269, 1270, 1271, 1272, 1273, 1274, 1275]

## HPC Environment Details:

Based on the project findings, the SINES NUST HPC cluster (`afrit.rcms.nust.edu.pk`) features:
* [cite_start]**Total Nodes:** 34 (2 Head Nodes, 32 Compute Nodes) [cite: 3270]
* [cite_start]**Processing Cores:** 272 total, with observed heterogeneity (e.g., 16-core Intel Xeon E5520, 24-core Intel Xeon 5600 "Westmere-EP" nodes). [cite: 3270, 834, 844]
* [cite_start]**Total Memory:** 1.312TB [cite: 3270]
* [cite_start]**Operating System:** CentOS Linux 6.5 [cite: 3270]
* [cite_start]**Interconnects:** Infiniband Switch (40 Gbps Data Rate) [cite: 3270, 3244]
* [cite_start]**Storage:** 22TB SAN Storage [cite: 3270, 3261]
* [cite_start]**GPU Cores:** 30720 (NVidia Tesla S1070 GPUs on compute nodes). [cite: 3270, 3220, 3221, 3224]
* [cite_start]**Peak Performance:** 132 Teraflops [cite: 3270]
