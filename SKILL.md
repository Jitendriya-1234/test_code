---
name: safety-code-review
description: "Use when reviewing C or C++ code for MISRA guidelines, ISO 26262 functional safety alignment, dead code, unreachable code, or unused logic. Report evidence-based findings and safety evidence gaps without changing files or claiming certification."
argument-hint: "Provide the review target, language, MISRA edition, ISO 26262 edition, ASIL, and available safety requirements or analyzer reports."
---

# Safety Code Review

Review code for applicable MISRA guidance, ISO 26262 software safety alignment,
and the absence of dead code. This is an evidence-based review, not a compliance
assessment, certification, or substitute for qualified safety engineering.

## Constraints

- Inspect files and existing reports only. Do not edit code or run commands.
- Use project-provided standards, coding policies, and approved deviations.
  Do not reproduce proprietary standards text or invent rule or clause numbers.
- Cite a MISRA rule or ISO 26262 clause only when its edition and reference can
  be verified from available authoritative material. Otherwise label the concern
  as general guidance requiring verification against the applicable standard.
- Separate confirmed defects, suspected issues, approved deviations, and missing
  evidence. A missing document does not prove the code violates a requirement.
- Do not infer an ASIL from code or claim compliance from a clean review.

## Procedure

### 1. Establish Context

Identify the files or changes, C or C++ language version, target platform,
compiler assumptions, build variants, and generated or third-party boundaries.
Determine the applicable MISRA edition and amendments, ISO 26262 edition,
allocated ASIL or QM classification, and project safety and coding requirements.
If these are missing, request the critical context or continue with an explicitly
limited preliminary review. Do not silently choose an edition or classification.

Read available safety requirements, architecture, deviation records, test
evidence, and static-analysis reports relevant to the target. Record what was
actually available; do not imply that unavailable artifacts were reviewed.

### 2. Review MISRA-Related Risks

Check applicable language and project policies for:

- Undefined, unspecified, and implementation-defined behavior and assumptions.
- Initialization, object lifetime, pointer validity, bounds, aliasing, and nulls.
- Type conversions, signedness, integer overflow, shifts, and enum usage.
- Expression side effects, evaluation order, and unsafe macro expansion.
- Control-flow correctness, switch handling, loop termination, and return paths.
- Declaration consistency, linkage, visibility, and interface contracts.
- Recursion, dynamic allocation, library use, and error handling where restricted
  by the applicable rule set or project policy; do not treat every use as banned.

For each potential violation, establish the triggering code and applicable
policy. Check approved deviations and their scope, rationale, risk assessment,
and supporting evidence before reporting a violation as unresolved.
State whether existing analyzer evidence covers the relevant configuration.

### 3. Review ISO 26262 Alignment

Focus on software-level evidence relevant to the reviewed component, especially
the activities addressed by Part 6. Check available evidence for:

- Traceability from allocated safety requirements to implementation and tests.
- Consistency with the software architecture, interfaces, and safety mechanisms.
- Input plausibility, boundary handling, fault detection, diagnostic reporting,
  and specified safe-state or degraded-mode behavior.
- Timing constraints, bounded execution, stack and memory budgets, shared state,
  concurrency, and freedom from interference where required by the architecture.
- Verification of normal behavior, boundary cases, fault paths, and integration
  assumptions, with requirements-based and structural coverage evidence suited
  to the applicable ASIL and project verification plan.
- Change impact analysis, configuration identification, and documented review
  or tool-confidence evidence where relevant and available.

Do not prescribe a generic safe state, universal coverage target, or mandatory
method without the applicable safety requirements and verification plan.
Report absent traceability or verification artifacts as evidence gaps rather
than automatically classifying the implementation as unsafe or noncompliant.

### 4. Check for Dead and Unreachable Code

The review objective is no unresolved dead code in the reviewed scope. Keep
unreachable statements distinct from executed computations whose results are
never used. Check both, along with unused functions, objects, parameters,
redundant conditions, overwritten values, and inactive preprocessor branches.

Trace entry points, callers, branches, and data usage before confirming an issue.
Consider interrupt handlers, callbacks, registration tables, linker references,
external consumers, generated code, assembly, and supported build variants.
Absence of textual references alone does not prove that code is dead.
Conditional code may be active in another supported configuration.

Do not recommend removing required defensive checks merely because nominal
execution cannot reach them. Check the fault model and safety requirements.
Explain evidence for dead-code findings and whether removal changes behavior,
side effects, diagnostics, interface compatibility, or safety mechanisms.
Recommend removal or justified restructuring and focused regression checks;
never remove code automatically. If reachability cannot be established with
available artifacts, mark it as suspected and specify the evidence needed.

### 5. Report Results

Lead with actionable findings ordered by Critical, High, Medium, and Low severity.
Base severity on demonstrated impact, not merely a rule category or missing
artifact. For each finding provide:

- Category: MISRA, safety alignment, dead code, or evidence gap.
- Status: confirmed, suspected, or evidence gap; note applicable deviations.
- Workspace-relative file link and relevant line number, or artifact reference
  for evidence gaps that cannot be tied to a source line.
- Trigger, evidence, impact, and verified standard or project-policy reference
  when available. Explicitly label unverified standards references.
- Recommended correction and a focused verification step, without applying it.

Finish with the scope and configurations reviewed, standards context, evidence
examined, and validation limitations. Say explicitly when there are no confirmed
findings, but do not claim MISRA compliance, ISO 26262 certification, or the
absence of all dead code without adequate whole-program and variant evidence.