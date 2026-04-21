# ClearNote — Meeting Transcript Analyzer

**BUS 670 | Strategic AI for Modern Business | Spring 2026**
**Student:** Kysha Beach
**Instructor:** Ray Bryant

---

## What This Is

ClearNote is an AI-powered meeting transcript analyzer built using Claude Code for the BUS 670 Capstone project. Target user: small business owners and founders (5–50 employees) who run their own meetings without a dedicated notetaker. A user pastes in a raw transcript, and the tool returns a structured one-page brief covering summary, decisions made, action items with owners and deadlines, open questions, and risks.

This repository contains the complete project: the working prototype, the sample inputs and outputs, the 5 documented stress tests, the 5 prompt iterations, the Product Brief, the demo script, and screenshot evidence.

---

## How to Read This Repository

**Start here:**
- `ClearNote_Product_Brief.docx` — 2-page Product Brief written for a business audience
- `ClearNote_Demo_Script.docx` — 10-minute demo script with failure analysis

**The working tool:**
- `analyzer.py` — the actual Python script that runs ClearNote
- `transcript.txt` — sample meeting transcript used to test it
- `output_final.txt` — final structured analysis produced by the tool
- `output_stage1.txt` — the original baseline output (before prompt refinements) — useful for before/after comparison

**Stage 2 stress tests (5 types):**
- `test1_garbage.txt` / `test1_output.txt` — gibberish input
- `test2_edge.txt` / `test2_output.txt` — 2-sentence "meeting" edge case
- `test3_adversarial.txt` / `test3_output.txt` — prompt injection attempt
- `test4_volume.txt` / `test4_output.txt` — transcript duplicated 10×
- `test5_ambiguous.txt` / `test5_output.txt` — tentative language ("maybe," "we could")

**Stage 3 prompt refinements:**
- `CHANGELOG.md` — 5 documented prompt iterations with BEFORE / AFTER / WHY / RESULT
- `test1_output_v2.txt` — verification that the friendly error message now fires
- `test3_output_v2.txt` — verification that the tool now flags prompt injection attempts in RISKS / CONCERNS

**Screenshots:**
- `screenshot_1_working.png` — successful 5-section analysis
- `screenshot_2_adversarial_defense.png` — tool catching a prompt injection attempt
- `screenshot_3_friendly_error.png` — friendly error message on invalid input

---

## Key Outcomes

- 4 of 5 stress tests passed cleanly on first run; 1 returned a cryptic error (fixed in Stage 3).
- A "plausible hallucination" was caught in Stage 1 baseline output where the tool incorrectly attributed a decision to the CEO based on seniority rather than explicit assignment. This became Change #1 in the refinement log and is the central failure story in the demo.
- The tool correctly resisted a direct prompt injection attempt and, after Stage 3, now explicitly flags injection attempts under RISKS / CONCERNS.

---

## How the Tool Was Built

ClearNote was built using **Claude Code** (Anthropic's terminal-based coding agent). The core idea was to treat this as a prompt engineering project rather than a coding project — the `analyzer.py` script is a thin wrapper around a carefully iterated prompt that instructs Claude how to analyze meeting transcripts, refuse to invent names or dates, and flag missing information explicitly.

The full iteration history is in `CHANGELOG.md`.
