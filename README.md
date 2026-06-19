# Comfy-OOM-Shield v0.7

**Check a ComfyUI workflow before it crashes your GPU.**

Comfy-OOM-Shield is a local Windows pre-run checker for ComfyUI workflow JSON files.

It helps you inspect downloaded or unfamiliar workflows before pressing **Queue**:

* estimate VRAM, RAM, and SSD swap risk
* identify heavy workflow patterns
* report detected model and reference-media entries
* flag possible custom node types
* detect local video and API/cloud workflows
* repair some broken workflow JSON files
* safely optimize supported Flux / Flux1 / Flux2 workflows for lower-VRAM systems

> Built mainly for Windows users with 6 GB–12 GB VRAM who regularly test workflows from Civitai, YouTube, Reddit, Discord, or workflow packs.

---

## Why use it?

Downloaded a random ComfyUI workflow and do not know whether it will:

* exceed your VRAM
* spill into RAM or SSD swap
* require unknown models or media
* depend on custom nodes
* use local video models or cloud/API nodes
* fail because the JSON is damaged

Comfy-OOM-Shield gives you a readable preflight report before you run it.


Download workflow
        ↓
Analyze in Comfy-OOM-Shield
        ↓
Read Preflight Verdict
        ↓
Check risks, assets, and node hints
        ↓
Apply a safe fix when available
        ↓
Open the result in ComfyUI


---

## Main Features

### Preflight Verdict

The report begins with a clear workflow verdict:

* workflow type
* VRAM risk
* RAM / SSD swap risk
* detected assets
* safe optimization availability
* main reason for the current risk level

Example:


PREFLIGHT VERDICT
=================

Status: HIGH RISK
Main reason: This workflow may be too heavy for your GPU.
Workflow type: Generation Workflow, Image Workflow
VRAM risk: HIGH
Safe optimizations available: YES


---

### Recommended Next Steps

Comfy-OOM-Shield generates practical recommendations based on the detected workflow.

Examples:

* try **Optimize For My GPU**
* reduce video frame count manually
* reduce video resolution manually
* lower sampler steps manually
* verify possible custom nodes in ComfyUI-Manager
* close background GPU applications
* use memory-efficient attention

Recommendations are based on detected workflow information and do not silently modify unsupported settings.

---

### VRAM, RAM, and SSD Swap Estimation

The analyzer estimates:

* approximate workflow memory size
* available VRAM
* possible VRAM overflow
* possible RAM spill
* possible SSD swap usage
* expected performance penalty
* compatibility with common NVIDIA GPUs

Memory estimates are approximate and should be treated as pre-run guidance, not exact runtime measurements.

---

### Workflow Type Detection

Supported classification includes:

* image workflows
* generation workflows
* local video workflows
* API/cloud video workflows
* Flux / Flux1 / Flux2 workflows
* GGUF-related workflows
* workflows containing subgraphs

Local and API/cloud workflows are reported separately to avoid fake local VRAM warnings for cloud-based generation.

---

### Detected Assets

The analyzer reports model and reference-media entries found inside the workflow.

Examples:

* checkpoints
* diffusion models
* UNET models
* CLIP and text encoders
* VAE files
* LoRA files
* input images
* input videos
* audio references

Detected assets are not automatically confirmed to exist on the current computer.

Only confirmed missing files should be described as missing.

---

### Custom Node Hints

Comfy-OOM-Shield may flag node types that should be verified manually.


MISSING CUSTOM NODES / INSTALL HINTS
====================================

- ExampleNode: possibly custom / verify manually.


Custom Node Hints are informational only.

Comfy-OOM-Shield does not:

* install custom nodes automatically
* clone Git repositories
* download unknown node packages
* modify the ComfyUI installation

Use ComfyUI-Manager or the node developer’s documentation for manual installation.

---

### Fix Workflow

The fixer can repair some common workflow JSON problems:

* trailing commas
* garbage after valid JSON
* supported structural problems
* some invalid or incomplete fields

It also reports:

* broken links
* missing source or target nodes
* dangling references
* unrepaired problems
* warnings that require manual review

The fixer does not guess how ambiguous graph connections should be rebuilt.

Fixed files are saved separately with:


_fixed.json


---

### Optimize For My GPU

The current safe optimizer supports confirmed Flux / Flux1 / Flux2 image-workflow patterns.

Example safe change:


1024 × 1024 → 768 × 768


The optimizer preserves important workflow values:

* seed
* prompt
* model filename
* CFG
* unrelated numeric values
* connected latent settings that should remain unchanged

Optimized files are saved separately with:


_optimized.json


If no confirmed safe change is found, the app reports:


No safe optimizations applied.


This does not mean the workflow is broken.

It means the optimizer did not find a change that could be applied safely.

---

## Video Workflow Support

Video workflows are analyzed, but they are **not automatically optimized yet**.

For local video workflows such as Wan, Comfy-OOM-Shield may recommend:

* reducing frame count manually
* reducing resolution manually
* reducing sampler steps manually
* closing background GPU applications
* using memory-efficient attention

Wan and other video workflow settings are not mutated automatically.

API/cloud video workflows are detected separately and are not treated as heavy local-model workflows.

---

## AI Assistant — Optional

Comfy-OOM-Shield includes an optional AI Assistant.

Supported provider options may include:

* local Ollama / Qwen
* OpenAI API

AI Chat is optional.

Without AI Chat:

* Workflow Analyzer still works
* Fix Workflow still works
* Optimize For My GPU still works
* Save Report still works
* Copy Report still works

Recommended local model:


qwen3:8b


Included helper scripts may provide:


install_ollama.bat
install_qwen.bat
start_ollama.bat
test_qwen.bat


---

## Save and Share Reports

The complete analysis can be:

* copied to the clipboard
* saved as a text report
* shared when requesting help on GitHub, Discord, or other ComfyUI communities

The saved report includes:

* Preflight Verdict
* Recommended Next Steps
* detailed memory analysis
* detected assets
* custom node hints
* GPU compatibility
* optimization suggestions
* developer analysis

---

## What’s New in v0.7

* Added **Preflight Verdict**
* Added **Recommended Next Steps**
* Added report-only **Custom Node Hints**
* Improved detected asset wording
* Improved report structure and readability
* Improved Flux optimization availability checks
* Improved optimizer result messages
* Improved separation of local video and API/cloud workflows
* Added clear video-workflow limitations
* Disabled automatic custom-node installation paths
* Improved Save Report and Copy Report consistency
* Removed unnecessary analyzer debug output
* Added additional regression and safety tests

Current verification:


Compilation: passed
Unit tests: 39 passed
Manual GUI smoke test: passed


---

## Installation

1. Download the latest Windows ZIP from GitHub Releases.
2. Extract the complete archive.
3. Open the extracted folder.
4. Run:


Comfy-OOM-Shield.exe


Do not run the executable directly from inside the ZIP archive.

The standalone release does not need to be installed inside the ComfyUI folder.

---

## Basic Usage

1. Launch `Comfy-OOM-Shield.exe`.
2. Drag and drop a ComfyUI workflow `.json` file.
3. Read the Preflight Verdict.
4. Review memory risk, detected assets, and node hints.
5. Use **Fix Workflow** when JSON repair is needed.
6. Use **Optimize For My GPU** when a safe optimization is available.
7. Open the resulting JSON in ComfyUI.

---

## System Requirements

Recommended:

* Windows 10 or Windows 11, 64-bit
* 8 GB RAM minimum
* 16 GB RAM or more recommended
* NVIDIA GPU recommended for local ComfyUI generation
* Internet connection only for downloads, OpenAI, or optional AI setup

The analyzer itself does not require a high-end GPU.

---

## Current Limitations

* VRAM, RAM, and SSD swap estimates are approximate.
* The app cannot guarantee that a workflow will run successfully.
* Full automatic video optimization is not implemented.
* Automatic custom-node installation is not implemented.
* Detected model and media references are not automatically confirmed to exist.
* Full reconstruction of heavily corrupted JSON is not implemented.
* Some normal nodes may still appear under Custom Node Hints.
* Some failures may come from ComfyUI updates, drivers, Python packages, custom-node regressions, or model incompatibility rather than the workflow JSON.

---

## Who Is This For?

Comfy-OOM-Shield is mainly built for:

* Windows ComfyUI users
* 6 GB, 8 GB, 10 GB, and 12 GB VRAM systems
* users downloading random workflows
* Flux / Flux1 / Flux2 users
* Wan and local-video users
* beginners and intermediate ComfyUI users
* anyone tired of OOM crashes, broken JSON, and unclear workflow dependencies

---

## Project Status

Comfy-OOM-Shield is under active development.

Current stable release:


v0.7


Planned future work may include:

* safer optimizer profiles
* improved model and node databases
* improved VRAM estimation
* broader workflow compatibility
* expanded video workflow support
* improved repair validation and rollback

Features will be added gradually, with safety preferred over aggressive workflow mutation.

---

## Support and Feedback

Useful feedback includes:

* broken workflow JSON files
* low-VRAM Flux workflows
* Wan and other video workflows
* incorrect workflow classification
* false custom-node warnings
* inaccurate memory estimates
* optimizer no-op cases

Please include the saved report when opening an issue.

---

## Disclaimer

Comfy-OOM-Shield is provided as-is.

Always keep backups of important workflows.

The application is designed to provide pre-run analysis, supported repairs, safe optimization, and practical recommendations. It is not a replacement for testing the final workflow inside ComfyUI.
