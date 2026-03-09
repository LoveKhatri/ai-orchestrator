# Agent Registry
_Last updated: March 2026_
_Usage: master references these profiles when generating boot 
prompts and task prompts. Each agent has a fixed [AgentID] tag._

---

## [AgentID: CLAUDE]
**Platform:** claude.ai
**Default role:** Master
**Context window:** 200k tokens
**Strengths:**
- Direct, doesn't fold under pressure
- Strong at reasoning, system design, architecture decisions
- Code review and technical decision-making
- Orchestration — knows when to delegate and how to frame it
- Projects feature with Google Doc live sync
- Extended thinking mode for complex problems
- Memory across chats within a project

**Weaknesses:**
- Context compaction on very long projects
- Not ideal for heavy generative tasks (large docs, images, SVGs)
- Slower and more expensive for high-volume generation tasks

**Features:**
- Projects (instructions panel + file knowledge + Google Doc sync)
- Extended thinking mode
- Memory within projects
- GitHub file sync via files panel

**Best used for:** All thinking, decision-making, orchestration,
architecture, generating prompts for slaves, distilling outputs
back into project docs.

**Notes:** When context is getting long, start a fresh chat.
Project files carry the state, not the chat history.

---

## [AgentID: GEMINI]
**Platform:** gemini.google.com
**Default role:** Slave
**Context window:** 1 million tokens (2M coming)
**Strengths:**
- Largest context window of the three — can ingest entire 
  codebases, long research documents, multiple files at once
- Deep Research feature — autonomous multi-source research,
  produces comprehensive reports
- Canvas — collaborative real-time document editing where both 
  you and Gemini can edit the same document simultaneously. 
  Use this for tasks that need back-and-forth co-authoring, 
  not just output generation.
- Image generation
- Gems — persistent chat setup, equivalent to a saved boot prompt
- Strong at long-context reasoning and multimodal tasks
  (text, images, audio, video)

**Weaknesses:**
- Verbose — adds preamble, motivational closers, filler headers
- Glosses over details — output looks thorough but can be shallow
- Folds under pressure — pushback often causes it to agree 
  rather than defend a correct position
- Weaker than Claude at precise reasoning and architecture decisions

**Features:**
- Deep Research (autonomous web research, 5-30 min tasks)
- Canvas (real-time collaborative editing)
- Image generation
- Gems (persistent context, equivalent to saved boot prompts)
- Google Workspace integration

**Best used for:** Large context ingestion, deep research reports,
tasks that would burn Claude's context window, image generation,
co-authoring documents via Canvas.

**Suppress in boot prompts:** preamble, motivational closers,
excessive headers, sycophantic affirmations ("Great question!"),
filler content, confident-sounding output that glosses over gaps.

---

## [AgentID: CHATGPT]
**Platform:** chatgpt.com
**Default role:** Slave
**Context window:** 128k tokens
**Strengths:**
- Deep Research — comprehensive multi-source research reports,
  powered by o3, takes 5-30 minutes, strong at synthesis
- Web search — real-time web access via Bing integration
- Canvas — collaborative editing for writing and code
- Agent mode — can browse websites, click, interact with pages,
  and take real-world actions autonomously
- Projects feature — persistent context across chats
- Strong at isolated, self-contained tasks

**Weaknesses:**
- Smaller context window than Gemini (128k vs 1M)
- Less used in this system — profile will sharpen over time
- Can be verbose with unnecessary explanations and caveats
- Agent mode introduces prompt injection risks on untrusted sites

**Features:**
- Deep Research (o3-powered, async, comprehensive reports)
- Web search (real-time)
- Canvas (collaborative writing and code editing)
- Agent mode (web browsing + actions)
- Projects (persistent context)
- Image generation (GPT-4o native)

**Best used for:** Tasks that need real-time web information,
isolated context-burning tasks that don't need project history,
one-off generation tasks, anything requiring web interaction
via agent mode.

**Suppress in boot prompts:** verbose explanations when not asked,
excessive caveats, unsolicited suggestions outside task scope.

---

## Adding New Agents

When a new platform is added (e.g. Kimi, Minimax), add an entry
here following the same structure. Master references [AgentID]
tags when generating boot prompts and task prompts. The slave
boot template pulls behavioral suppression rules and feature
notes from this file.

Fields required for each new entry:
- AgentID (fixed tag, never change once set)
- Platform URL
- Default role
- Context window size
- Strengths (specific, not generic)
- Weaknesses (honest, will inform suppression rules)
- Features (only what's available on the web UI)
- Best used for (specific task types)
- Suppress in boot prompts (behavioral rules to enforce)