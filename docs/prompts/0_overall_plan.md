# The overall plan

## What we wish to build is a structured decision process that:

1. Understand document intent (from title + content)
2. Infer scope (what matters / what doesn’t)
3. Plan minimal repo exploration strategy
4. Gather only relevant evidence
5. Validate claims vs evidence
6. Classify issues:

   * incorrect
   * outdated
   * missing
   * ambiguous
7. Rewrite document in improved Markdown
8. Provide explanation + evidence mapping

This is exactly a **skill / playbook / reasoning system**.

## Mental Model for our Project

### Phase 1 (NOW)

You are building:

> 🧠 **Agent Skill + Workflow Engine**

This includes:

* document understanding logic
* repo reasoning strategy
* validation logic
* refinement logic
* prompt orchestration

This becomes your **core engine**

---

### Phase 2

You wrap it into:

> ⚙️ CLI tool (your current plan)

Example:

```bash
doc-refiner refine --doc x.md --repo y/
```

This CLI simply triggers the skill.

---

### Phase 3

You add:

> 📦 MCP server layer

Now your same engine becomes callable by:

* Claude Code
* Cursor
* other AI agents

without rewriting logic.

---
