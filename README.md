# gStar2EventB

This repository contains the tool-support and experimental artifacts for the paper:

**A Formal Semantic Framework for Goal-Oriented Requirements Modeling**

The repository provides the metamodels, transformation rules, code-generation templates, case-study models, generated formal artifacts, and experimental results used to support the evaluation reported in the paper.

## 1. Overview

`gStar2EventB` implements a model-driven engineering process for deriving formal artifacts from gStar requirements models.

The toolchain takes as input a gStar model and produces two groups of formal artifacts:

1. **Event-B artifacts**  
   These artifacts represent the state-based and behavioral interpretation of the gStar model. They include Event-B contexts, machines, variables, invariants, events, guards, and actions.

2. **Temporal artifacts**  
   These artifacts represent temporal requirements specified in gStar as LTL-based formulae and related temporal specifications.

The generated Event-B artifacts can be analyzed using Rodin and ProB. The generated temporal formulae can be checked using ProB or other compatible LTL analysis tools.

## 2. Repository Structure

```text
gstar2eventb/
├── README.md
├── LICENSE
├── metamodels/
│   ├── gstar.ecore
│   └── eventb.ecore
├── transformations/
│   └── atl/
│       └── gstar2eventb.atl
├── generators/
│   └── acceleo/
│       ├── eventb/
│       └── ltl/
├── case-studies/
│   ├── mine-pump/
│   │   ├── model/
│   │   ├── generated-eventb/
│   │   └── results/
│   └── meeting-scheduler/
│       ├── model/
│       ├── generated-eventb/
│       ├── generated-ltl/
│       └── results/
├── experiments/
│   ├── rq1-construct-coverage/
│   └── rq2-formal-analysis/
└── docs/
    ├── installation.md
    ├── running-transformations.md
    └── reproducing-experiments.md
