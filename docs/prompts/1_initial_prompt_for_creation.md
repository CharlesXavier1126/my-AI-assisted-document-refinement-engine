You are a principal software architect and AI tooling engineer.

Help me design and implement a production-quality AI-assisted document refinement engine. (that will later be exposed via CLI and MCP. Future work, not the focus of current task)

# Product Vision
The product goal is:
- intelligently refine target document
- correct any missing or inaccurate content
- improve format and expression
- validate improvement before update
- update/rewrite target document

Here are more details:

--------------------------------------------------
# PRIMARY INPUTS
--------------------------------------------------

The application receives:

1. A target document
2. A target repository/folder

The target document will ALWAYS be:
- .txt OR .md
- human-written
- focused on a specific topic, usually revealed from its title or its content

The target repository/folder will ALWAYS be:
- the path where this system can gather all the required information about the target document
- this system should read the files within this path which are relevant to the topic the target document is about
- system can ignore the files within this path which are totally irrelevent to the target document topic

The FINAL OUTPUT must ALWAYS be:
- firstly discuss with user about uncertainties if any
- then confirm with user about all the key improvements system is about to make
- finally output a file that is:
  - refined markdown (.md)
  - structured and improved
  - evidence-based
  - good human readability

--------------------------------------------------
# VERY IMPORTANT CORE CONCEPT
--------------------------------------------------

The target document title and topic determine the analysis strategy.

The system MUST:
1. Understand the document's title
2. Infer the document's topic and purpose
3. Infer the document scope
4. Determine WHICH repository areas/files are relevant
5. Scan ONLY the relevant repository areas/files when possible

This is CRITICAL.

The system should NOT blindly scan:
- all files

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
- Output a total token usage after whole process is done

The system should discuss:
- WHY something is inaccurate
- WHICH repository evidence supports the correction
- WHAT should be rewritten

How the system can achive this:
- The system will make api request to use LLM in layers like
  - intelligently refine
  - correct
  - improve
  - validate
  - update
- Try to minimize the token usage
- Parameters like LLM model name, API key are configurable in a configuration file

--------------------------------------------------
# INITIAL PRODUCT FORM
--------------------------------------------------

For this current task, we DO NOT build:
- desktop app
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
