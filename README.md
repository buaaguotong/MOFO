# Multiobjective Autoformulation Benchmark (MAB)

A novel, structurally decoupled benchmark designed specifically for evaluating the Multiobjective Autoformulation capabilities of Agentic AI in Operations Research and Combinatorial Optimization.

## Overview

While existing OR benchmarks evaluate Large Language Models primarily as code translators focusing on single-objective code correctness, real-world combinatorial optimization involves strict trade-offs among solving time, memory footprint, and solution quality. 

This benchmark shifts the evaluation paradigm. It tests whether an Agentic AI can act as a sophisticated OR consultant: penetrating diverse, out-of-domain industrial narratives, understanding explicit computational preferences, and generating a Pareto-optimal portfolio of mathematical models.

## Key Features

* **Semantic Decoupling**: Mathematical parameters are entirely separated from the problem narratives. Isomorphic graph structures are disguised under highly diverse contexts such as VLSI laser drilling, disaster relief drone routing, and space exploration. This strictly tests domain generalization.
* **Preference-Aware Alignment**: Each instance includes a `user_preference` instruction. The AI must adapt its mathematical formulation choice based on specified operational boundaries, such as strict memory limits on edge devices or absolute cost minimization on server clusters.
* **Multiobjective Evaluation Ready**: Built upon classic academic instances, every JSON file incorporates mathematically proven Best Known Solutions (BKS). This provides an absolute ground truth for calculating multiobjective evolutionary metrics like Inverted Generational Distance (IGD) and Hypervolume (HV).

## Supported Problem Categories

The repository is organized into four core routing problem variants of increasing complexity:

1.  **TSP** (Traveling Salesman Problem): Sourced from TSPLIB.
2.  **CVRP** (Capacitated Vehicle Routing Problem): Sourced from classic sets like Augerat (A, B), Christofides (E, M), and Fisher (F).
3.  **MDVRP** (Multi-Depot Vehicle Routing Problem): Sourced from Cordeau instances, testing simultaneous assignment and routing.
4.  **VRPTW** (Vehicle Routing Problem with Time Windows): Sourced from Solomon instances (C, R, RC classes), testing soft/hard constraint handling.

## Directory Structure

After running the initialization script, the repository follows a clean, machine-readable hierarchy:

```text
000-benchmark/
├── 1-TSP/
│   ├── raw_instances/       # Original .tsp files
│   └── json_benchmarks/     # Agentic AI ready JSON files
├── 2-CVRP/
│   ├── raw_instances/       # Original .vrp files
│   └── json_benchmarks/     # Agentic AI ready JSON files
├── 3-MDVRP/
│   ├── raw_instances/       # Original .txt files
│   └── json_benchmarks/     # Agentic AI ready JSON files
└── 4-VRPTW/
    ├── raw_instances/       # Original .txt files
    └── json_benchmarks/     # Agentic AI ready JSON files
```

## Data Structure Example

Each JSON instance is heavily structured to facilitate automated Agentic workflows. Key fields include:

- **instance_id**: Unique identifier mapping to the base raw data.
- **domain**: The applied physical or industrial scenario.
- **nlp_description**: A synthesized natural language prompt without explicit academic OR terminology.
- **user_preference**: The computational constraints governing formulation selection.
- **data_attachment**: Structured tensors containing nodes, demands, vehicle capacities, and distance metrics.
- **ground_truth**: The absolute optimal objective value for MIPGap calculation and references to expert formulations.

## Usage

You can load these instances directly into your multi-agent evaluation sandbox using Python:

Python

```
import json

with open('000-benchmark/2-CVRP/json_benchmarks/cvrp_diverse_contexts.json', 'r') as file:
    benchmark_data = json.load(file)

for instance in benchmark_data:
    prompt = instance['nlp_description']
    preference = instance['user_preference']
    # Pass prompt and preference to your Agentic Formulator
```

