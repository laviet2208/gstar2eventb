# gStar2EventB

This repository contains the tool-support artifacts used to support the paper:

**A Formal Semantic Framework for Goal-Oriented Requirements Modeling**

Repository URL:  
https://github.com/laviet2208/gstar2eventb

---

## Table of Contents

- [1. Overview](#1-overview)
- [2. Installation and Environment Setup](#2-installation-and-environment-setup)
- [3. Importing the Repository into Eclipse](#3-importing-the-repository-into-eclipse)
- [4. Registering the Metamodels](#4-registering-the-metamodels)
- [5. Running the ATL Transformation](#5-running-the-atl-transformation)
- [6. Running the Acceleo Generators](#6-running-the-acceleo-generators)
- [7. Checking the Generated Artifacts](#7-checking-the-generated-artifacts)
- [8. Reproducing the Case Studies](#8-reproducing-the-case-studies)
- [9. Troubleshooting](#9-troubleshooting)

## 1. Overview

`gStar2EventB` implements a model-driven toolchain for deriving formal artifacts from gStar requirements models.

The toolchain takes as input a gStar model conforming to `gstar.ecore` and produces formal artifacts through two main steps:

1. **Model-to-model transformation with ATL**  
   A gStar model is transformed into an Event-B-oriented target model conforming to `eventb.ecore`.

2. **Model-to-text generation with Acceleo**  
   The generated target model and the temporal-requirement constructs of the gStar model are used to generate textual Event-B artifacts and LTL-based temporal artifacts.

The repository currently includes:

- the source gStar metamodel;
- the target Event-B-oriented metamodel;
- ATL transformation modules;
- Acceleo generation templates;
- the Mine Pump case-study model;
- the MeetingScheduler case-study model.

The generated artifacts can be used to support the formal analysis described in the paper, including state-based and behavioral analysis in Event-B and temporal-property analysis using LTL-based specifications.

---

## 2. Installation and Environment Setup

This section describes the software required to run the transformation and generation process.

---

### 2.1 Eclipse Modeling Tools

**Purpose.**  
Eclipse Modeling Tools is used as the main environment for opening metamodels, managing models, running ATL transformations, and executing Acceleo generators.

**Download.**  
Install Eclipse Modeling Tools from:

https://www.eclipse.org/downloads/packages/

**Recommended package.**

- Eclipse Modeling Tools; or
- Eclipse IDE for Java and DSL Developers.

**Expected result.**  
After installation, Eclipse should be able to open `.ecore` files and XMI-based models.

---

### 2.2 Eclipse Modeling Framework

**Purpose.**  
EMF is required to open, inspect, and register the `gstar.ecore` and `eventb.ecore` metamodels.

**Installation steps.**

1. Open Eclipse.
2. Go to **Help > Eclipse Marketplace**.
3. Search for **EMF - Eclipse Modeling Framework**.
4. Install the required EMF components.
5. Restart Eclipse.

**Expected result.**  
Eclipse can open `.ecore` files using the EMF Ecore editor.

---

### 2.3 ATL Transformation Language

**Purpose.**  
ATL is used to execute the model-to-model transformation from gStar to the Event-B-oriented target model.

**Installation steps.**

1. Open Eclipse.
2. Go to **Help > Eclipse Marketplace**.
3. Search for **ATL Transformation Language**.
4. Install ATL.
5. Restart Eclipse.

**Expected result.**  
Eclipse provides an **ATL Transformation** run configuration.

---

### 2.4 Acceleo

**Purpose.**  
Acceleo is used to perform model-to-text generation. In this repository, it is used to generate textual Event-B artifacts and LTL-based temporal artifacts.

**Installation steps.**

1. Open Eclipse.
2. Go to **Help > Eclipse Marketplace**.
3. Search for **Acceleo**.
4. Install Acceleo.
5. Restart Eclipse.

**Expected result.**  
Eclipse provides an **Acceleo Application** run configuration and can execute `.mtl` generation modules.

---

## 3. Importing the Repository into Eclipse

This section explains how to import the repository after cloning or downloading it.

---

### 3.1 Clone the Repository

Run:

```bash
git clone https://github.com/laviet2208/gstar2eventb.git
cd gstar2eventb
```

Alternatively, download the repository as a ZIP file from GitHub and extract it locally.

---

### 3.2 Import as an Eclipse Project

**Steps.**

1. Open Eclipse Modeling Tools.
2. Select or create a workspace.
3. Go to **File > Import**.
4. Select **General > Existing Projects into Workspace**.
5. Click **Next**.
6. Select the local `gstar2eventb` folder.
7. Select the available project.
8. Click **Finish**.

**Expected result.**  
The repository contents appear in the **Project Explorer**.

---

### 3.3 Import as a General Folder

Use this option if Eclipse does not recognize the repository as an Eclipse project.

**Steps.**

1. Create a new general project in Eclipse.
2. Right-click the project.
3. Select **Import > General > File System**.
4. Select the local `gstar2eventb` folder.
5. Import all files into the project.

---

## 4. Registering the Metamodels

The toolchain requires two metamodels:

```text
metamodels/gstar.ecore
metamodels/eventb.ecore
```

---

### 4.1 Open the Metamodels

**Steps.**

1. Open `metamodels/gstar.ecore`.
2. Check that the Ecore model loads correctly.
3. Open `metamodels/eventb.ecore`.
4. Check that the Ecore model loads correctly.

---

### 4.2 Register the EPackages

If Eclipse, ATL, or Acceleo cannot resolve the metamodels, register the EPackages manually.

**Steps.**

1. Open the `.ecore` file.
2. Right-click the root package.
3. Select **Register EPackages** if available.
4. Repeat this step for both `gstar.ecore` and `eventb.ecore`.

**Common issue.**  
The menu name may vary depending on the Eclipse and EMF versions.

---

### 4.3 Check Metamodel URIs

If the ATL transformation or Acceleo generation reports that a metamodel cannot be found, check that the metamodel URIs match across:

- the `.ecore` file;
- the input model;
- the ATL run configuration;
- the Acceleo run configuration.

A URI mismatch is one of the most common causes of execution errors in EMF-based toolchains.

---

## 5. Running the ATL Transformation

This section explains how to run the model-to-model transformation from gStar to the Event-B-oriented target model.

---

### 5.1 Create an ATL Run Configuration

**Steps.**

1. Open Eclipse.
2. Go to **Run > Run Configurations**.
3. Select **ATL Transformation**.
4. Click **New Configuration**.
5. Name the configuration, for example:

```text
gStar2EventB - MeetingScheduler
```

or:

```text
gStar2EventB - MinePump
```

---

### 5.2 Select the ATL Module

Select the main ATL transformation file:

```text
transformations/gstar2eventb.atl
```

Make sure the helper module is also available:

```text
transformations/helpers.atl
```

If `gstar2eventb.atl` imports `helpers.atl`, the helper module must be reachable from the ATL execution environment.

---

### 5.3 Configure the Source Model

Choose one of the provided input models.

For Mine Pump:

```text
case-studies/mine-pump/minepump.gstar
```

For MeetingScheduler:

```text
case-studies/meeting-scheduler/meetingscheduler.gstar
```

---

### 5.4 Configure the Metamodels

**Source metamodel.**

```text
metamodels/gstar.ecore
```

**Target metamodel.**

```text
metamodels/eventb.ecore
```

Make sure that the ATL model aliases match those used in the ATL file.

For example, if the ATL file uses:

```atl
GSR!Model
EB!Machine
```

then the source and target metamodels must be configured using the corresponding ATL model names.

---

### 5.5 Configure the Output Model

Choose an output path for the generated Event-B-oriented target model.

Example for Mine Pump:

```text
case-studies/mine-pump/minepump-eventb.xmi
```

Example for MeetingScheduler:

```text
case-studies/meeting-scheduler/meetingscheduler-eventb.xmi
```

The output file name can be changed if needed, but it should clearly indicate the case study and the generated target model.

---

### 5.6 Run the Transformation

Click **Run**.

**Expected result.**

After the transformation finishes, the output model should be generated successfully.

Check that:

- the output file exists;
- the ATL console does not report runtime errors;
- the generated model conforms to `eventb.ecore`;
- the generated model contains Event-B-oriented elements such as contexts, machines, variables, invariants, events, guards, and actions.

---

## 6. Running the Acceleo Generators

This section explains how to generate textual artifacts using Acceleo after the ATL transformation has produced the Event-B-oriented target model.

The repository includes Acceleo templates for generating:

1. textual Event-B artifacts; and
2. LTL-based temporal artifacts.

---

### 6.1 Generate Event-B Textual Artifacts

**Purpose.**  
This step generates textual Event-B artifacts from the Event-B-oriented target model produced by the ATL transformation.

**Input.**

Use the Event-B-oriented model generated in Section 5.

Example:

```text
case-studies/meeting-scheduler/meetingscheduler-eventb.xmi
```

or:

```text
case-studies/mine-pump/minepump-eventb.xmi
```

**Steps.**

1. Open Eclipse.
2. Go to **Run > Run Configurations**.
3. Select **Acceleo Application**.
4. Click **New Configuration**.
5. Select the main Acceleo module for Event-B generation.
6. Select the generated Event-B-oriented model as the input model.
7. Select an output folder for the generated Event-B textual artifacts.
8. Click **Run**.

**Expected result.**

The generator should produce textual Event-B artifacts, such as:

- context-level declarations;
- machine-level declarations;
- variables;
- invariants;
- events;
- guards;
- actions;
- axioms or assumptions where applicable.

---

### 6.2 Generate LTL-Based Temporal Artifacts

**Purpose.**  
This step generates LTL-based temporal artifacts from the temporal-requirement constructs of the gStar model.

**Input.**

Use the original gStar model containing temporal-requirement constructs.

For MeetingScheduler:

```text
case-studies/meeting-scheduler/meetingscheduler.gstar
```

**Steps.**

1. Open Eclipse.
2. Go to **Run > Run Configurations**.
3. Select **Acceleo Application**.
4. Click **New Configuration**.
5. Select the main Acceleo module for LTL or temporal-artifact generation.
6. Select the gStar model as the input model.
7. Select an output folder for the generated temporal artifacts.
8. Click **Run**.

**Expected result.**

The generator should produce LTL-based temporal artifacts, such as:

- atomic propositions derived from temporal variables;
- eventuality formulae;
- response formulae;
- ordering formulae;
- invariance formulae;
- assumption-style temporal formulae;
- traceability information where supported.

---

### 6.3 Recommended Output Locations

The generated files may be stored under the corresponding case-study folders.

Example for Mine Pump:

```text
case-studies/mine-pump/generated-eventb/
```

Example for MeetingScheduler:

```text
case-studies/meeting-scheduler/generated-eventb/
case-studies/meeting-scheduler/generated-ltl/
```

If these folders do not exist, create them manually before running the Acceleo generators.

---

## 7. Checking the Generated Artifacts

After running ATL and Acceleo, inspect the generated outputs.

---

### 7.1 Check the Generated Event-B-Oriented Model

Open the generated target model in Eclipse and inspect whether it contains:

- an Event-B project representation;
- an Event-B context;
- an Event-B machine;
- variables;
- invariants;
- events;
- guards;
- actions;
- axioms or domain assumptions where applicable.

For the Mine Pump case study, the generated model should include Event-B-oriented representations of safety goals and pump-control operations.

For the MeetingScheduler case study, the generated model should include Event-B-oriented representations of scheduling milestones, operations, assumptions, obstacles, and related behavioral structures.

---

### 7.2 Check the Generated Event-B Textual Artifacts

Inspect the generated Event-B files and check whether they contain:

- context declarations;
- machine declarations;
- typing information;
- invariants;
- events;
- guards;
- actions;
- assumptions or axioms where applicable.

The generated Event-B artifacts should reflect the state-based and behavioral interpretation of the input gStar model.

---

### 7.3 Check the Generated Temporal Artifacts

Inspect the generated temporal files and check whether they contain LTL-based formulae corresponding to the temporal requirements in the gStar model.

For MeetingScheduler, expected temporal artifacts may include properties such as:

```text
G(requestReceived -> F(scheduled))
```

This formula expresses a response-style requirement: whenever a request is received, the system should eventually reach a scheduled state.

---

## 8. Reproducing the Case Studies

This section summarizes the steps required to reproduce the outputs for the two case studies.

---

### 8.1 Mine Pump

To reproduce the Mine Pump transformation and generation result:

1. Import the repository into Eclipse.
2. Register `gstar.ecore` and `eventb.ecore`.
3. Create an ATL run configuration.
4. Select:

```text
transformations/gstar2eventb.atl
```

5. Use the following source model:

```text
case-studies/mine-pump/minepump.gstar
```

6. Use `gstar.ecore` as the source metamodel.
7. Use `eventb.ecore` as the target metamodel.
8. Choose an output path, for example:

```text
case-studies/mine-pump/minepump-eventb.xmi
```

9. Run the ATL transformation.
10. Run the Acceleo Event-B generator using the generated target model.
11. Inspect the generated Event-B textual artifacts.

---

### 8.2 MeetingScheduler

To reproduce the MeetingScheduler transformation and generation result:

1. Import the repository into Eclipse.
2. Register `gstar.ecore` and `eventb.ecore`.
3. Create an ATL run configuration.
4. Select:

```text
transformations/gstar2eventb.atl
```

5. Use the following source model:

```text
case-studies/meeting-scheduler/meetingscheduler.gstar
```

6. Use `gstar.ecore` as the source metamodel.
7. Use `eventb.ecore` as the target metamodel.
8. Choose an output path, for example:

```text
case-studies/meeting-scheduler/meetingscheduler-eventb.xmi
```

9. Run the ATL transformation.
10. Run the Acceleo Event-B generator using the generated target model.
11. Run the Acceleo temporal generator using the original gStar model.
12. Inspect the generated Event-B textual artifacts and LTL-based temporal artifacts.

---

## 9. Troubleshooting

---

### 9.1 Eclipse Does Not Recognize the Repository as a Project

If Eclipse does not detect the repository as an existing project, create a new general project and import the repository files manually through:

```text
File > Import > General > File System
```

---

### 9.2 The gStar Model Cannot Be Opened

Check that:

- the `.gstar` file exists;
- the model is a valid XMI-based model;
- `gstar.ecore` is available in the workspace;
- the metamodel URI in the model matches the URI of `gstar.ecore`;
- there are no unresolved references.

---

### 9.3 ATL Cannot Find the Source or Target Metamodel

Check that:

- `gstar.ecore` and `eventb.ecore` are imported into the workspace;
- both metamodels are registered;
- the ATL configuration uses the correct metamodel aliases;
- the metamodel URIs match those declared in the `.ecore` files.

---

### 9.4 ATL Cannot Find `helpers.atl`

Check that:

- `helpers.atl` is located in the `transformations/` folder;
- the import path in `gstar2eventb.atl` is correct;
- the Eclipse project has been refreshed.

To refresh the project, right-click the project and select **Refresh**.

---

### 9.5 The ATL Transformation Produces an Empty Model

Check that:

- the input model contains the expected gStar elements;
- the ATL rules match the class names in `gstar.ecore`;
- rule guards are not too restrictive;
- the input model conforms to the expected version of the metamodel.

---

### 9.6 The Generated Target Model Cannot Be Opened

Check that:

- the output model was generated completely;
- the output model conforms to `eventb.ecore`;
- the target metamodel is registered;
- the output file was not partially written because of a transformation error.

---

### 9.7 Acceleo Does Not Produce Output Files

Check that:

- the Acceleo plugin is installed correctly;
- the correct Acceleo main module is selected;
- the input model is the expected model type;
- the output directory exists or can be created;
- the required metamodels are registered;
- the generator has permission to write to the selected output folder.

---

### 9.8 The Generated Event-B Text Is Incomplete

Check that:

- the ATL transformation produced the expected target model;
- the generated target model contains contexts, machines, variables, invariants, events, guards, and actions;
- the Acceleo templates match the structure of `eventb.ecore`;
- the input model passed to the Acceleo generator is the Event-B-oriented target model, not the original gStar model.

---

### 9.9 The Generated Temporal Artifacts Are Missing

Check that:

- the selected gStar model contains temporal-requirement constructs;
- `TemporalVariable`, `TemporalRequirement`, and `TemporalLink` elements are present where expected;
- the Acceleo temporal generator is executed on the original gStar model;
- the output folder is correctly configured;
- the generator templates match the current version of `gstar.ecore`.

---
## 12. Contact

For questions about the transformation artifacts, generation templates, or case-study models, please open an issue in this repository.
