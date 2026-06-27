Permanent evidence storage	Memory/Evidence/acme.com_nuclei.md
✅ Knowledge Quality Standards
Every knowledge file must include:

Purpose: Why does this knowledge exist? (e.g., "To explain CORS configuration risks in Express").
Summary: One-paragraph overview.
Prerequisites: Required prior knowledge (e.g., "Basic HTTP concepts").
Concepts: Detailed technical explanation.
Relationships: Links to relevant categories or files.
Examples: Real-world snippets or case references.
Common Mistakes: What researchers often get wrong (e.g., "Assuming CORS is the only API security vector").
Real-world Relevance: How this applies across industries/targets.
References: Linked to References/ or Cases/.
Future Improvements: Known gaps or suggested extensions (e.g., "Expand to include FastAPI examples").
Confidence: High, Moderate, or Low.
Version: v0.1.0, v1.2.3, etc.
🔄 Knowledge Evolution
Conditions	Owner
New evidence, tool changes, or industry shifts	Researcher
File exceeds 2000 words or contains unrelated sub-topics	Editor
Duplicated content across files	Editor
Obsoleted by new technology or research	Reviewer
Structural issues, poor clarity, or incorrect evidence	Researcher
Knowledge is invalid or replaced by better patterns	Reviewer
🔗 Cross-Linking Philosophy
Avoid duplication by linking to authoritative files (e.g., CORS.md in Web/Security).
Use reference IDs (e.g., pattern_id=SSRF-001) for pattern relationships.
Reference cases with case_id=2023-001 to show real-world relevance.
Maintain a "See Also" section for related knowledge, patterns, and cases.
🔍 Indexing Strategy
Hybrid Index with 3 Layers:

Category-Based Directories: Technologies/, Vulnerabilities/, Patterns/.
Tag-Based Search:
vulnerability=SSRF, technology=AWS, pattern=IDOR
tool=nuclei, target=acme.com, confidence=High
Index Files:
index.md in each directory for curated entries.
search_index.json for programmatic querying.
⚖️ Conflict Resolution
Version Resolution:
Higher versions (v2.0.0 > v1.0.0) override lower ones.
Validation Check:
validated=True entries override validated=False.
Governance Approval:
Conflicts with validated=True must be resolved by Reviewer.
Obsolescence:
Older entries are archived automatically if outdated by more than 30 days.
🔄 Knowledge Review
Frequency	Method
Monthly	Review Future Improvements sections.
Weekly	Flag entries >90 days old without version bump.
Quarterly	Analyze popular GitHub projects for new stack trends.
Biweekly	Cross-reference with new cases for accuracy.
🌐 Future Scalability
50,000 Knowledge Files will require:
Automated Indexing using a search_index.json database.
Modular Sub-Directories by technology (e.g., /Technologies/Web/React/).
Distributed Indexing for cross-reference resolution.
Scalability Principles:
No directory exceeds 1,000 files.
No file exceeds 2,000 lines.
No circular dependency between categories.
🏛️ The Constitution of Knowledge
Unbreakable Laws
No Unvalidated Knowledge: Every claim must include validation evidence or be tagged hypothetical.
Single Source of Truth: No overlapping knowledge for the same concept.
Versioning is Mandatory: File vX.Y.Z must align with Quality_Checklist.md.
No Static Knowledge: Files must evolve or be archived every 3 months.
Cross-Linking is Required: No knowledge can exist in isolation—reference others.
Indexing is Non-Negotiable: Every file must appear in search_index.json for traceability.
Evidence is Mandatory: No knowledge without traceable sources (tool output, cases, research).
Reviewer Authority: Final validation rights lie with Reviewer.
This document defines the architectural framework for knowledge growth. It is not a suggestion. It is the governance foundation for every knowledge file in the repository.



You are designing the taxonomy of the entire knowledge system.

This is NOT documentation.

This is NOT a folder structure.

This defines how every concept inside the repository will be classified forever.

Create:
