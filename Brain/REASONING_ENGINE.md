The Permanent Reasoning Architecture for Autonomous Security Research

🧠 What Is Reasoning?
Reasoning is the structured process of deriving justified conclusions from evidence through logical deduction, pattern matching, and contextual analysis. It differs from:

Difference From Reasoning
Static understanding that reasoning applies to specific contexts.
Permanent storage of findings, reasoning generates traceable conclusions.
Reusable attack templates, reasoning adapts them to new situations.
Predefined steps for actions, reasoning decides why and when to follow them.
Rule-based execution, reasoning evaluates the validity of actions.
Carrying out actions, reasoning determines which actions to prioritize.
Triggering specific behaviors, reasoning synthesizes responses from patterns.
Finding information, reasoning evaluates the relevance and quality of results.
Unvalidated assumptions, reasoning requires evidence-based validation.
🎯 Fundamental Objective
Reasoning is Not Just Answering. It is Building Justified Conclusions from:

Evidence (tool output, manual findings, historical data)
Patterns (validated attack templates)
Knowledge (domain-specific understanding)
Context (target environment, tool constraints, business logic)
Every conclusion must be:

Explainable (Why was this decision made?)
Traceable (Which patterns/knowledge files influenced it?)
Adaptable (Can it evolve with new evidence?)
🔁 Reasoning Lifecycle

Understand → Decompose → Collect Evidence → Generate Hypotheses → Rank Hypotheses → Attempt Falsification → Gather Missing Evidence → Update Confidence → Choose Best Explanation → Decide Next Action → Review Decision  
Understand: Define the problem clearly (e.g., "Why is the API responding with 500 errors?").
Decompose: Break into smaller questions (e.g., "Is it a rate limit? A misconfigured endpoint? A server error?").
Collect Evidence: Combine tool outputs, memory, and cross-referenced patterns.
Generate Hypotheses: Always create 3+ alternatives (e.g., "Rate limit bypass", "Misconfigured headers", "Server-side validation flaw").
Rank Hypotheses: Use evidence quality, confidence, and relevance.
Attempt Falsification: Test assumptions (e.g., "Simulate different requests to see behavior").
Gather Missing Evidence: Query logs, patterns, or perform targeted tool checks.
Update Confidence: Reflect new evidence (e.g., "XSS hypothesis confirmed with 2 tool corroboration").
Choose Best Explanation: Select the most plausible hypothesis.
Decide Next Action: Plan next steps (e.g., "Test SSRF chain", "Document findings").
Review Decision: Check for bias, false positives, or missing constraints.
🧩 Hypothesis Generation
Never stop at the first explanation. Always ask:
What if the target is using a CDN that hides internal IPs?
Could this false positive be a tool misinterpretation?
Rank hypotheses by:
Evidence strength (tool corroboration ≥ manual analysis ≥ research).
Pattern confidence (Well-established > Experimental).
Reject weak hypotheses:
"All 403 responses are WAF blocks" (overgeneralization).
"XSS in every Angular app" (lack of contextual validation).
Strengthen good hypotheses:
Use multiple tools to confirm edge cases.
Correlate with existing workflows and patterns.
📊 Confidence
Description	Evolution
Initial hypothesis (e.g., "Possibly IDOR in endpoints").	Requires tool corroboration.
One validated evidence source (e.g., "Nuclei detects XSS").	Needs additional validation.
Two corroboration sources (e.g., "Nuclei and manual test confirm").	Acceptable for case documentation.
Three+ corroboration and no contradictions (e.g., "Burp confirms SSRF chain").	Suitable for pattern reuse.
Corroborated across workflows, tools, and cases (e.g., "JWT misconfig proven in 5 targets").	Foundation for long-term knowledge.
Confidence never increases without evidence.

🔍 Evidence Evaluation
What Counts as Evidence
Tool outputs (e.g., Katana finds JS file).
Memory entries (e.g., "Similar pattern in AWS S3 buckets").
Case data (e.g., "Confirmed JWT signing key leak in Case_2026-001").
Pattern corroboration (e.g., SSRF-001 applies to this target).
What Does Not
Uncorrelated logs.
Untested assumptions (e.g., "This might be a race condition").
Tool false positives (e.g., Nuclei reports a vulnerability without manual validation).
Handling Conflicts
Prefer evidence from higher-confidence sources (e.g., manual validation > raw Nuclei output).
Reject contradictory evidence unless it's clearly outdated or misclassified.
Expressing Uncertainty
Use qualifiers like "Possible", "Unconfirmed", "Unlikely", "Conditional On".
Example: "XSS possible in endpoint /api/v2 conditional on missing sanitization".
🤔 Reasoning Styles
Purpose	When to Use
From general to specific	Validating a pattern against a target (e.g., "SSRF-001 applies here").
From specific to general	Creating new patterns from case findings.
Best-explanation inference	Explaining unexpected behavior (e.g., "Why is WAF blocking these requests?").
Contrasting similar patterns	Resolving ambiguity between "JWT signing key reuse" vs "HMAC token forgery".
Identifying cause-effect relationships	Debugging why an API fails under load.
Testing alternate outcomes	"What if the CDN wasn’t configured? Would SSRF be exploitable?"
Simulating attacker intent	"How could an attacker bypass this WAF rule?"
Breaking problems into sub-problems	Decomposing a complex race condition.
Structured multi-layer reasoning	Solving business logic flaws by analyzing authentication, authorization, and rate limits.
🚫 Failure Detection
The AI must actively detect:

Tunnel Vision: Overreliance on a single pattern (e.g., "Everything is IDOR").
Confirmation Bias: Ignoring contradictory evidence (e.g., "Only testing XSS in known endpoints").
Overconfidence: Assuming "This is always a false positive" without validation.
Weak Evidence: Accepting Nuclei reports without manual verification.
Circular Reasoning: "This is a WAF because it blocks SSRF requests, and I know it’s a WAF because it blocks SSRF."
Premature Conclusion: Stopping investigation when a pattern is only 50% confirmed.
Pattern Overfitting: Applying SSRF-001 when it’s a CDN misconfiguration, not SSRF.
Tool Bias: Assuming every Bandit finding is valid.
Automation Bias: Trusting workflows without questioning context.
🔍 Self-Critique
Every conclusion should trigger a formal self-review process:

What if I am wrong?
Could this be a false positive?
Am I mistaking correlation for causation?
What evidence contradicts me?
Are logs inconsistent with my hypothesis?
Do other tools or memory entries suggest a different outcome?
What assumptions am I making?
Do I assume the WAF is configured identically everywhere?
Am I ignoring business logic constraints?
What am I missing?
Could there be a race condition I haven’t tested?
Have I checked rate limit policies?
Could there be another explanation?
What if the 403 response is due to missing CSRF tokens, not a WAF?
🛡️ Security Reasoning
Reasoning Focus
Deductive and inductive reasoning for fingerprinting.
Pattern-based reasoning to identify technologies.
Causal reasoning to confirm server-side frameworks.
Hierarchical reasoning to model user workflows.
Abductive reasoning to test JWT token security.
Recursive reasoning to map access control chains.
Comparative reasoning to identify prototype pollution.
Causal reasoning to debug malformed requests.
Inductive reasoning to detect misconfigured services.
Deductive reasoning to confirm network topology.
Counterfactual reasoning to simulate attacker behavior.
Confidence-based reasoning to prioritize tool scans.
🚦 Decision Making
When to Use
Confidence is high, next step is clear.
Missing critical evidence (e.g., "Need to test 503 responses before SSRF").
New pattern or hypothesis requires further validation.
Conflicting evidence needs manual testing.
Requires user input (e.g., "Confirm if WAF rule is valid").
Store findings in memory or cases.
Evidence is robust and reusable.
Workflows or patterns are outdated.
Low-confidence evidence (e.g., "Experimental pattern, insufficient corroboration").
🧬 Long Investigations
Investigations spanning hours/days must:

Retain State: Use memory (Session_Memory/) to track unresolved questions.
Reference External Data: Link to knowledge, patterns, and cases.
Iterate: Return to Generate Hypotheses if new evidence arises.
Resume from Checkpoints: Ensure reasoning continuity after context loss (e.g., "Restart session from Case_2026-001").
🔗 Interaction with System Components
Role in Reasoning
Provides foundation for pattern generalization.
Hypotheses are evaluated against validated patterns.
Historical evidence resolves ambiguity.
Actions are prioritized based on pattern confidence.
Real-world validation refines hypothesis ranking.
Hypotheses evolve into new patterns.
Predefined reasoning pathways for common scenarios.
Directly feeds confidence scoring.
Document traceable conclusions for future reuse.
Ensures reasoning compliance with governance (e.g., Pattern_Constitution).
🔄 Continuous Improvement
The reasoning engine must:

Learn from Successes
Store well-ranked hypotheses into patterns.
Learn from Failures
Archive hypotheses with poor corroboration into anti-patterns.
Adapt to Missed Vulnerabilities
Update reasoning rules to prioritize previously overlooked patterns.
Reduce False Positives/Negatives
Use case metrics to refine confidence thresholds.
Evolve with Architecture
Integrate new knowledge categories into reasoning workflows.
🏛️ The Laws of Reasoning
No Unvalidated Conclusions: Every hypothesis must evolve from confidence to action.
No Single-Source Evidence: Must corroborate across at least 2 independent sources.
No Unchallenged Assumptions: Every conclusion must be subjected to falsification.
No Static Hypotheses: Must revisit outdated conclusions at least every 30 days.
No Untraced Decisions: Every critical step must document evidence, patterns, and knowledge used.
No Biased Reasoning: Actively detect and reject tunnel vision, confirmation bias.
No Premature Automation: Avoid executing workflows without confidence validation.
This is not a suggestion. These laws govern every reasoning process, ensuring robustness, adaptability, and long-term correctness regardless of AI model implementation.



You are designing the decision engine of this autonomous security research platform.

This document defines how every future AI agent decides what to do next.

Create:
