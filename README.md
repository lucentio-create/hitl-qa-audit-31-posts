hitl-qa-audit-31-posts
A human QA audit of 31 labelled social media posts, using a 6-point checklist.

Data note: The 31 posts are synthetic practice data written for training, not real social media data. This is a simulated QC audit, not a production project. No AI model was tested. I audited labels and priority flags that were already assigned.

What I did
Acting as QC, I checked each post's label (Complaint, Inquiry, Praise, Spam) and priority flag against six criteria, marked Pass or Fail, and wrote a reason for every Fail.

Audit checklist
ID	Criterion	What it checks
C1	Intent label	The label matches the real meaning of the post
C2	Dialect / Pidgin	Fails only if misreading the dialect caused a wrong label
C3	Urgency flag	Urgent complaints (money stuck, failed charges, outages) are flagged Yes
C4	Spam handling	Spam is labelled Spam, and genuine posts are not wrongly labelled Spam
C5	Ambiguity	Sarcasm or dual-intent posts get a sensible label
C6	Completeness	Every post has a label
Results (31 posts)
Error rate = posts failed / posts audited x 100

Posts audited: 31
Posts with at least one Fail: 7 (23%)
Total criterion failures: 11 (one post can fail several criteria, e.g. Post 24 failed C1, C2 and C3)
Criterion	Fails	Failed Posts
C1	3	1, 23, 24
C2	1	24
C3	5	3, 5, 15, 24, 28
C4	2	1, 23
C5	0	None
C6	0	None
Findings
Most common error: C3 (urgency flag), 5 of 31 posts.
Flag: Yes was often missing on financial loss (stuck refunds, failed debits, overcharges) and major outages, even though similar complaints in the same set were flagged correctly.

Next: C1 (intent label), 3 of 31 posts.
Example (Post 1): A genuine price query was labelled Spam. This is a false positive, so it fails C1 and C4.

Dialect example (Post 24): A Pidgin financial phrase was misread, which caused a wrong intent label and a missing urgency flag. This is why C2 and C3 are checked separately from C1 - a dialect miss can cause two downstream errors.

Recommendations
High (C3, 5 fails): Require Flag: Yes for any post citing lost or stuck funds, unauthorized debits, or outages over 24 hours.

High (C1, 3 fails): Add worked examples to the guidelines showing how to tell intent when a post mixes complaint, question and praise.

Medium (C4, 2 fails): Make spam rules work both ways. Scams must not pass as Inquiries or Praise (Post 23), and genuine price queries must not be tagged Spam (Post 1).

Lower (C2, 1 fail): Add Pidgin financial-phrase examples to the guidelines (Post 24).

Limitations
Synthetic data, one auditor, a sample of 31. Results show the method, not real-world error rates. With a second reviewer, I would have both audit independently, compare Pass/Fail calls, discuss each disagreement against the written guideline, and update the guideline where it was unclear.

Files
31_practice_posts_raw.csv: the 31 practice posts with Original_Label, Original_Flag, Audit decision and reason for every Fail
How to reproduce
Open 31_practice_posts_raw.csv
For each Post_ID, check the label and flag against C1 to C6 in the checklist above
Mark Pass or Fail per criterion and write a reason for every Fail
Count posts with at least one Fail to get the error rate
