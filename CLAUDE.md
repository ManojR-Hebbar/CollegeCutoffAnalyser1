# Rules

## Before making any code changes
1. Describe exactly what you plan to change (which file, what you will add or modify).
2. Wait for explicit confirmation ("yes", "go ahead", etc.) before touching any file.
3. If the user provides a format or specification, confirm you understood it correctly and ask permission to proceed — do not treat the specification itself as a go-ahead.
4. This applies even when auto-accept / auto-edit mode is ON. Auto-accept is never approval — always pause, describe, get approval, then edit.
5. Describe the change as a plain-language description of the intended outcome — NOT code, not a diff. For any text/wording change, show the exact final text and get explicit approval before applying it. A shorthand or direction from the user is not approval of the specific wording.
6. When asking for approval or a decision, present concrete options labeled A / B / C (etc.), and mark the recommended one.
7. When the user provides wording or text to apply, treat it as guidance — not final copy. Their input may be vague, contain typos, or be only a partial/guiding statement. Restate the exact, cleaned-up final text and get explicit confirmation before applying it.

## Changing table content
8. Whenever content in a table is added, deleted, or modified — a DB table, or any config that
   populates one (course codes, categories, keyword groups, abbreviations, typo fixes) — present the
   change **as a table** and get explicit consent before applying it. The table must show:
   - the exact rows being added / removed / changed, with before → after values;
   - **which pipeline Step performs the change**, and which file it lives in;
   - which board/exam it affects (KEA, ComedK, or both).
9. Never invent user-visible content — course names, abbreviations, category names, keyword-group
   labels or codes. If a value isn't supplied by the user or taken from an official source, say so
   plainly and ask, rather than filling the gap with a plausible guess.
