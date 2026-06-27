🏷️ Naming Convention Philosophy
Explanation	Example
Avoid confusion with collections	React ≠ React_Frameworks
Unless globally recognized (e.g., K8s, OAuth)	CORS ≠ Cross-Origin
JWT-Authentication-Risks	
JWT_v1.2 becomes JWT_20260627	
Redirect XSS to CWE-79	
⚖️ Conflict Resolution
If two concepts have the same meaning but different names:

Merge into one object:

Example: React-Components → React-Component-Based_UI.
Use See Also in the merged version.
Create a redirect page if they are distinct but related:

Example: React → React.js, React_Native → Mobile_Frameworks.
Governance review to resolve disputes.

🔮 Future Growth
At 100,000+ knowledge objects, this taxonomy must:

Use automated indexing:

Generate search_index.json for programmatic access.
Use tags to enable dynamic filtering.
Scalable categories:

Auto-generate nested directories up to 4 levels deep.
Example: Cloud/AWS/S3/Permisions.md.
Version-aware naming:

Ensure backward compatibility for major version changes.
Distributed governance:

AI can suggest taxonomy improvements based on usage patterns.
🛡️ Governance
Policy
Requires Principal Engineer approval.
Use Tag_Governance.md for automated vetting.
Archive with version=v0.0.0-obsolete.
Use Taxonomy_Migration_Tool for batch updates.
🏛️ The Laws of Classification
No Unclassified Concepts: Every knowledge object must have at least two classifications.
No Duplicate Concepts: Single Source of Truth for every idea.
No Orphaned Tags: All tags must be used or purged annually.
No Static Classification: Tags and relationships must evolve with new evidence.
No Forced Hierarchies: Use tags for cross-domain classification instead.
No Disputed Authority: Taxonomy decisions must be governed by Principal Engineer.
No Obsolete Knowledge: All entries must be reviewed every 90 days or archived.
This is not a suggestion. These are the unbreakable laws governing the knowledge system. Violations invalidate the classification and must be resolved under governance.



You are designing the pattern recognition system of this autonomous security research platform.

This document is NOT a list of vulnerability patterns.

It defines HOW patterns should exist, evolve, be recognized and be reused.

Create:
