# Task Templates
_Last updated: March 2026_
_Usage: master adapts these before sending to a slave. 
Reference by ID when generating task prompts. If no template 
fits, generate from scratch and consider adding a new one._

---

## [T-001] Deep Research Report
**Target:** GEMINI (Deep Research feature) or CHATGPT 
  (Deep Research feature)
**When to use:** Need comprehensive research on a topic before 
  making decisions. Output is a structured report, not a 
  quick answer.
**Template:**
"""
Use Deep Research for this task.

Topic: [specific topic or question]

Context: [1-2 sentences on why this matters for the project — 
  do not over-explain, the boot prompt has project context]

Cover:
- [specific angle 1]
- [specific angle 2]
- [specific angle 3]

Output format: Structured report with clear sections. 
Cite sources. Flag anything that is uncertain or contested.
No preamble. Start directly with findings.
"""

---

## [T-002] Debug Runtime Error
**Target:** Any slave with debugging domain
**When to use:** Runtime error with a traceback you need 
  diagnosed and fixed.
**Template:**
"""
Context: [1 sentence — what this part of the project does]
Stack: [relevant components involved]

Error:
[paste full traceback here]

File(s) involved: [list]
What was expected: [describe expected behaviour]

Task: Identify root cause and provide the fix.
Output: Short explanation (2-3 sentences) + corrected 
  code only. No preamble.
"""

---

## [T-003] Write or Refactor Code
**Target:** Any slave with coding domain
**When to use:** Generating new code or refactoring existing 
  code based on project context.
**Template:**
"""
Context: [what this code is for, where it fits in the project]
Relevant decisions: [D-XXX if any constraints apply]
Stack: [language, framework, libraries involved]

Task: [write / refactor] [specific function, module, or component]

Requirements:
- [requirement 1]
- [requirement 2]

[If refactoring, paste existing code here]

Output: Complete code only. No explanation unless something 
  deviates from the requirements. No preamble.
"""

---

## [T-004] Draft a Document
**Target:** GEMINI (Canvas if co-authoring) or CHATGPT (Canvas)
**When to use:** Need a structured written document — spec, 
  report, proposal, README, etc.
**Template:**
"""
Context: [what this document is for and who reads it]

Document type: [spec / report / proposal / README / other]
Tone: [formal / informal / technical / non-technical]

Cover:
- [section 1]
- [section 2]
- [section 3]

Constraints: [length, format, anything to avoid]

Output: Complete document, ready to use. No preamble. 
  No commentary after the document.
"""
Note: If this needs back-and-forth editing, use Gemini Canvas 
so you can co-edit in real time.

---

## [T-005] Summarise and Distil Research Output
**Target:** CLAUDE (master, in current chat)
**When to use:** A slave has returned a large research report 
  or document. You need master to extract what's relevant and 
  update project docs.
**Template:**
"""
The following is output from [SlaveID] on [topic].

[paste slave output]

Task: 
1. Extract what's relevant to the project
2. Flag anything that changes or informs existing decisions
3. Generate the additions or updates needed for:
   - project-brief.md (Current Status section if applicable)
   - decisions-log.md (new [D-XXX] entry if a decision 
     is implied)
   - architecture.md (Stack or Ruled Out section if applicable)

Output each update as a labeled block I can paste directly 
into the relevant doc. Only generate sections that actually 
need updating.
"""

---

## [T-006] Generate or Refresh Slave Boot Prompt
**Target:** CLAUDE (master, in current chat)
**When to use:** Initialising a new slave, or refreshing a 
  stale boot prompt after project has evolved.
**Template:**
"""
Generate a boot prompt for [AgentID] scoped to this project.

SlaveID: [what to call this instance, e.g. GEMINI-RESEARCH]
Domain: [what this slave handles]
Off-limits: [what it must not touch]
[If refresh]: What's changed since v[X]: [list changes]

Base on the slave boot template. Pull platform-specific 
suppression rules from agent-registry.md.
Output the complete boot prompt as a single copy-pasteable block.
"""

---

## Adding New Templates

When a novel task type produces a prompt worth reusing, append 
it here. Fields required:
- Sequential ID ([T-XXX])
- Target agent(s)
- When to use (specific trigger condition)
- Template (with [placeholders] for variable parts)
- Any notes on platform-specific variations

Keep templates as lean as possible. The boot prompt already 
has project context — templates only carry what varies per task.