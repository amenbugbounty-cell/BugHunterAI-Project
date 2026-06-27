Runtime Operating Rules for AI Agents

🔧 Repository Rules
File Creation:

Only create files explicitly required by CURRENT_STATE.md or Definition_of_Done.md.
Always search the repository before creating a file to avoid duplication.
New files must be documented in CURRENT_STATE.md under "In Progress" or "Pending Work".
File Updates:

Update files only to correct errors, expand knowledge, or align with architectural changes.
Never overwrite user work unless explicitly permitted and documented.
Always preserve original content before rewriting.
File Archiving:

Archive files when they become obsolete or superseded (move to /Archive/).
Archive files must retain metadata (version, date, reason for deactivation).
File Merging/Spitting:

Merge files only when their content is functionally identical or complementary.
Split files when exceeding 2000 lines or 4000 words (use .md or .py as needed).
Documentation Updates:

Documentation must be rewritten when:
The implementation changes.
Critical vulnerabilities are discovered.
Tooling or workflow patterns evolve.
🧱 Architecture Rules
Directory Structure:

Use 3 levels max of folder nesting.
All new systems must declare their location in Definition_of_Done.md before implementation.
Cohesion & Coupling:

No file may own more than 5 public methods or 1000 lines of code.
No system may depend on more than 3 direct neighbors.
Refactoring Rules:

Refactor when:
Files grow >2500 words.
Coupling crosses 10% of system.
Technical debt accumulates in 3+ areas.
📘 Documentation Rules
Clarity:

Every file must explain why it exists, not just what it does.
Use formal templates for workflows, prompts, and memory entries.
Completeness:

Every file must include:
Purpose declaration (≤3 paragraphs).
Input/output definitions.
Dependency declarations.
Versioning:

All documentation must include version numbers (e.g., v0.2.0).
💬 Prompt Rules
Modularity:

Prompts must be split into reusable components.
No monolithic prompts >1000 words.
Versioning:

Every prompt must use semantic versioning (e.g., 1.2.3).
Validation:

Prompt input must include:
Schema.
Expected confidence levels.
🧠 Knowledge Rules
Single Source of Truth (SSoT):

Every domain concept must have exactly one authoritative location (e.g., Knowledge/JavaScript.md).
Cross-Reference:

Use tags instead of duplication.
All cross-references must be updated when knowledge evolves.
Versioning:

Knowledge must be versioned with clear change logs.
💾 Memory Rules
Temporary vs Permanent:

Session memory is allowed for active workflows.
Repository memory must store all validated findings.
Storage Requirements:

Chat conversations are temporary. Repository files are authoritative.
Important discoveries must be persisted with tags (e.g., tool=nuclei, target=acme.com).
🤔 Reasoning Rules
Evidence-Based Decisions:

Always gather 3+ hypotheses before reaching a conclusion.
Prefer disproof of hypotheses over confirmation.
Assumption Avoidance:

Every claim must be labeled as Fact, Hypothesis, or Pattern.
State confidence levels explicitly (e.g., "High", "Possible", "Unconfirmed").
⚙️ Execution Rules
Pre-Requisites for Execution:

Understand dependencies and objective before executing.
Estimate execution impact.
Tool Selection:

Only run tools when:
They reduce cognitive load.
Their purpose is justified.
Document why a tool was selected in memory.
Avoid Blind Execution:

Never run tools "just because".
Prefer intelligent execution over brute force.
🛠️ Tool Rules
Usage Justification:

Every tool use must be justified in memory (e.g., "Validates HTTP response patterns").
Correlation Requirement:

Correlate results across 2+ tools to reduce false positives.
Tool Limits:

Never run unnecessary scans.
Follow false positive documentation in Tools/*.yaml.
🧩 Workflow Rules
Design Requirements:

Workflows must be decision trees, not linear lists.
Include exit conditions, confidence scoring, and recovery strategies.
Review Cycles:

Workflows must be reviewed every 60 days or after 50+ file changes.
🧹 Refactoring Rules
When to Refactor:

Refactor when:
3+ files share duplicated logic.
Technical debt accumulates in 3+ areas.
Refactoring Constraints:

Always preserve backward compatibility.
Test rewritten systems in memory first.
🔄 Review Rules
Self-Review Requirements:

All major changes must:
Challenge assumptions.
Check for duplication/architecture drift.
Look for missing documentation.
Rule Hierarchy:

Never compromise Golden Rules for convenience.
📢 Communication Rules
Transparency Mandates:

Always state uncertainty explicitly.
Always separate facts from assumptions.
Confidence Levels:

Use qualifiers like "High", "Possible", "Unconfirmed".
Never exaggerate findings.
✅ Quality Rules
Output Evaluation:

Every output must improve in at least one of:
Correctness ✅
Maintainability ✅
Scalability ✳️
Reusability ✳️
Rejection Threshold:

Discard outputs that:
Increase duplication.
Violate governance.
Add uncontrolled complexity.
♻️ Continuous Improvement
Improvement Cycle:
Review documentation monthly.
Refactor architecture quarterly.
Expand knowledge base with 8 new modules per year.
⛔ Golden Rules
These override all other rules:

No Duplication: Duplicate knowledge must be removed or merged.
No Assumptions: Every claim must be verified.
No Fabrication: Never create knowledge without evidence.
Single Source of Truth: Every concept must have exactly one location.
Continuous Improvement: Always leave the repository better than you found it.
Violation Consequences:
Violating a Golden Rule invalidates the current session and requires prior written approval.
Violating a technical rule triggers automatic review and possible rollback.
This is not a guideline—it is an operational constitution.



You are designing the memory architecture of an autonomous AI security research platform.

Do NOT implement memory.

Design the architecture first.

Create:
