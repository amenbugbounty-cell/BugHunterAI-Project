Memory System Design Specification

🧠 What Is Memory?
Purpose
Memory is the repository’s permanent record of validated discoveries, patterns, and learned behaviors. It serves as the foundational reference for all future AI agents operating in this system.

Why It Exists
To store verified evidence and codified knowledge across sessions.
To eliminate redundant work by ensuring no finding is rediscovered without purpose.
To provide evidence-based reasoning for future workflows, research decisions, and strategic planning.
Problems It Solves
Scalable knowledge retention across years and many AI agents.
Traceable decision-making by linking conclusions to their source memory.
Avoidance of duplicate work in recon, analysis, or reporting.
Problems It Does Not Solve
Temporary session state: Chat history, unvalidated thoughts, or exploratory reasoning.
Unverified hypotheses: These require validation before being stored.
Short-term caching: These belong in session memory, not the repository.
🧩 Memory Categories
Lifetime	Storage	Update Policy	Deletion Policy	Validation	Owner	Relationships
Ephemeral (1 session)	/Memory/Sessions/	Overwrite if session active	Automatically deleted after session ends	Minimal	Planner	→ Research, Evidence
Short-Term (1-7 days)	/Memory/Working/	Updated hourly	Purged if idle >7 days	Moderate	Executor	→ Cases, Hypotheses
Permanent	/Memory/LongTerm/	Only on validation	Never deleted	Strict	Knowledge Manager	← Evidence, Patterns
Permanent	/Knowledge/	Only on architectural changes	Never deleted	Strict	Researcher	← Evidence
Permanent	/Memory/Evidence/	Versioned updates	Never deleted	Strict	Executor	→ Cases, Hypotheses
Temporary	/Memory/Hypotheses/	Overwritten on validation	Moved to Knowledge/Patterns/Case	Moderate	Researcher	→ Evidence
Permanent	/Knowledge/Patterns/	Only on new validation	Never deleted	Strict	Researcher	← Cases
Permanent	/Memory/Cases/	Updated after validation	Never deleted	Strict	Browser	→ Evidence, Patterns
Session/Permanent	/Memory/Preferences/* or /Config/	Overwrite for session, archived for permanent	User-managed	Strict	User	→ All modules
Permanent	/Architecture/	Immutable after finalization	Never deleted	Strict	AI Architect	← Knowledge
Permanent	/Governance/	Versioned updates	Never deleted	Strict	Principal Engineer	← Knowledge
Temporary	/Memory/Ideas/	Overwritten weekly	Purged after 30 days	Low	Researcher	→ Cases, Hypotheses
Permanent	/Memory/Failures/	Versioned updates	Never deleted	Strict	Researcher	→ Hypotheses
Permanent	/Memory/Lessons/	Only added with validation	Never deleted	Strict	Reviewer	→ Cases, Knowledge
Permanent	/Tools/	Only when tool changes	Never deleted	Strict	Executor	← Evidence
Permanent	/Memory/Target_Knowledge/	Updated with target	Never deleted	Strict	Planner	← Evidence
Permanent	/Memory/History/	Versioned updates	Never deleted	Strict	Knowledge Manager	← Cases
🔁 Memory Lifecycle
Information Enters:
From chat conversations, tool outputs, or researcher analysis.
Classification:
Determine type using context:
Tool Output → Evidence
Pattern → Knowledge/Patterns
Unproven Claim → Hypotheses
Session State → Session Memory
Validation:
Cross-reference with existing memory for duplicates or contradictions.
Verify against governance rules (e.g., Definition_of_Done.md).
Destination Selection:
Hypotheses → /Memory/Hypotheses/
Validated Cases → /Memory/Cases/
Permanent Knowledge → /Knowledge/
Storage:
All entries include metadata:
confidence: High, Moderate, Low
source: tool=nuclei, user=acme.com
validated: True/False
Review:
Automate periodic review for outdated information (Review_Checklist.md).
Refinement:
Convert Hypotheses to Patterns/Knowledge after validation.
Reuse:
Future agents query based on confidence, source, and tag.
Deletion:
Only possible after explicit review and governance approval.
🧮 Memory Classification Rules
Belongs in Knowledge:
Reusable patterns (e.g., JavaScript/IDOR_patterns.md).
Validated domains (e.g., Cloud/K8s_patterns.md).
Belongs in Research:
Unverified but plausible findings (e.g., SSRF_variant_2026.md).
Belongs in Cases:
Domain-specific findings (e.g., acme.com/admin_logic.md).
Belongs in Hypotheses:
Unproven attack vectors (e.g., SSRF_chain_for_aws.md).
Belongs in Session Memory:
Ephemeral session state (e.g., browser_session_20260627.md).
Belongs Nowhere:
Raw tool output (must be normalized into Evidence),
Unvalidated chat history.
🏦 Memory Validation
Avoid Garbage:
Require explicit validation rules (e.g., confidence threshold).
Correlate findings via 2+ tools for high confidence.
Avoid Duplicates:
Use tag-based searching with tool=, target=, pattern=.
Reject entries without traceable source validation.
Prevent Contradictory Knowledge:
Enforce Single Source of Truth (SSoT) for every pattern.
Use metadata to resolve conflicts (e.g., validated=True wins).
Detect Outdated Memory:
Tag with version= and target_date=.
Automate review based on timestamp and tool metadata.
🔄 Memory Review
Policy
Every 30 days for Working/Evidence; every 90 days for Patterns.
When tooling changes, domain evolves, or patterns become obsolete.
Requires governance approval and evidence of redundancy.
Move obsoleted entries to /Memory/Archive/ with metadata.
Finalized Knowledge/Evidence must be versioned and immutable.
🔄 Memory Relationships
Evidence → Cases: Tool outputs become part of domain-specific cases.
Cases → Knowledge: Generalization of findings into reusable patterns.
Hypotheses → Cases/Evidence: Validated hypotheses become cases/evidence.
Cases ↔ Failures: Correlated failures inform case updates.
Lessons → Cases/Knowledge: Historical validation improves future analysis.
No Duplicates: All relationships use reference IDs (e.g., case_id=1234).
📊 Memory Quality Metrics
Description	Policy
Validated by tool/output and source evidence	Must be validated=True
Time since last update	Revalidate if >90 days old
Traceable to source	Must include tool=, source=
High/Moderate/Low	Required for classification
Used in other memory types	High reuse = permanent Knowledge
Covers all validation requirements	Must pass Quality_Checklist.md
🔍 Memory Retrieval
Search:
Query by context tags (tool=nuclei, target=acme.com).
Prioritize validated=True entries.
Prioritization:
High confidence → Cases/Knowledge first.
Low confidence → Hypotheses/Research.
Conflict Resolution:
Prefer validated=True over validated=False.
Use timestamps and source metadata to break ties.
Confidence Affects Retrieval:
High confidence: Used directly in planning.
Low confidence: Requires manual review before use.
🧭 Repository Memory Philosophy
Repository Memory Is Permanent:
Chat memory is temporary; repository memory is eternal.
Every Claim Must Be Traceable:
No conclusions without source evidence.
No Garbage Memory:
Entry must pass validation before storage.
Memory Is Immutable (except metadata like validated flag):
New versions = new entries, not overwrites.
All Memory Must Be Versioned:
v0.1.0, v1.2.3, etc., for clarity.
📜 The Memory Constitution
Golden Rules
No Unvalidated Memory:
All entries must include validated=True or be explicitly tagged as Hypotheses.
No Duplicated Knowledge:
One authoritative location for every domain (e.g., JavaScript/ holds all JS patterns).
No Untraceable Claims:
Every memory must include source= and tool= metadata.
Repository Memory > Conversation Memory:
Chat history is temporary; repository memory is canonical.
Memory Must Survive:
Never delete memory without governance approval.
Confidence Must Be Explicit:
Label entries with High, Moderate, or Low confidence.
Evidence is Mandatory:
No claims without traceable source.
This is not a guideline. These are the unbreakable laws governing memory in this system. Failure to follow these rules invalidates the repository’s long-term integrity.



You are designing the permanent knowledge architecture of this repository.

You are NOT writing knowledge.

You are designing how knowledge itself should exist.

Create:
