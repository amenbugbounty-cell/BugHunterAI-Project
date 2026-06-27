The Permanent Pattern System for Autonomous Security Research

🧠 What Is a Pattern?
A pattern is a reusable, structured representation of a common vulnerability, attack vector, or security misconfiguration that can be generalized across targets, technologies, and workflows. It is the result of observed or simulated relationships between inputs, outputs, and contextual factors.

Differences from Other Artifacts
Purpose	Key Characteristics
Reusable attack mechanism	Structured, validated, technology-agnostic as possible.
Foundation of understanding	General principles, reusable across contexts.
Permanent storage of findings	Ephemeral state, session data, validated evidence.
Composable attack steps	Linear or decision-tree sequence of actions.
Target-specific analysis	Validated evidence for a specific domain.
Repeatable attack template	High-level instructions for exploiting a vulnerability.
Unverified finding	Raw output from tool or manual inspection.
Exploration of unproven ideas	Hypotheses, experimental evidence, draft patterns.
Traceable, verifiable claim	Must include tool, source, and validation.
Hard-coded constraint	No context or adaptability (e.g., code linter).
Specific issue in a target	Must be tied to a case or pattern.
🧩 Why Pattern Recognition Over Brute-Force Testing?
Pattern recognition enables researchers to:

Avoid reinventing the wheel by reusing validated attack chains.
Reduce false positives through contextual understanding (e.g., "SSRF from a CDN" is more valid than random IP discovery).
Scale efficiently by generalizing findings across technologies (e.g., "XSS in input validation" applies to React, Angular, and Django).
Prioritize high-impact vulnerabilities (e.g., "business logic flaws" often rank higher than "low-severity XSS").
Experience becomes patterns by:

Codifying observations into structured, repeatable steps.
Validating findings through multi-tool correlation and real-world cases.
Refining patterns to remove noise and focus on causality.
🧭 Pattern Categories
Purpose	Example
Discovery techniques	CDN fingerprinting, rate-limit detection
Stack-specific attacks	Python deserialization in Flask
Framework-specific flaws	Django missing CSRF protection
Token-based issues	JWT signing key reuse
Access control bypasses	Missing role enforcement in GraphQL
Workflow-specific exploits	Cart checkout bypass in e-commerce
Timing-based flaws	Concurrent withdrawal exploit
Misconfigured uploads	MIME-type bypass in Next.js
REST/GraphQL specific	Over-fetching in GraphQL
Cloud-specific misconfig	Open S3 bucket in AWS
Client-side attacks	Prototype pollution in Vue
Browser-specific behavior	XSS in Chrome's WebKit engine
Cache misconfigurations	Insecure CDN caching of sensitive data
CDN-related vulnerabilities	Misconfigured Cloudflare cache-control
Query-related issues	Query overload in Apollo
Token misuse	None algorithm bypass
Authorization flow flaws	Invalid redirect URI
Server-side request forgery	Bypassing WAF to access internal APIs
Insecure direct object references	Bypassing product ID access in Express
Cross-site scripting	DOM-based XSS in Angular
Injection techniques	Blind SQLi in PHP
Server-side template injection	Mustache template code execution
Deserialization flaws	Java deserialization in log4j
Config errors	Open Redis server in Kubernetes
WAF evasion	Bypassing ModSecurity with Unicode encoding
Identifying targets	Detecting WordPress via HTTP headers
Evasion techniques	Slow scan to avoid rate-limiting
Tool chaining	Nuclei + Katana for JS-based XSS discovery
Structuring evidence	Organizing SSRF findings in Markdown templates
Misleading tool outputs	Nuclei false positive in benign input
Missed attacks	SQLi skipped due to poor query structure
📌 Pattern Structure
Every pattern must define:

Purpose: High-level intent (e.g., "Exploit SSRF via CDN misconfiguration").
Recognition Signals: Indicators observed during recon/scan (e.g., "CDN returns internal IP in headers").
Confidence: Hypothesis, Candidate, Validated, Well-established, Legacy, Deprecated, Experimental.
Prerequisites: Required tools/systems (e.g., "Wget", "Nuclei", "Katana").
Typical Environments: Technologies/conditions where it’s likely (e.g., "AWS S3 buckets", "React SPAs").
Technologies Involved: Frameworks, libraries, and tools (e.g., "React", "Node.js").
Common Mistakes: What researchers often get wrong (e.g., "Assuming SSRF requires public IP").
Related Bug Classes: Associated vulnerabilities (e.g., "SSRF", "Insecure Access Control").
Related Workflows: Example workflows using this pattern (e.g., "Recon → SSRF → Internal API Exploitation").
Related Tools: Tools that validate it (e.g., "Burp", "Bandit").
Possible Attack Chains: Composable patterns (e.g., "SSRF + Redis RCE").
False Positives/Negatives: Conditions to avoid (e.g., "CDN response may be unrelated to internal networks").
Evidence Requirements: What must be present to qualify (e.g., "Internal IP returned in response").
Severity Tendency: Likely impact (e.g., "High: Full system takeover").
Frequency: How common it is (e.g., "Medium: Seen in 30% of AWS deployments").
🔁 Pattern Lifecycle
Pattern Discovery:
From chat, tool output, or research (e.g., "Observed SSRF in CDN response").
Validation:
Correlate with existing patterns (e.g., "SSRF_CDN.md") and evidence (e.g., "Case_2026-001").
Generalization:
Remove target-specific details to make reusable (e.g., "SSRF in CDN" becomes "SSRF_CDN_Pattern").
Storage:
Add to /Patterns/ with pattern_id=SSRF-001.
Cross-Linking:
Add to related technologies (e.g., AWSCloud.md) and cases (e.g., Case_2026-001).
Reuse:
Apply in workflows (e.g., "Recon → CDN → SSRF_CDN_Pattern").
Improvement:
Update based on new evidence (e.g., "False positive rate reduced with new detection script").
Deprecation:
Archive if obsolete (e.g., "SSRF-001 replaced by SSRF-002 with better validation").
📈 Confidence Scoring
Description	Transition Conditions
Early-stage assumption	Confirmed by 2+ tools or cases.
Partially validated	Correlated with existing patterns.
Confirmed by 3+ cases or tools	Becomes Well-established after 180 days.
High consensus and reuse	Becomes Legacy if outdated.
No longer actively used	Merged into newer patterns.
Replaced by newer pattern	Removed after confirmation.
New and unproven	Becomes Candidate after validation.
🔗 Pattern Relationships
Purpose	Example
Depends on other pattern	Pattern_001 uses SSRF-002.
Shared concepts	IDOR.md is related to SSRF.md.
Provides realization	Pattern_001 implements SSRF.md.
Different but similar	Bandit is alternative to Nuclei.
Replaces outdated pattern	SSRF-002 supersedes SSRF-001.
Must be known before	XSS.md is prerequisite for DOM-XSS.md.
🔄 Pattern Evolution
Conditions	Owner
New evidence or validation	Researcher
Pattern becomes too broad	Editor
Duplicate with another pattern	Editor
Replaced by more accurate pattern	Reviewer
🔍 Pattern Search
Architecture for Querying Patterns:

Multi-dimensional indexing:
Tag-based search: technology=React, bug_class=CSRF.
Confidence filter: confidence=High, deprecated=False.
Tool-based query: tools=nuclei, tools=katana.
Relationship-based filtering:
"Show patterns related to SSRF that use CDN."
"Find patterns validated by Burp and Nuclei."
Context-aware prioritization:
Weight patterns by relevance to current target (e.g., "AWS-based SSRF patterns").
Highlight patterns with high evidence quality.
Gap detection:
"No validated patterns for SSRF in GCP." → Flag for improvement.
❌ Anti-Patterns
An anti-pattern is a recurring error, assumption, or false correlation that misleads researchers.

Examples:

False Correlation: "Assuming XSS in all <input> fields."
Tool Misuse: "Using Nuclei for business logic checks without contextual validation."
Weak Evidence: "XSS reported without browser console verification."
Premature Conclusion: "Declaring WAF bypass without correlation to backend logs."
Why Anti-Patterns Matter:

Reduce false positives/negatives.
Prevent wasted effort on invalid attack chains.
Improve overall system correctness.
🔗 Repository Integration
Integration	Example
Patterns derive from generalized knowledge	XSS.md in Web/.
Stored validated patterns feed memory	Pattern_001 becomes case evidence.
Patterns become steps in workflows	Workflow_XSS.md includes Pattern_001.
Validated patterns apply to real targets	Case_2026-001 references Pattern_001.
Playbooks apply patterns in sequences	SSRF_Playbook.md includes Pattern_002.
Reports must reference validated patterns	Report_2026-001 includes Pattern_003.
Reporting templates use pattern IDs	XSS_Template.md includes {pattern_id=001}.
🏛️ The Pattern Constitution
No Unvalidated Patterns: Must transition from hypothesis to validated before use.
No Duplicates: Single Source of Truth for every pattern.
No Isolated Patterns: Must link to at least 2 knowledge types (e.g., technology + bug class).
No Static Patterns: All patterns must evolve based on new evidence.
No Untracked Usage: Every pattern must appear in at least 1 workflow, case, or playbook.
No Unproven Confidences: Confidence must be explicitly defined and justified.
No Obsolete Patterns: All patterns must be reviewed every 180 days or archived.
This document defines how patterns are designed, validated, and reused at scale. It ensures that the system remains adaptable, accurate, and aligned with expert-level security research. Violations invalidate the pattern and require governance review.



You are designing the reasoning architecture of this autonomous security research platform.

You are NOT implementing reasoning.

You are defining how every future AI agent inside this repository should think.

Create:
