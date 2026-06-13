# Comfy-OOM-Shield v0.5

Comfy-OOM-Shield is a Windows desktop assistant for analyzing, fixing and safely optimizing ComfyUI workflow JSON files.

It helps users understand workflow structure, VRAM/RAM pressure, GPU compatibility, heavy nodes, local models, reference media, video workflow type and safe optimization options before running heavy ComfyUI workflows.

v0.5 focuses on stability, safer workflow repair, safer Flux/Flux-style optimization, better subgraph handling, and improved local/API video workflow analysis.

---

## Main Features

* Workflow Analyzer
* Fix Workflow
* Optimize For My GPU
* AI Assistant / Chat
* Save Report
* Copy Report
* VRAM / RAM / SSD swap estimation
* GPU compatibility warnings
* Local model detection
* Reference media detection
* Subgraph workflow analysis
* Local video workflow detection
* API/cloud video workflow detection

---

## What Works in v0.5

### Workflow Analyzer

Comfy-OOM-Shield can analyze ComfyUI workflow JSON files and report:

* Workflow type
* Node count
* Workflow structure
* Subgraphs
* Heavy nodes
* Local model loader nodes
* Required local models
* Reference images/videos
* Local video workflows
* API/cloud video workflows
* VRAM/RAM/SSD swap risk
* GPU compatibility
* Practical optimization suggestions

---

### Fix Workflow

Fix Workflow is now safer and more useful.

It can:

* Repair some broken JSON workflow files
* Remove trailing commas when safe
* Remove garbage after a valid JSON document
* Validate root workflow links
* Validate subgraph links
* Support ComfyUI subgraph link formats
* Correctly handle ComfyUI subgraph input/output virtual nodes
* Detect broken links
* Report unsafe repair cases instead of guessing
* Save a repaired workflow as a separate `_fixed.json` file

Fix Workflow does **not** randomly rewrite:

* Seeds
* Prompts
* Model filenames
* CFG values
* Unknown numeric values
* Connected latent widget defaults

If a workflow cannot be repaired safely, the tool will report the problem instead of guessing and breaking the workflow.

---

### Optimize For My GPU

Optimize For My GPU currently supports safe optimization for confirmed Flux / Flux1 / Flux2 style workflows.

It can safely reduce exposed workflow resolution values such as:

```text
1024x1024 -> 768x768
```

when the workflow structure is confirmed safe.

The optimizer avoids dangerous edits and does **not** mutate:

* Seeds
* Prompts
* Model filenames
* CFG values
* Random numeric values
* Unknown node settings
* Connected internal latent defaults

If no safe optimization path is found, the app will show:

```text
No safe optimizations applied.
```

This is expected for unsupported workflows, already optimized workflows, video workflows in v0.5, or workflows where changing values would be unsafe.

The optimized workflow is saved as a separate `_optimized.json` file.

---

### AI Assistant / Chat

The AI Assistant tab is available.

It can help explain workflow analysis results and provide workflow-related guidance.

Depending on your setup, AI Chat may use:

* Local Ollama provider
* OpenAI provider settings

AI Chat is optional.

Without AI Chat setup, the following features still work:

* Workflow Analyzer
* Fix Workflow
* Optimize For My GPU
* Save Report
* Copy Report

---

### Reports

v0.5 includes:

* Save Report
* Copy Report

Reports can be used for:

* Debugging
* Support requests
* Sharing workflow problems
* Comparing optimization results
* Posting analysis logs when asking for help

---

## Video Workflow Support

Video workflows are currently analyzed, not fully auto-optimized yet.

v0.5 can detect and analyze:

* Local video workflows
* Wan video workflows
* API/cloud video workflows
* Seedance-style API workflows
* Reference media used by video workflows
* Basic video width/height/length information when available

Important:

```text
Video workflows are analyzed in v0.5.
Full automatic video optimization is planned for future versions.
```

The optimizer does not yet automatically reduce Wan/Seedance video length, frame count, resolution or advanced video model settings.

---

## Current Limitations

The following features are not fully implemented yet:

* Full video workflow optimization
* Advanced optimizer profiles
* Automatic custom node installation
* Full reconstruction of heavily corrupted workflows
* Exact VRAM benchmarking
* Deep optimizer support for every possible ComfyUI custom workflow
* Advanced reroute/subgraph-boundary tracing

VRAM/RAM estimates are practical warning estimates, not exact benchmarks.

Real memory usage may vary depending on:

* ComfyUI version
* Custom nodes
* Model precision
* Driver version
* Background applications
* Workflow execution order

---

## System Requirements

Recommended:

* Windows 10 / 11
* NVIDIA GPU recommended
* 8GB+ RAM
* 8GB+ VRAM recommended for heavier local workflows
* Internet connection only required for online AI/provider features

The app can still analyze workflows without an internet connection.

---

## Installation

### 1. Download the Release ZIP

Download:

```text
Comfy-OOM-Shield-v0.5-Windows.zip
```

---

### 2. Extract the ZIP

Extract the full folder anywhere you want.

Example:

```text
Desktop\Comfy-OOM-Shield-v0.5-Windows
```

Important:

Do **not** move only the `.exe` file out of the extracted folder.

The app needs the full release folder to run correctly.

---

## Running Comfy-OOM-Shield

Open the extracted folder and run:

```text
Comfy-OOM-Shield.exe
```

If Windows SmartScreen appears, choose:

```text
More info -> Run anyway
```

This can happen because the app is not code-signed yet.

---

## Basic Usage

### Analyze Workflow

1. Open Comfy-OOM-Shield
2. Load or drag-and-drop a ComfyUI workflow `.json`
3. Click Analyze
4. Read the workflow report

---

### Fix Workflow

1. Load a workflow `.json`
2. Click Fix Workflow
3. The app will save a new file:

```text
your_workflow_fixed.json
```

Fix Workflow is designed to be safe. It reports unsafe problems instead of guessing and breaking the workflow.

---

### Optimize For My GPU

1. Load a supported workflow
2. Click Optimize For My GPU
3. The app will save a new file:

```text
your_workflow_optimized.json
```

If the workflow has no confirmed safe optimization path, the app will show:

```text
No safe optimizations applied.
```

This is expected behavior for unsupported workflows or video workflows that are currently analysis-only.

---

### Save / Copy Report

After analysis, you can:

* Save Report
* Copy Report

Use this for bug reports, support, sharing workflow diagnostics, or comparing workflow changes.

---

## AI Chat Setup Optional

AI Chat is optional.

Without AI Chat setup:

* Workflow Analyzer works
* Fix Workflow works
* Optimize For My GPU works
* Save Report works
* Copy Report works

Only AI Chat/provider features may be unavailable.

---

### Local AI Chat with Ollama

Comfy-OOM-Shield includes optional helper `.bat` files for local AI Chat setup.

Inside the release folder you may find:

```text
install_ollama.bat
install_qwen.bat
```

These files are optional.

They are only needed if you want to use local AI Chat with Ollama + Qwen.

Without Ollama/Qwen setup, the main features still work:

* Workflow Analyzer
* Fix Workflow
* Optimize For My GPU
* Save Report
* Copy Report

Only local AI Chat may be unavailable.

---

#### Step 1 - Install Ollama

Run:

```text
install_ollama.bat
```

This opens the Ollama download page.

Install Ollama normally.

After installing Ollama:

* Close all CMD windows
* Reopen CMD if needed

---

#### Step 2 - Install Qwen Model

Run:

```text
install_qwen.bat
```

This downloads and installs the local Qwen model used for AI Chat.

The download may take several minutes depending on your internet speed.

---

#### Step 3 - Start AI Chat

1. Launch Comfy-OOM-Shield
2. Open the Chat tab
3. Select the local/Ollama provider if available
4. Send a message

If AI Chat does not respond, check that Ollama is running:

```text
http://localhost:11434
```

---

### OpenAI Provider

OpenAI provider support is available through the app settings.

You may need to provide your own OpenAI API key.

Important:

* Your API key is your responsibility
* Do not share your config file publicly
* OpenAI usage may require paid API credits
* If OpenAI fails, Analyzer/Fix/Optimizer can still work without it

---

## Common Problems

### The app does not start

Make sure you are running the `.exe` from inside the extracted release folder.

Do not move the `.exe` alone.

---

### Windows blocks the app

Windows SmartScreen may appear because the app is not code-signed yet.

Use:

```text
More info -> Run anyway
```

---

### AI Chat does not respond

If using Ollama, check:

```text
http://localhost:11434
```

Ollama may not be running.

Try restarting Ollama and launching the app again.

---

### "ollama is not recognized"

Ollama is not installed or not available in PATH.

Fix:

1. Install Ollama
2. Restart CMD
3. Try again

---

### GPU shows as Unknown GPU

Some GPUs may not be detected correctly.

This does not stop workflow analysis.

---

### No safe optimizations applied

This is not always an error.

It means the optimizer did not find a confirmed safe mutation path.

This is expected for:

* Unsupported workflows
* Many custom workflows
* Video workflows in v0.5
* Workflows already optimized
* Workflows where changing values would be unsafe

---

## Recommended Use

Use Comfy-OOM-Shield v0.5 to:

* Check if a ComfyUI workflow is too heavy for your GPU
* Detect local models
* Detect reference media
* Detect local/API video workflows
* Estimate VRAM/RAM/SSD swap risk
* Safely repair simple broken JSON workflow files
* Safely optimize supported Flux/Flux-style workflows
* Save or copy workflow reports

---

## Not Recommended Yet

Do not expect v0.5 to:

* Automatically optimize every video workflow
* Fully repair heavily corrupted workflows
* Install every missing custom node automatically
* Guarantee exact VRAM usage
* Replace manual ComfyUI debugging completely

---

## Typical Release Folder

```text
Comfy-OOM-Shield-v0.5-Windows/
│
├── Comfy-OOM-Shield.exe
├── install_ollama.bat
├── install_qwen.bat
├── tools/
├── agents/
├── memory/
└── automation/
```

Some files may vary depending on the release build.

---

## Disclaimer

This software is provided as-is for educational and workflow assistance purposes.

Always keep backups of important workflows before editing or optimizing them.

Comfy-OOM-Shield saves fixed and optimized files as separate JSON files, but manual backups are still recommended.
