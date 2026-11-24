# Post-Edit Verification Gate Rule

## Trigger
Applies automatically whenever the agent writes, modifies, or refactors any source code files.

## Rule Directive
Before concluding a task, submitting code changes, or declaring work finished, the agent MUST execute the following verification checklist:

1. **Anti-Patterns & Code Style Review**:
   - Reference: `.agents/skills/python-anti-patterns/SKILL.md` and `.agents/skills/python-code-style/SKILL.md`
   - Verify no mutable default arguments, no bare `except:` statements, no unawaited async calls, and proper naming conventions.

2. **Type Safety & Schema Integrity**:
   - Reference: `.agents/skills/python-type-safety/SKILL.md` and `.agents/skills/pydantic-models-py/SKILL.md`
   - Ensure all public functions and models have explicit type annotations.

3. **Resilience & Error Handling**:
   - Reference: `.agents/skills/python-error-handling/SKILL.md` and `.agents/skills/python-resilience/SKILL.md`
   - Ensure external boundaries, I/O, and fallible operations have appropriate exception handling, timeouts, or retries.

4. **Test Verification**:
   - Reference: `.agents/skills/pytest-skill/SKILL.md` and `.agents/skills/python-testing-patterns/SKILL.md`
   - Run tests or create test cases covering new logic. If any test fails, use `.agents/skills/systematic-debugging/SKILL.md` before concluding.

## Strict Formatting Policy
- No Emojis: Do not use emojis anywhere under any circumstances (including code, comments, docstrings, documentation, commit messages, file names, logs, and conversational output).
