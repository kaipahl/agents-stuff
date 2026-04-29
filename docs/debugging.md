# Debugging

Before you attempt any fix, read these files: [file1, file2]. Explain what you think the root cause is and get my confirmation before making changes.

When debugging, exhaust diagnostic steps (read logs, check config, trace the actual code path) before attempting fixes. Avoid trial-and-error patching.

---

## Test-Driven debugging with iterative fix loops

I have a bug: [describe bug].  
Before attempting ANY fix, do this:
1. Investigate the codebase to understand the root cause — read relevant source files and configs,
2. Write a minimal test or script in ./debug-test.js that reproduces the exact failure,
3. Run it to confirm it fails,
4. Implement a fix,
5. Run the debug test again,
6. If it still fails, revert your fix, re-analyze, and try a different approach. Max 5 attempts. After each attempt log your hypothesis and result. Also run `npm test` to ensure no regressions. Do not ask me questions — work through this autonomously.
