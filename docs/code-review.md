# Code Review

Collect all files that were changed but not committed.

Perform a comprehensive and honest review of these files against 
- coding standards
- Best Practices, 
- Readability
- Clarity
- Project documentations and plans

Spawn a separate sub-task for each changed file or logical group of files.  
Give each sub-task sufficient informations for a correct evaluation, including the scope of the task and existing tests. 

Each sub-task should:
- read the file
- not make any assumptions about other files without having read the file
- check if the findings are real problems compared to the scope or only theoretical problems. If you don't have any solid proofs for problems, ignore theoretical problems as findings.
- list findings by severity (critical/warning/suggestion),
- include code snippets.

After all sub-tasks complete, consolidate into a single review report at ./.reviews/review-claude-YYYY-MM-DD.md with a summary table and detailed findings sorted by severity.

Run the review without asking me any questions.
