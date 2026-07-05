# Comfy-OOM-Shield v1.0-dev

**Comfy-OOM-Shield** is a desktop application for analyzing, repairing, and safely optimizing ComfyUI workflow files.

It helps users understand why a workflow may overload the GPU, fail to open, contain broken links, or require too much VRAM, RAM, or SSD swap.

> Current version: **v1.0-dev**  
> Status: Active development  
> Platform: Windows

## Features

### Workflow Analyzer

The Analyzer inspects ComfyUI workflow files and generates a detailed report.

It can:

- detect the workflow type;
- parse standard nodes and subgraphs;
- identify heavy models and nodes;
- detect resolution, batch size, sampler steps, and other known values;
- estimate VRAM, RAM, and SSD swap usage;
- calculate Workflow Health;
- calculate GPU Compatibility;
- calculate VRAM Safety;
- assign an overall risk level;
- generate recommendations for the detected GPU.

The Analyzer does not modify the original workflow.

### Workflow Fixer

The Fixer repairs confirmed JSON and workflow structure problems.

It can:

- remove trailing commas from JSON;
- trim garbage after the valid JSON document;
- validate nodes, inputs, outputs, and links;
- detect links that reference missing nodes;
- detect missing root links;
- detect links connected to the wrong target input;
- safely repair confirmed numeric parameters;
- preserve the original workflow;
- create a separate `_fixed.json` file;
- report repaired and unrepaired issues separately.

The Fixer does not create random nodes or guess ambiguous broken connections.

### Safe Workflow Optimizer

The Optimizer uses conservative safety rules.

It can:

- analyze the workflow for the detected GPU;
- detect high sampler step counts;
- detect large resolutions;
- detect large batch sizes;
- detect heavy models;
- list optimization candidates;
- apply only confirmed safe changes;
- preserve seed values;
- preserve prompts;
- preserve model filenames;
- preserve CFG;
- preserve sampler and scheduler values;
- preserve unknown numeric values;
- avoid creating an output file when no safe change is available;
- save optimized results as `_optimized.json`.

### Optimizer Profiles

Available profiles:

- **SAFE** — minimal changes with maximum workflow preservation;
- **BALANCED** — a compromise between quality and resource usage;
- **AGGRESSIVE** — stronger reductions for lower-end GPUs.

Some advanced BALANCED and AGGRESSIVE rules are still under development.

### AI Chat

The built-in AI assistant can help explain:

- workflow errors;
- Analyzer reports;
- VRAM problems;
- GPU compatibility issues;
- Fixer warnings;
- Optimizer candidates;
- ComfyUI workflow structure.

### Models

The Models section helps inspect:

- checkpoints;
- UNet models;
- CLIP models;
- VAE models;
- heavy model configurations;
- compatibility with available VRAM;
- possible lighter or FP8 alternatives.

The application does not silently replace model filenames.

### Custom Nodes

The Custom Nodes section can:

- detect custom node types;
- identify unknown or missing nodes;
- help explain why a workflow cannot be opened or executed;
- provide hints for finding required extensions.

### Batch Processing

The Batch section supports processing multiple workflow files.

Supported operations include:

- batch analysis;
- batch repair;
- batch optimization;
- separate reports for each file;
- preservation of original files.

### Backups / Recovery

The Backups / Recovery section provides access to:

- original workflow files;
- fixed workflow versions;
- optimized workflow versions;
- recovery files;
- generated outputs.

### Logs

The Logs section records:

- JSON loading errors;
- JSON recovery events;
- Fixer operations;
- Optimizer operations;
- generated output paths;
- unresolved JSON paths;
- application diagnostics.

### Diagnostics

The Diagnostics section checks:

- GPU model;
- VRAM;
- RAM;
- CPU;
- application paths;
- runtime dependencies;
- basic environment health.

## How to Run

1. Extract the ZIP archive into a separate folder.
2. Do not delete or move files located next to the executable.
3. Run:

```text
Comfy-OOM-Shield.exe
```

The standalone build requires all files inside the application folder.

## Quick Start

1. Open the **Analyzer** tab.
2. Click **Open Workflow**.
3. Select a ComfyUI workflow JSON file.
4. Click **Analyze Workflow**.
5. Review:
   - Workflow Health;
   - GPU Compatibility;
   - VRAM Safety;
   - Risk Level;
   - recommendations.
6. Use **Fix Workflow** for damaged workflow files.
7. Use **Optimize For My GPU** for safe optimization.

## Output Files

Original workflow:

```text
workflow.json
```

Fixed workflow:

```text
workflow_fixed.json
```

Optimized workflow:

```text
workflow_optimized.json
```

The original workflow is not overwritten.

## Safety Rules

Comfy-OOM-Shield does not automatically modify:

- seeds;
- prompts;
- model filenames;
- CFG values;
- sampler selection;
- scheduler selection;
- unknown numeric values.

A value is modified only when the application can identify the node type, widget position, and safe rule with confidence.

## Important Limitation

Comfy-OOM-Shield does not guarantee that every repaired workflow will immediately run in ComfyUI.

Manual correction may still be required when:

- custom nodes are missing;
- models are missing;
- external files are missing;
- broken links are ambiguous;
- the workflow uses an unknown or non-standard structure.

In these cases, the application reports the unresolved problem instead of making an unsafe guess.

## Current Status

Working modules:

- Workflow Analyzer;
- GPU Compatibility Analysis;
- VRAM / RAM / SSD Estimator;
- Workflow Type Detection;
- Heavy Node Detection;
- Subgraph Parsing;
- Workflow Fixer;
- JSON Recovery;
- Safe Optimizer;
- AI Chat;
- Optimizer Profiles;
- Models;
- Custom Nodes;
- Batch Processing;
- Backups / Recovery;
- Logs;
- Diagnostics.

In development:

- Optimizer v2;
- additional node-specific optimization rules;
- improved video workflow detection;
- expanded model compatibility data;
- more accurate VRAM estimation;
- additional safe structural repairs.

## Project Goal

Comfy-OOM-Shield is designed for ComfyUI users who need to:

- inspect workflows before running them;
- understand VRAM overflow risks;
- recover damaged JSON files;
- detect broken links and missing nodes;
- receive recommendations for lower-end and mid-range GPUs;
- preserve the original workflow without accidental overwrites.

**Comfy-OOM-Shield v1.0-dev** is a development build.  
Keep a backup of important workflow files before making changes.
