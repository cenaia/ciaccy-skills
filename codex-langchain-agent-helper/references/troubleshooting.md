# Beginner Troubleshooting (LangChain Agent Setup)

Use this checklist when users report setup failures.

## 1) Import Errors

Typical errors:

- `ModuleNotFoundError: No module named 'langchain'`
- `ModuleNotFoundError: No module named 'langchain_openai'`
- `ModuleNotFoundError: No module named 'dotenv'`

Fix steps:

1. Confirm active Python interpreter and virtual environment.
2. Reinstall dependencies in that environment:

```bash
python -m pip install -U langchain==1.2.7 langchain-openai python-dotenv
```

3. Verify packages:

```bash
python -m pip show langchain langchain-openai python-dotenv
```

## 2) `.env` / API Key Issues

Typical errors:

- Missing key errors
- Authentication failures from model provider

Fix steps:

1. Confirm `.env` exists next to `main.py`.
2. Confirm key name matches provider requirements (for example `OPENAI_API_KEY`).
3. Confirm `load_dotenv()` is called before model creation.
4. Print a safe check (never print full secrets):

```python
import os
print("OPENAI_API_KEY set:", bool(os.getenv("OPENAI_API_KEY")))
```

## 3) Model Configuration Errors

Typical errors:

- Unknown or unavailable model name
- Region/account access denied

Fix steps:

1. Use a known available model in `.env`.
2. Validate provider SDK setup and account permissions.
3. Retry with a smaller/cheaper known model first to isolate config issues.

## 4) Agent Runs But Tool Not Called

Symptoms:

- Agent answers directly without using expected tool

Fix steps:

1. Strengthen prompt to explicitly request tool use.
2. Use deterministic settings (`temperature=0`) for easier debugging.
3. Verify tool docstring clearly describes when to call the tool.
4. Test with a prompt that strongly requires computation.

## 5) MCP Integration Errors (Optional)

Typical issues:

- MCP client cannot connect
- Tool list from MCP server is empty

Fix steps:

1. Confirm MCP server process starts independently.
2. Verify transport config (`stdio` vs `streamable_http`) and command/args.
3. Test non-MCP baseline first, then add MCP as a second step.
4. If server details are incomplete, provide `pseudo-code` and request missing config.

## 6) Security And Privacy Reminders (lightweight)

- Do not put API keys directly in source code.
- Do not commit `.env` to git; add it to `.gitignore`.
- Redact secrets/tokens/user data before sharing logs.
