You are a principal Claude Code tooling engineer.

Help me design and implement a production-quality Claude Code agent skill for AI-assisted document refinement.

--------------------------------------------------
# WHAT WE ARE BUILDING
--------------------------------------------------

A Claude Code agent skill — a markdown instruction file that Claude Code executes
when invoked via a slash command inside a Claude Code session.

The skill leverages Claude Code's built-in tools and Claude's native reasoning.
There is NO standalone LLM API, NO SDK integration, NO API key configuration.
Claude IS the intelligence. Claude Code's tools ARE the infrastructure.

Invoked like:

/doc-refiner --doc ./docs/authentication.md --repo ./backend-repo

The skill file will live at:

.claude/skills/doc-refiner/SKILL.md

--------------------------------------------------
# PRIMARY INPUTS
--------------------------------------------------

The skill receives two arguments:

1. --doc   path to the target document (.txt or .md)
2. --repo  path to the target repository or folder

The target document will ALWAYS be:
- .txt OR .md
- human-written
- focused on a specific topic, usually clarified from its title

The target repository/folder will ALWAYS be:
- the source of ground truth about the document's topic
- contains files that are relevant AND irrelevant to the document topic
- the skill must read only the relevant ones

--------------------------------------------------
# VERY IMPORTANT CORE CONCEPT
--------------------------------------------------

The target document title and topic determine the repository exploration strategy.

The skill MUST:
1. Read the target document first
2. Understand its title
3. Infer the document purpose
4. Infer the document scope
5. Determine WHICH repository areas/files are relevant to that topic
6. Use Glob and Grep to discover and read ONLY the relevant files

This is CRITICAL.

The skill should NOT blindly read:
- all files
- package.json / pom.xml / build configs
- every module

unless they are directly relevant to the document topic.

Examples:

If the document is:
- "Authentication Flow"
→ inspect auth modules, middleware, JWT config, login APIs

If the document is:
- "Playwright E2E Strategy"
→ inspect test folders, playwright config, CI pipeline, reporting setup

If the document is:
- "Vue I18n Implementation"
→ inspect frontend i18n usage and locale structure

The document purpose drives repository exploration.

--------------------------------------------------
# SKILL WORKFLOW
--------------------------------------------------

The skill executes in three sequential phases.

## Phase 1 — Analysis (silent, no user output yet)

1. Read the target document (Read tool)
2. Identify the topic, purpose, and scope from the title and content
3. Use Glob and Grep to discover relevant files in the target repository
4. Read relevant repository files (Read tool)
5. Identify all of the following:
   - inaccurate or incorrect claims
   - outdated content
   - missing important details
   - unclear or poorly written sections
   - content that is correct and should be preserved

## Phase 2 — Discussion (interactive, requires user response before proceeding)

6. Present a structured summary of findings:
   - WHAT is inaccurate or missing
   - WHY it is wrong (reasoning)
   - WHICH repository file/evidence supports the correction
7. Raise any uncertainties and ask the user for clarification
8. List all planned improvements and ask the user to confirm before writing output

The skill MUST NOT write any output file before the user confirms in Phase 2.

## Phase 3 — Output (after user confirmation)

9. Rewrite the document as a refined markdown file
10. Write the output file using the Write tool
11. Output file naming: {original-filename}-refined.md in the same directory as --doc

--------------------------------------------------
# OUTPUT FILE REQUIREMENTS
--------------------------------------------------

The refined output file must be:
- Format: markdown (.md)
- Structured and well-organized
- Evidence-based (corrections tied to repository findings)
- Good human readability
- Preserving useful human-written context where it is accurate and relevant

--------------------------------------------------
# CLAUDE CODE TOOLS TO USE
--------------------------------------------------

| Tool  | Purpose                                              |
|-------|------------------------------------------------------|
| Read  | Read the target document and relevant repo files     |
| Glob  | Discover files in the repository by name pattern     |
| Grep  | Search for specific symbols, keywords, or patterns   |
| Write | Output the refined markdown file                     |

--------------------------------------------------
# WHAT WE ARE NOT BUILDING
--------------------------------------------------

For this current task, we DO NOT build:
- A standalone CLI application
- An LLM SDK or API integration
- A configuration file for API keys or model names
- Any backend server or MCP server

--------------------------------------------------
# LONG-TERM GOAL
--------------------------------------------------

This skill is the working prototype of the document refinement engine.

Once the workflow is validated through skill usage, the same logic can be
extracted into a standalone CLI or MCP server in a future task. The skill
is the design specification made executable — not a throwaway prototype.
