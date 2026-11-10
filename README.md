PRISM — Privilege Review Multi-Agent System (Design)
Status: Design document. Not built. Not tested in production.

PRISM is a design for a privilege review / QC workflow. It describes how multiple review agents and a human reviewer would work together, with a human gate and an audit trail. It is not a running system.

Problem it is designed for
In eDiscovery / records review, privilege review needs:

Consistent application of privilege rules
A clear reason for every privilege call
A human reviewer who makes the final decision
An audit trail that shows who / what decided what, and why
PRISM is a proposal for how to structure that, not a claim that it is already working.

Proposed architecture
Agent 1 — Triage

Checks completeness: Does the document have text, metadata, and a privilege tag?
Flags missing data for human review.
Agent 2 — Privilege Classifier (proposed)

Applies written privilege guidelines to label: Privileged / Not Privileged / Needs Human Review.
Must output a rationale citing the guideline rule used, not just a label.
Agent 3 — QC / Consistency Checker

Checks for conflicts: e.g. same email thread labelled differently, or privilege label without a rationale.
Flags edge cases: mixed content, forwarded emails, attachments with different privilege.
Human Review Gate — Final Decision

A human reviewer sees the agent proposal, rationale, and source document.
Human can Accept, Overturn, or Send for Second Review.
No document is marked Privileged without human approval. The agents propose, the human decides.
Audit trail (design)
Every decision would log:

Document ID
Agent proposal + rationale + guideline rule cited
Human decision + human rationale
Timestamp
Final label
This is required for chain of custody and for explaining a privilege call later.

Manual test scenarios (paper walkthrough, not code)
These are 3 paper scenarios I walked through manually to test the design logic. No code was run.

Scenario 1 — Clear Privileged Email

Email from lawyer to client asking for legal advice.
Expected: Agent proposes Privileged, human accepts. Passes design check.
Scenario 2 — Mixed Thread

Thread starts as business update, later adds a lawyer asking for legal advice.
Expected: Agent flags Needs Human Review, human splits the review by message, not by thread. Tests edge-case handling.
Scenario 3 — False Positive Risk

Business email that mentions “legal” but is not legal advice.
Expected: Agent must not auto-label Privileged on keyword alone. Must check intent against guideline. Human overturns if agent over-calls.
What this project is NOT
Not a running multi-agent system
Not tested on real client data
Not tested on production data
Not a claim of AI accuracy
No model was trained, fine-tuned, or evaluated
It is a design + 3 paper scenarios to show how I think about guideline adherence, rationale writing, and human-in-the-loop QC.

Limitations
Design only. No code, no evaluation, no inter-annotator agreement measured.
No real or synthetic dataset was run through it.
Privilege rules vary by matter and jurisdiction — this design uses generic rules, not a real matter’s protocol.
Next steps (if I build it)
Write a short privilege guideline with worked examples and edge cases
Build a small synthetic dataset (20-30 docs, no PII, no real client data)
Run a pilot with Label Studio or a spreadsheet: agent proposal vs human decision, measure agreement and rationale quality
Update this README only after the pilot exists
Files
README.md: this design document (only file for now)
