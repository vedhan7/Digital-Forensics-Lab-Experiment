# Ex. No. 10: Static Binary Analysis Using Ghidra

**Course / Lab:** Digital Forensics Laboratory  
**Experiment:** Static Binary Analysis Using Ghidra  
**Status:** Procedure and analysis record

---

## Overview

Ghidra is a software reverse-engineering platform for analysing compiled code without executing it. This experiment focuses on safe static analysis of an authorised, benign training binary inside an isolated lab environment. The objective is to identify functions, strings, imports, and control flow, then distinguish observed facts from analyst hypotheses.

## Safety Rules

- Use an isolated virtual machine or analysis network.
- Do not execute the sample to obtain a screenshot or test a hypothesis.
- Use only instructor-provided, benign training samples.
- Record the sample SHA-256 value before importing it into a project.

## Objectives

1. Create a non-shared Ghidra project and import a controlled sample.
2. Run auto-analysis and inspect the CodeBrowser panels.
3. Review strings, imports, cross-references, and a selected function graph.
4. Report observations separately from conclusions and preserve indicators of compromise only when supported.

## Tools Required

- [Ghidra](https://ghidra-sre.org/)
- JDK compatible with the chosen Ghidra release
- An isolated analysis VM
- An instructor-approved, benign sample binary

## Step 1: Preserve and import the sample

Create a case folder and calculate the file hash before analysis. Create a **Non-Shared Project**, then use **File → Import File**. Verify that Ghidra's detected format, processor, language, and compiler match the sample's known characteristics.

```bash
sha256sum training-sample.exe
```

## Step 2: Run auto-analysis in CodeBrowser

Accept the appropriate auto-analysis options and open the program in CodeBrowser. The Program Tree and Symbol Tree aid navigation; the Listing shows machine instructions and references; the Decompiler presents C-like pseudocode for the current function.

![Real Ghidra CodeBrowser with listing and decompiler panels](https://dl.flathub.org/repo/screenshots/org.ghidra_sre.Ghidra-stable/1248x702/org.ghidra_sre.Ghidra-95e44eab06b8e4b15706f1c538f1c46c.png)

*Figure 10.1: A real Ghidra CodeBrowser view showing the symbol tree, disassembly listing, and decompiler output for a selected function.*

## Step 3: Build observations from multiple views

| View | What to record | Caution |
| --- | --- | --- |
| Defined Strings | URLs, paths, registry names, encoded strings | A string can be unused or benign |
| Import table | APIs and imported libraries | An import does not prove a call is reached |
| Cross-references | Callers, references, data flow | Validate direction and context |
| Function graph | Branches, loops, and control flow | Decompiler labels are analyst aids, not ground truth |
| Decompiler | Pseudocode and likely parameters | Confirm key conclusions in the assembly listing |

## Step 4: Write the analysis record

For every finding, record the file hash, Ghidra version, program address, evidence view, and interpretation. Example phrasing: *"The binary imports `RegSetValueEx`; further control-flow review is required to determine whether it is used for persistence."* This avoids treating a possible capability as proven behaviour.

## Result

The static-analysis procedure produces a repeatable record of observed code artefacts, their addresses, and the analyst's supported interpretations without executing the sample.

## Visual source

Figure 10.1 is the published Ghidra application screenshot from [Flathub](https://flathub.org/apps/org.ghidra_sre.Ghidra). It is a genuine interface reference and not a result from the lab sample.
