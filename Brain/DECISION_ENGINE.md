Autonomous Security Research Decision Engine

🎯 What Is a Decision?
A decision is a deliberate selection of the next action to take, based on reasoning, evidence, and predefined strategic goals. It differs from:

Relationship to Decision
Generates hypotheses and conclusions that feed into decisions.
Carries out the chosen action.
High-level strategy that informs decisions by defining objectives.
🔁 Decision Lifecycle
A comprehensive decision process:


Understand Context → Collect Information → Evaluate Knowledge → Generate Actions →  
Estimate Value → Estimate Cost → Estimate Risk → Rank Actions → Choose Best Action →  
Execute → Observe Result → Learn → Update State  
Understand Context:

Define the current objective (e.g., "Validate SSRF in CDN").
Identify constraints (e.g., "Rate limited to 100 requests/day").
Collect Information:

Pull from memory (e.g., "Similar SSRF pattern in case_2026-001").
Query knowledge (e.g., "AWS S3 misconfigurations").
Gather partial evidence (e.g., "Nuclei output for endpoint /api/v1").
Evaluate Available Knowledge:

Correlate with patterns (e.g., "Match to SSRF-004: CDN Bypass").
Verify knowledge relevance (e.g., "Is this applicable to current target?").
Generate Possible Actions:

Enumerate options (e.g., "Test SSRF exploit", "Check WAF rules", "Gather logs").
Estimate Expected Value:

Information gain (e.g., "Testing endpoint /api/v1 provides 80% confidence").
Vulnerability yield (e.g., "Potential SSRF exploit with high SEV score").
Estimate Cost:

Time (e.g., "Manual test vs automated tool").
Resources (e.g., "GPU usage for crawling").
Complexity (e.g., "JavaScript DOM analysis vs API brute-force").
Estimate Risk:

Likelihood of false positives/negatives.
Impact of premature execution (e.g., "Triggering WAF may exhaust rate limit").
Rank Actions:

Use a weighted scoring model (e.g., 40% Value : 30% Cost : 30% Risk).
Choose Best Action:

Select the top-ranked option.
Execute:

Carry out the action (e.g., "Run Nuclei template for SSRF").
Observe Result:
Capture new data (e.g., "Nuclei confirms SSRF in response").
Identify side effects (e.g., "WAF triggered by 5 requests").
Learn:
Update pattern confidence (e.g., "SSRF-004 score increases with tool corroboration").
Store new evidence in memory (e.g., "Case_2026-002").
Update State:
Modify the investigation roadmap.
Adjust knowledge relevance.
Reopen paused investigations if new evidence emerges.
🛠️ Decision Categories
Purpose
Proceed along current path.
Wait for new evidence.
Collect data before next step.
Change from recon to exploitation.
Execute automated tests (e.g., Nuclei, Subfinder).
Human intervention for ambiguous cases.
Test UI-based patterns (e.g., DOM XSS).
Query patterns or workflows.
Retrieve historical findings.
Finalize findings.
Save validated pattern.
Optimize future steps.
Handle advanced threats (e.g., WAF evasion).
Simplify investigation scope.
Include new surfaces (e.g., test mobile endpoints).
Focus on high-value targets.
Defer to human when uncertain.
Repost failed step with modified parameters.
Terminate dead-end investigations.
Revisit later with additional data.
📊 Decision Scoring
Every action is evaluated across dimensions:

Description	Example Weights
30%	"Testing /admin may reveal sensitive data."
25%	"High SEV if XSS in login page."
20%	"Pattern confirmed by 3 tools."
10%	"Manual test vs automated script."
10%	"CPU/GPU usage for crawling."
5%	"Premature testing may trigger WAF."
Adaptive Scoring: Adjust weights based on context:

Recon Phase: Prioritize information gain over risk.
Exploitation Phase: Prioritize vulnerability yield and risk.
🧭 Branching Philosophy
The AI must evaluate all possible decision branches simultaneously, prioritizing based on dynamic evidence:

Should I continue here? → Yes if current path has sufficient confidence.
Should I switch? → Yes if higher-value action exists (e.g., "Switch to SSRF testing").
Should I investigate deeper? → Yes if current evidence is inconclusive.
Should I create parallel investigations? → Yes if multiple hypotheses are valid (e.g., "Test XSS and CSRF in parallel").
Should I postpone this path? → Yes if low-confidence evidence (e.g., "Defer IDOR until WAF is resolved").
Should I revisit later? → Yes if dependency on another task (e.g., "Revisit API rate limits after WAF test").
🔄 Adaptive Decision Making
Decisions must evolve with new evidence:

Immediate Adaptation:

If a tool confirms an SSRF pattern, shift to exploitation workflows.
Plan Refinement:

Update scoring if confidence in a pattern decreases.
Fallback Strategies:

If automated testing fails, trigger manual analysis.
🧩 Investigation Strategies
Purpose	Preferred Use Case
Cover many surfaces (e.g., "Scan all endpoints with Nuclei").	Initial recon phase.
Focus on one surface (e.g., "Test 50 scenarios for XSS in login page").	When high-confidence pattern is identified.
Prioritize framework-specific flaws (e.g., "Test JWT token validation in Angular app").	Targeting well-known tech stacks.
Prioritize high-risk surfaces (e.g., "Focus on /admin and /api/v1").	Time-constrained scenarios.
Prioritize business-critical flows (e.g., "Test checkout API").	Corporate or e-commerce targets.
Use known patterns to guide testing (e.g., "Apply IDOR pattern to product IDs").	High-confidence pattern contexts.
🔌 Resource Management
Use Case	Optimization Criteria
Crawling, pattern generation	Prioritize parallelism for high-efficiency tasks.
Deep learning tasks	Use when analyzing large datasets (e.g., JS reverse engineering).
UI-based testing (e.g., DOM XSS)	Limit to high-priority flows to reduce rate limit risk.
Broad exploration	Maximize speed but avoid triggering WAF.
Automated enumeration (e.g., Katana)	Use in early recon to gather baseline data.
High-uncertainty scenarios (e.g., complex business logic)	Only when automated tools fail or risk is high.
High-confidence patterns (e.g., testing multiple XSS endpoints)	Scale only when resource limits allow.
Redundant tool usage	Check if pattern already validated in memory.
🔍 Uncertainty Handling
When uncertainty exists, evaluate:

Action
Example: "Need manual test for DOM XSS if Nuclei output is ambiguous."
Example: "Switch to business logic testing instead of brute-forcing endpoints."
Example: "Test IDOR and SSRF in parallel if both are likely."
Example: "Ask user to confirm if target allows SSRF exploitation for legal reasons."
🛑 Stopping Conditions
Decide to stop based on evidence, not arbitrary thresholds:

Path Excluded: If evidence discredits a pattern (e.g., "No IDOR in endpoint /api/v2").
Sufficient Evidence: If confidence in a vulnerability is 95%+ (e.g., "Burp confirms XSS").
Report Ready: If all critical findings are validated and documented.
Knowledge Updated: If new patterns or workflows are required.
New Investigation: If a higher-priority target is identified.
🧪 Post-Decision Review
After every major decision, the AI should ask:

Was this the best decision?

Compare against alternatives (e.g., "Could SSRF be tested through other endpoints?").
What did I learn?

Update scoring weights based on success/failure (e.g., "Nuclei has 75% false positive rate for this target").
Would I choose differently now?

Adapt to new evidence (e.g., "Use manual validation next time to avoid false positives").
🔄 Continuous Optimization
Pattern Influence: Use validated patterns to guide decisions without overriding evidence.
Success Reinforcement: Reward high-value decisions (e.g., "High-scored actions get 20% weight in future scoring").
Failure Learning: De-prioritize low-success actions (e.g., "Reduce Nuclei usage for false positives").
Dynamic Weights: Adjust scoring weights as new patterns emerge (e.g., "IDOR patterns gain 10% weight during API testing").
🏛️ The Decision Constitution
No Arbitrary Decisions: Every choice must be traceable to evidence and reasoning.
No Static Plans: Decisions must adapt to evolving evidence and context.
No Unbalanced Risk: High-risk actions require corroboration or user approval.
No Premature Automation: Manual verification is mandatory if confidence is low.
No Wasted Resources: Every action must have measurable benefit (e.g., "Avoid redundant tool scans").
No Isolated Patterns: Decisions must integrate knowledge, memory, and evidence.
No Unreviewed Decisions: Post-execution analysis is mandatory for all high-impact choices.
This document defines the governance for autonomous decisions. It ensures adaptability, efficiency, and correctness in complex, evolving security scenarios, regardless of underlying AI model or toolset.



You are designing the planning engine of this autonomous security research platform.

Create:
