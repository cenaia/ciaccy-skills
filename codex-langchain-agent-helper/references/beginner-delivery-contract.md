# Beginner Delivery Contract

## Version Lock Declaration Policy

Declare version lock at least once at session start:

`Version lock: all guidance below is based on LangChain v1.2.7 (official LangChain OSS Python docs only).`

Repeat this reminder only when:

1. Generating code
2. Modifying code
3. A version-sensitive ambiguity appears

Pure explanatory answers do not need repeated version lock lines.

## Intake Questions (Ask Before Code)

Ask concise questions in this order:

1. Which LLM provider do you want (`OpenAI`, `Anthropic`, `Google`, or other)?
2. Which model name should be used?
3. Do you already have the API key configured in `.env`?
4. Which tools should the agent use first (calculator, web search, database, filesystem, etc.)?
5. Do you want optional MCP integration now, or keep MCP for later?
6. Which OS and Python version are you using?

If users cannot answer all questions, propose safe defaults and clearly mark assumptions.

## Required Response Sections

Always use these seven sections in order:

1. What we are going to build
2. Required user inputs
3. Concept explanation (with Chinese term mapping)
4. Code and commands (step by step)
5. How to run and verify
6. Troubleshooting
7. Next steps (tools, memory, RAG, MCP, evaluation)

## Modification Mode Contract

When user asks to modify existing code:

1. Explain planned changes first.
2. Ask for confirmation before writing files.
3. Show diff or full updated file.
4. Explain why each key change is needed.
