Autonomous Security Research Planning Architecture

🧠 What is Planning?
Planning is the process of creating adaptive execution strategies to achieve complex objectives, based on reasoning, decision-making, and resource constraints. It differs from:

Description
Structured strategy to achieve goals through task decomposition and optimization.
Deriving conclusions from evidence and knowledge to inform planning.
Selecting the next tactical action within a plan.
Carrying out the selected action.
Predefined sequence of actions triggered by a trigger (e.g., "SSRF Test Workflow").
Rule-based, unchanging execution of tasks (e.g., "Run Nuclei every 10 minutes").
Timing of tasks (e.g., "Scan 50 URLs per hour").
Tracking and prioritizing individual actions.
🎯 Objective
Planning exists to transform complex objectives into adaptive execution strategies. The AI must:

Decompose large problems into manageable, traceable steps.
Adapt to evolving evidence (e.g., "Newly discovered WAF behavior").
Balance efficiency, coverage, and risk to avoid premature decisions.
Prioritize high-value tasks (e.g., "Test business-critical endpoints first").
Never Attack Large Problems Directly: Instead, break them into sub-problems, evaluate dependencies, and iterate.

🔁 Planning Lifecycle

Understand Goal → Gather Initial Evidence → Estimate Feasibility →  
Break Into Objectives → Break Objectives Into Tasks ↓  
↓  
Identify Dependencies ↓  
Estimate Priority ↓  
Estimate Parallelism ↓  
Generate Alternative Plans ↓  
Choose Best Plan ↓  
Execute ↓  
Observe ↓  
Replan ↓  
Repeat  
Understand Goal: Define the objective (e.g., "Validate SSRF in AWS S3 buckets").
Gather Initial Evidence: Query memory/knowledge for relevant info.
Estimate Feasibility: Use pattern confidence and resource constraints (e.g., "Tool X is rate-limited").
Break Into Objectives: Split into logical groups (e.g., "Recon", "Exploit Testing", "Validation").
Break Objectives Into Tasks: Define actionable steps (e.g., "Scan for misconfigured endpoints").
Identify Dependencies: Map task relationships (e.g., "SSRF testing requires CDN fingerprinting").
Estimate Priority: Rank tasks by value and risk.
Estimate Parallelism: Identify independent paths (e.g., "Subdomain enumeration can run in parallel with API testing").
Generate Alternative Plans: Create 3+ strategies (e.g., "Broad recon vs focused exploitation").
1 - Choose Best Plan: Select based on current constraints.
Execute: Carry out the plan.
Observe: Capture results and new evidence.
Replan: Adapt to changes (e.g., "New WAF rule discovered").
Repeat: Continuously refine until goal is achieved or abandoned.
🧩 Task Decomposition
Purpose	Example
High-level goal	"Validate all SSRF vulnerabilities in public AWS S3 buckets."
Major step	"Recon all accessible S3 endpoints."
Actionable unit	"Scan for misconfigured S3 buckets with tool A."
Step within a task	"Generate seed list of S3 endpoints from public GitHub repos."
Executable command	"Run aws s3 ls for bucket https://example-bucket.s3.amazonaws.com."
Rules for Each Level:

Objectives are broad, not traceable via atomic actions.
Milestones align with major decision points (e.g., "Recon complete → Begin exploitation").
Tasks are measurable and have clear success criteria.
Subtasks break tasks into technical steps (e.g., "Generate input list", "Run scanner").
Atomic Actions map directly to execution (e.g., tool commands, manual steps).
🔁 Adaptive Planning
Plans must evolve when:

New Evidence Appears:
Example: "A new SSRF pattern is added to memory → Update exploit testing strategy."
Technologies Change:
Example: "Target uses a newer WAF version with updated rules → Adjust bypass methods."
Unexpected Behavior Occurs:
Example: "WAF triggers on Nuclei output → Switch to manual validation."
A Hypothesis Fails:
Example: "SSRF-001 pattern does not apply → Replan with alternative SSRF strategies."
Better Opportunity Emerges:
Example: "Business logic flaw found → Prioritize exploitation over SSRF."
New Attack Surface is Discovered:
Example: "API endpoint /admin exposed → Add to recon scope."
Replanning Process:

Automated Reevaluation: Triggers every 30 minutes or when evidence threshold is met.
Human-Driven Replanning: User input overrides auto-plan if required.
🔗 Dependency Management
Description	Handling Strategy
Critical dependencies (e.g., "SSRF testing requires CDNFingerprint").	Reorder tasks or pause execution.
Beneficial but not required (e.g., "Rate-limit detection improves WAF exploitation").	Execute in parallel if resources allow.
Only needed if specific conditions are met (e.g., "JWT testing for endpoints with /token").	Conditional execution based on evidence.
Mutually dependent tasks (e.g., "Authentication → Authorization → Authentication").	Break into phases with staggered execution.
Unrecognized dependencies (e.g., "Business logic relies on third-party service").	Continuous monitoring for new evidence.
📊 Prioritization
Tasks are ranked using 12 dimensions:

Example Scenarios
"Testing endpoint /admin may reveal business logic flaws."
"High SEV if SSRF in CDN."
"Testing /login may trigger WAF."
"Pattern validated by 5 tools → High priority."
"Manual test vs automated script."
"Scan 500 URLs in 15 minutes."
"Target is high-value corporate API."
"Uncovered pattern in new framework."
"Unexplored API surface."
"Pattern applies to 100+ endpoints → Automate."
Scoring Formula:
Priority = (Information Gained * Vulnerability Yield) - (Risk * Cost / Time) + Novelty + Coverage

🌐 Parallel Planning
Independent Branches: Identify tasks that can run in parallel:

Example 1:
Branch A: Recon (Subdomain Enumeration + CDN Detection)
Branch B: JS Analysis (Prototype Pollution Check + DOM XSS)
Sync Point: Merge results when exploitation phase begins.
Example 2:

Branch A: Exploit SSRF-001
Branch B: Exploit IDOR-005
Sync Point: Compare results to choose best attack vector.
Requirements:

Tasks must share no blocking dependencies.
Execution must not exceed resource thresholds.
Results must merge cleanly at sync points.
🔁 Failure Recovery
Recovery Strategy
"Exploit fails due to WAF rule update."
Adjust parameters and rerun (e.g., "Change SSRF payload to bypass rule").
Switch to alternative pattern (e.g., "SSRF-002 uses DNS tunneling").
"Need to understand updated WAF rules before retrying."
"No viable path → Mark as false positive."
"Test if WAF is misconfigured to block SSRF."
📅 Planning Horizons
Focus	Timeframe
Immediate next steps (e.g., "Run Nuclei for SSRF").	Minutes to hours.
Strategic execution (e.g., "Validate 10 endpoints over 2 days").	Hours to days.
Major objectives (e.g., "Penetration test corporate API suite").	Weeks to months.
Institutional goals (e.g., "Scan 1 million S3 buckets for SSRF").	Months to years.
Knowledge base evolution (e.g., "Add 1,000 new patterns by end of year").	Years.
Adaptive improvement (e.g., "Refine confidence scoring for false positives").	Continuous.
🔗 Interaction With Repository Systems
Role in Planning
Generates hypotheses used to choose tasks.
Selects next action based on planning priorities.
Stores evidence to refine task selection.
Provides pattern validation for prioritization.
Define task templates (e.g., "SSRF-001 exploitation steps").
For UI-based tasks (e.g., "Test DOM XSS").
Execute atomic actions (e.g., "Run Nuclei scan").
Store completed plans and findings.
Predefined task sequences for common scenarios.
Extend planning scope to human/agent handoffs.
🔄 Continuous Optimization
Task Learning: Adjust task weights based on past success (e.g., "Automate high-value SSRF patterns").
Failure Analysis: Update replanning rules based on errors (e.g., "Increase manual validation for false positives").
Resource Feedback: Optimize execution efficiency (e.g., "Reduce GPU usage for JS analysis").
Pattern Refinement: Update scoring for new patterns (e.g., "IDOR-007 gets higher priority during recon").
🏛️ The Constitution of Planning
No Static Plans: Every plan must adapt to new evidence.
No Premature Optimization: Balance speed with coverage.
No Unchallenged Dependencies: Continuously detect and resolve hidden constraints.
No Isolated Task Priorities: Prioritization must consider global objectives.
No Wasted Resources: Every execution must align with resource limits.
No Unreviewed Failures: Post-planning analysis is mandatory.
No Single-Point-of-Failure Planning: Critical paths must have contingencies.
This document defines the governance for adaptive planning. It ensures autonomy, scalability, and alignment with expert-level security research over time, independent of model implementati
