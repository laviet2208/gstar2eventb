# gStar2EventB

This repository contains the model-transformation artifacts used to support the paper:

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
- [6. Checking the Generated Target Model](#6-checking-the-generated-target-model)
- [7. Reproducing the Case Studies](#7-reproducing-the-case-studies)
- [8. Troubleshooting](#8-troubleshooting)
  
---

## 1. Overview

`gStar2EventB` implements a model-to-model transformation from gStar requirements models to Event-B-oriented models.

The transformation takes as input a gStar model conforming to `gstar.ecore` and produces a target model conforming to `eventb.ecore`.

The repository currently includes:

- the source gStar metamodel;
- the target Event-B-oriented metamodel;
- ATL transformation modules;
- the Mine Pump case-study model;
- the MeetingScheduler case-study model.

---

## 2. Installation and Environment Setup

This section describes the software required to run the transformation.

### 2.1 Eclipse Modeling Tools

**Purpose.**  
Eclipse Modeling Tools is used as the main environment for opening metamodels, managing models, and running the ATL transformation.

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

## 3. Importing the Repository into Eclipse

This section explains how to import the repository after cloning or downloading it.

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

The transformation requires two metamodels:

```text
metamodels/gstar.ecore
metamodels/eventb.ecore
```

### 4.1 Open the Metamodels

**Steps.**

1. Open `metamodels/gstar.ecore`.
2. Check that the Ecore model loads correctly.
3. Open `metamodels/eventb.ecore`.
4. Check that the Ecore model loads correctly.

---

### 4.2 Register the EPackages

If Eclipse or ATL cannot resolve the metamodels, register the EPackages manually.

**Steps.**

1. Open the `.ecore` file.
2. Right-click the root package.
3. Select **Register EPackages** if available.
4. Repeat this step for both `gstar.ecore` and `eventb.ecore`.

**Common issue.**  
The menu name may vary depending on the Eclipse and EMF versions.

---

## 5. Running the ATL Transformation

This section explains how to run the transformation from gStar to the Event-B-oriented target model.

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

Choose an output path for the generated target model.

Example for Mine Pump:

```text
case-studies/mine-pump/minepump-eventb.xmi
```

Example for MeetingScheduler:

```text
case-studies/meeting-scheduler/meetingscheduler-eventb.xmi
```

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

## 6. Checking the Generated Target Model

Open the generated target model in Eclipse and inspect its contents.

Expected elements include:

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

## 7. Reproducing the Case Studies

### 7.1 Mine Pump

To reproduce the Mine Pump transformation result:

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

9. Run the transformation.
10. Inspect the generated Event-B-oriented model.

---

### 7.2 MeetingScheduler

To reproduce the MeetingScheduler transformation result:

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

9. Run the transformation.
10. Inspect the generated Event-B-oriented model.

---

## 8. Troubleshooting

### 8.1 Eclipse Does Not Recognize the Repository as a Project

If Eclipse does not detect the repository as an existing project, create a new general project and import the repository files manually through:

```text
File > Import > General > File System
```

---

### 8.2 The gStar Model Cannot Be Opened

Check that:

- the `.gstar` file exists;
- the model is a valid XMI-based model;
- `gstar.ecore` is available in the workspace;
- the metamodel URI in the model matches the URI of `gstar.ecore`;
- there are no unresolved references.

---

### 8.3 ATL Cannot Find the Source or Target Metamodel

Check that:

- `gstar.ecore` and `eventb.ecore` are imported into the workspace;
- both metamodels are registered;
- the ATL configuration uses the correct metamodel aliases;
- the metamodel URIs match those declared in the `.ecore` files.

---

### 8.4 ATL Cannot Find `helpers.atl`

Check that:

- `helpers.atl` is located in the `transformations/` folder;
- the import path in `gstar2eventb.atl` is correct;
- the Eclipse project has been refreshed.

To refresh the project, right-click the project and select **Refresh**.

---

### 8.5 The Transformation Produces an Empty Model

Check that:

- the input model contains the expected gStar elements;
- the ATL rules match the class names in `gstar.ecore`;
- rule guards are not too restrictive;
- the input model conforms to the expected version of the metamodel.

---

### 8.6 The Generated Model Cannot Be Opened

Check that:

- the output model was generated completely;
- the output model conforms to `eventb.ecore`;
- the target metamodel is registered;
- the output file was not partially written because of a transformation error.
