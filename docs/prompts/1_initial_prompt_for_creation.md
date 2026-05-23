You are a principal software architect and AI tooling engineer.

Help me design and implement a production-quality AI-assisted document refinement engine.

# Product Vision

The product is NOT primarily a repository analysis tool.

The real product goal is:
- intelligently refine
- correct
- improve
- validate
- update

a target document using evidence gathered from a codebase/repository.

Repository scanning and codebase understanding are ONLY supporting mechanisms used to improve the document.

The system should behave like:
- an intelligent documentation reviewer
- an AI-powered document corrector
- a repository-aware document refinement engine

--------------------------------------------------
# PRIMARY INPUTS
--------------------------------------------------

The application receives:

1. A target document
2. A target repository/folder

The target document will ALWAYS be:
- .txt OR .md
- human-written
- focused on a specific topic

The FINAL OUTPUT must ALWAYS be:
- refined markdown (.md)
- structured and improved
- evidence-based
- repository-aware

--------------------------------------------------
# VERY IMPORTANT CORE CONCEPT
--------------------------------------------------

The target document title and topic determine the analysis strategy.

The system MUST:
1. Understand the document title
2. Infer the document purpose
3. Infer the document scope
4. Determine WHICH repository areas are relevant
5. Scan ONLY the relevant repository areas when possible

This is CRITICAL.

The system should NOT blindly scan:
- all files
- package.json
- pom.xml
- every config file
- every module

unless they are relevant to the target document topic.

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
# PRIMARY PRODUCT OBJECTIVE
--------------------------------------------------

The system should:

- understand the target document intent
- validate document accuracy
- identify outdated content
- identify incorrect claims
- identify missing important details
- suggest improvements
- rewrite unclear sections
- generate corrected markdown
- preserve useful human-written context when appropriate

The system should discuss:
- WHY something is inaccurate
- WHICH repository evidence supports the correction
- WHAT should be rewritten

--------------------------------------------------
# INITIAL PRODUCT FORM
--------------------------------------------------

DO NOT build:
- desktop app
- Electron app
- IDE plugin

Start with:

A terminal-executable CLI application.

Example:

doc-refiner refine \
  --doc ./docs/authentication.md \
  --repo ./backend-repo

The tool should:
- run in any terminal
- work inside any IDE terminal
- later become MCP-compatible naturally

--------------------------------------------------
# LONG-TERM ARCHITECTURE GOAL
--------------------------------------------------

Design the system so the core engine is reusable and headless.

The architecture should eventually support:

- CLI usage
- MCP server exposure
- AI agent integration
- IDE integration later if needed

DO NOT tightly couple:
- UI
- CLI
- repository access
- AI orchestration
- refinement logic

--------------------------------------------------
# IMPORTANT ARCHITECTURAL LAYERS
--------------------------------------------------

The system should have distinct layers:

1. Document Understanding Layer
- infer document purpose
- infer intended audience
- infer technical scope
- determine investigation strategy

2. Repository Intelligence Layer
- selectively inspect relevant repository areas
- analyze implementation details
- gather evidence
- summarize findings

3. Document Validation Layer
- compare document claims vs repository evidence
- detect inaccuracies
- detect omissions
- detect stale information

4. Refinement Layer
- rewrite sections
- improve markdown structure
- generate corrected markdown
- preserve useful context

5. Interface Layer
- CLI initially
- MCP exposure later

--------------------------------------------------
# CORE CAPABILITIES
--------------------------------------------------

## Document Intelligence
- title understanding
- topic inference
- semantic scope analysis
- audience inference
- markdown structure understanding

## Selective Repository Investigation
- targeted file discovery
- semantic search
- code relevance detection
- dependency tracing
- architecture inference only when needed

## Validation
- evidence-based corrections
- confidence scoring
- hallucination reduction
- traceable findings

## Refinement
- markdown rewriting
- section restructuring
- clarity improvement
- missing section generation
- outdated content replacement

--------------------------------------------------
# NON-FUNCTIONAL REQUIREMENTS
--------------------------------------------------

The system must:
- scale to medium/large repositories
- minimize hallucinations
- provide evidence-based reasoning
- avoid unnecessary repository scanning
- optimize token/context usage
- support incremental future improvements

Target ecosystems initially:
- Java
- JavaScript
- TypeScript
- Vue.js
- Node.js
- C#
- YAML
- Markdown

--------------------------------------------------
# RECOMMENDED TECH STACK
--------------------------------------------------

Please recommend and justify:

## Core Engine
- Node.js vs Python
- architecture style
- modularization strategy

## Repository Intelligence
- semantic search strategy
- AST parsing strategy
- repository indexing strategy
- selective scanning strategy

## AI Layer
- embeddings
- retrieval pipeline
- chunking strategy
- context orchestration
- prompt orchestration
- hallucination reduction

## CLI Design
- executable structure
- command design
- config management
- output formatting

## Future MCP Evolution
Design the architecture NOW so it can later expose MCP tools naturally.

Potential future MCP tools:
- refine_document()
- validate_document()
- explain_document_issue()
- summarize_repository_topic()
- find_related_repository_context()

But DO NOT build MCP-first.

Build a strong reusable refinement engine first.

--------------------------------------------------
# VERY IMPORTANT DESIGN PRINCIPLES
--------------------------------------------------

The system should behave intelligently like a senior engineer/reviewer.

It should:
- investigate based on document intent
- avoid unnecessary analysis
- avoid generic repository scanning
- gather evidence before rewriting
- preserve accurate human-written content
- explain corrections clearly

The repository is supporting evidence.
The document refinement is the real product.

--------------------------------------------------
# OUTPUT REQUIREMENTS
--------------------------------------------------

Provide:

1. High-level architecture
2. Recommended folder structure
3. Core engine design
4. CLI design
5. Repository investigation workflow
6. Document understanding workflow
7. Document refinement workflow
8. AI orchestration strategy
9. Hallucination reduction strategy
10. Incremental implementation roadmap
11. MVP scope recommendation
12. Future MCP migration strategy
13. Suggested prompt architecture
14. Suggested repository evidence strategy
15. Suggested markdown refinement strategy

Then:
- propose the best MVP implementation approach
- generate the initial project structure
- generate the first implementation milestones
- generate the first coding tasks

Act like a principal engineer designing a long-term AI tooling platform, not just a quick prototype.