# P4P CapsNet Accelerator — Research Compendium

**Project:** Capsule Network Acceleration on the AMD/Xilinx ZCU102  
**Institution:** University of Auckland  
**Contributors:** Tonny Chen · Beren Eskildsen  
**Academic year:** 2026  
**Repository (project reference):** https://github.com/wolfuoa/P4P-CapsuleNetworkAccelerator

> **Purpose**  
> This compendium preserves the documentation, source code, experimental procedures, evidence and individual submissions associated with the CapsNet accelerator project. It is organised so that future students can understand the design, rebuild the implementation, reproduce the measurements and extend the work.

**Status:** This README defines the *intended submission structure*. Before submitting, ensure that every listed file exists, update any names that differ from the final deliverables, and remove unused placeholders. The linked public repository may not contain all final project files; use the archived source code in this compendium as the authoritative submitted revision.

---

## 1. Start here

| Your goal | Start with | Then consult |
|---|---|---|
| Understand the project and its contributions | [`01_Main_Compendium/Research_Compendium.pdf`](01_Main_Compendium/Research_Compendium.pdf) | `03_System_Architecture/` |
| Set up a new development computer | [`02_Software_Setup_Guide/Software_Setup_Guide.pdf`](02_Software_Setup_Guide/Software_Setup_Guide.pdf) | `04_Source_Code/` |
| Understand model compilation and FPGA integration | `03_System_Architecture/` | `04_Source_Code/` |
| Build and run the accelerator on ZCU102 | `02_Software_Setup_Guide/` | `04_Source_Code/` |
| Repeat the measurements | `05_Experimental_Procedures/` | `06_Experimental_Data/`, `07_Verification_and_Results/` |
| Recreate the report figures | `06_Experimental_Data/` | `01_Main_Compendium/` |
| Inspect project decisions and individual work | `08_Project_Records/` | `09_Individual_Submissions/` |
| Continue the research | `10_Future_Development/` | Source code and experiment guides |

### Recommended reproduction sequence

1. **Read the project overview** in `01_Main_Compendium/` and the system diagrams in `03_System_Architecture/`.
2. **Prepare the host computer** using the step-by-step guide in `02_Software_Setup_Guide/`. This covers the Ubuntu environment, relevant Xilinx tools, model toolchain and ZCU102 deployment prerequisites.
3. **Build or obtain the required model and FPGA artifacts** using the exact source revision and commands documented alongside `04_Source_Code/`.
4. **Deploy to the ZCU102 and run a first inference.** Verify the expected model output and save the terminal log before proceeding.
5. **Reproduce experiments** with `05_Experimental_Procedures/`, checking the equipment, operating points, data inputs and pass/fail criteria.
6. **Regenerate figures and tables** using the raw data and processing scripts in `06_Experimental_Data/`; compare them against the archived results in `07_Verification_and_Results/`.

**Two distinct configurations:** The *integrated CapsNet system* is used for end-to-end inference and application-level measurements; the *standalone DigitCaps design* is used for isolated accelerator and voltage–frequency/power characterisation. Do not interchange their build artifacts or measurement procedures.

---

## 2. Directory structure

```text
P4P_CapsNet_Research_Compendium/
├── README.md                         # Entry point and navigation
│
├── 01_Main_Compendium/
│   └── Research_Compendium.pdf       # Project overview and evidence index
│
├── 02_Software_Setup_Guide/
│   ├── Software_Setup_Guide.pdf      # From host setup to first inference
│   └── installation_screenshots/    # Screenshots referenced in the guide
│
├── 03_System_Architecture/
│   ├── CapsNet_System_Architecture.pdf
│   ├── Model_Compilation_Flow.pdf
│   └── FPGA_Build_Flow.pdf
│
├── 04_Source_Code/
│   ├── CapsNet_Model/                # Model preparation/quantisation/compilation
│   ├── DigitCaps_V1_V2_V3/          # HLS versions and relevant verification
│   ├── FPGA_Build_Scripts/          # Build/link/package configuration and scripts
│   └── Host_Applications/           # Embedded runtime and host applications
│
├── 05_Experimental_Procedures/
│   ├── Latency_and_Accuracy.pdf
│   ├── Voltage_Frequency_Characterisation.pdf
│   └── Power_and_Energy_Measurement.pdf
│
├── 06_Experimental_Data/
│   ├── Raw_Data/                     # Original measurements and unmodified logs
│   ├── Processed_Data/               # Derived datasets and calculations
│   └── Plotting_Scripts/             # Scripts used to generate figures/tables
│
├── 07_Verification_and_Results/      # Checks, comparison results, synthesis reports
├── 08_Project_Records/              # Meetings, decisions and progress records
│
├── 09_Individual_Submissions/
│   ├── Tonny_Chen/                   # Tonny's individual Canvas submissions
│   └── Beren_Eskildsen/              # Beren's individual Canvas submissions
│
└── 10_Future_Development/           # Limitations, recommendations and next steps
```

The numbering indicates **navigation order**, not strict execution order. Original data files should remain unmodified; put cleaned or calculated data under `Processed_Data/`.

---

## 3. What each folder contains

### `01_Main_Compendium/` — Project overview
A concise description of the research objective, system design, major findings, roles and contributions. This document acts as an *index* to the technical evidence, rather than repeating every command or raw result.

### `02_Software_Setup_Guide/` — From zero to first inference
A standalone walk-through for a future student starting with a compatible Ubuntu computer and ZCU102 board. It should identify hardware prerequisites, exact software versions, installation instructions, environment variables, project dependencies, build commands, board boot steps, a **first successful inference** test, expected outputs and common troubleshooting steps. The reference development flow uses the Xilinx 2022.1-era toolchain; record the *actual validated versions* and paths instead of assuming they are interchangeable.

### `03_System_Architecture/` — How the system fits together
Diagrams showing the CapsNet processing stages, software/hardware split, partial-model compilation, HLS compilation and final FPGA/SD-card packaging. Include the original system/SD-card generation diagram here alongside any revised final diagrams.

### `04_Source_Code/` — Rebuildable project sources
Code and machine-readable configurations needed to reproduce the implementation: the model preparation workflow, DigitCaps V1/V2/V3 designs, custom accelerators as applicable, build scripts, host applications, testbenches, weights and relevant configuration files. Each major subfolder should contain a short local README specifying the entry-point command, required inputs and expected outputs. Archive a known-good Git commit or source snapshot; avoid relying solely on a moving branch or external link.

### `05_Experimental_Procedures/` — How measurements were made
Step-by-step procedures for latency/accuracy, voltage–frequency reliability, and energy/power testing. Specify the experimental configuration, equipment and board identifiers, firmware/build version, test dataset, trial count, timing procedure, supply settings, settling time, reference output, success/failure definition and data-file naming. If calibration was not applicable or not carried out, say so explicitly.

### `06_Experimental_Data/` — Evidence behind the plots
Store **raw data as collected**, derived data separately, and the analysis/plotting scripts required to regenerate report figures. For each final figure or table, include or maintain a mapping from reported result → script → processed data → original measurement or build report. Record units and column definitions for CSV files.

### `07_Verification_and_Results/` — Verification evidence
Preserve functional checks, reference-versus-accelerator comparisons, bit-exact checks where applicable, representative runtime logs, synthesis/implementation timing and resource reports, and final experiment result summaries. Clearly distinguish measured results from calculated values or estimates.

### `08_Project_Records/` — Research process
Meeting minutes, decisions, task allocations, dated progress notes and records of significant design changes or unsuccessful experiments. Organise chronologically and avoid including unrelated or sensitive personal material.

### `09_Individual_Submissions/` — Evidence of joint and individual work
Keep each contributor's **actual final Canvas-submitted files** in the corresponding named directory. Include a short manifest noting the filename, submission type and version/date. Joint work can be referenced by both manifests without unnecessary duplication if the exact joint submission is available elsewhere in the compendium.

### `10_Future_Development/` — Hand-over notes
Known limitations, unverified areas, unresolved technical issues, reproducibility risks and feasible follow-up research. Distinguish demonstrated findings from ideas that have not been implemented or tested.

---

## 4. Reproduction prerequisites and boundaries

**Baseline hardware:** ZCU102 development board, compatible power supply, USB-UART connection, Ethernet connection, bootable SD card and reader, and a suitable x86-64 development workstation.

**Software:** The detailed setup guide is the authoritative source for installation steps, tool versions and configuration. Record the exact Vivado/Vitis/Vitis HLS, Vitis AI, platform, PetaLinux/SDK, XRT and Python versions actually used. For any version that cannot be installed or verified, document the limitation rather than silently substituting a newer release.

**External dependencies:** Proprietary AMD/Xilinx tools, platform images, licensed components and very large generated artifacts may not be included in the archive. Their versions, official retrieval locations, expected filenames and generation procedures must be specified in the relevant guide.

**Validation boundary:** A documented procedure is not automatically a clean-room-tested procedure. Mark any steps or platforms that were not independently retested, and retain evidence of the configuration in which results were obtained.

---

## 5. File conventions and data traceability

- Prefer descriptive filenames with a design, frequency and date/run identifier where meaningful; for example, `digitcaps_v3_300MHz_voltage_sweep_run01.csv`.
- Use relative paths from this README so that documents work after the ZIP is extracted.
- Preserve original logs and raw measurements; perform cleaning and aggregation only in `Processed_Data/`.
- For scripts, document command-line arguments, units, expected input files and generated outputs.
- For archived build artifacts, record the source revision, tools, platform and configuration that generated them.
- For important large files omitted because of the submission limit, provide regeneration instructions and, where available, a SHA-256 checksum.

## 6. Submission checklist

- [ ] README hyperlinks and directory names match the **actual ZIP contents**.
- [ ] Main Compendium and both technical guides are complete and readable.
- [ ] Software setup and first-inference instructions have been verified, or any unverified steps are labelled.
- [ ] Integrated and standalone build flows are clearly distinguished.
- [ ] Source code, configurations, test inputs and executable build scripts are included or precisely referenced.
- [ ] Each major reported result is traceable to raw data or original tool reports.
- [ ] Equipment, test conditions, calibration/verification and experiment procedures are recorded.
- [ ] Both students' final Canvas submissions are clearly identified.
- [ ] No credentials, private keys or unnecessary bulky build caches are included.
- [ ] Final archive is within the Canvas size limit (less than 2 GB), or alternative submission arrangements have been agreed with the supervisor.

---

**Questions or omissions:** Consult the main report and the guide corresponding to the relevant workflow. If a required artifact is absent, record that fact explicitly rather than treating an external GitHub repository as proof that the missing final version is available.
