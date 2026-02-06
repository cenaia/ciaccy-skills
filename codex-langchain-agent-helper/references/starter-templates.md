# Starter Templates (LangChain v1.2.7)

Use these templates for beginner-first projects.
Agent builder entrypoints may change across versions. Do not treat any single function name as fixed; use the pattern explicitly recommended on the v1.2.7 official Agents docs page.

## 1) Minimal Project Structure

```text
agent_starter/
  main.py
  .env.example
  requirements.txt
```

## 2) Dependencies (pip)

```bash
python -m pip install -U \
  langchain==1.2.7 \
  langchain-openai \
  python-dotenv
```

Optional MCP dependencies (only when needed):

```bash
python -m pip install -U langchain-mcp-adapters fastmcp
```

## 3) `.env.example`

```dotenv
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-4.1-mini
```

## 4) `main.py` (pseudo-code, replace with v1.2.7 official Agent pattern)

```python
from __future__ import annotations

import os
from typing import Any

from dotenv import load_dotenv
from langchain.tools import tool
from langchain_openai import ChatOpenAI

load_dotenv()


@tool
def add_numbers(a: int, b: int) -> int:
    """Return the sum of two integers."""
    return a + b


def build_agent():
    model_name = os.getenv("OPENAI_MODEL", "gpt-4.1-mini")
    model = ChatOpenAI(model=model_name, temperature=0)
    # pseudo-code:
    # return AGENT_BUILDER_FROM_OFFICIAL_V127_DOCS(
    #     model=model,
    #     tools=[add_numbers],
    #     system_prompt="You are a beginner-friendly assistant.",
    # )
    raise NotImplementedError("Replace with v1.2.7 official Agent builder pattern")


def extract_text(result: dict[str, Any]) -> str:
    messages = result.get("messages", [])
    if not messages:
        return str(result)
    last = messages[-1]
    content = getattr(last, "content", "")
    if isinstance(content, list):
        parts = []
        for item in content:
            if isinstance(item, dict) and "text" in item:
                parts.append(str(item["text"]))
            else:
                parts.append(str(item))
        return " ".join(parts).strip()
    return str(content)


def main() -> None:
    if not os.getenv("OPENAI_API_KEY"):
        raise RuntimeError("Missing OPENAI_API_KEY. Add it to .env first.")

    agent = build_agent()
    user_input = input("请输入问题: ").strip() or "请调用 add_numbers 计算 12 + 30"
    result = agent.invoke({"messages": [{"role": "user", "content": user_input}]})

    print("\nAgent 输出:\n")
    print(extract_text(result))


if __name__ == "__main__":
    main()
```

## 5) Verification Prompt

Use a prompt that strongly encourages tool use:

```text
请调用 add_numbers 工具计算 19 + 23，并只输出最终数字。
```

## 6) Optional MCP Example (Runnable only if MCP server is available)

```python
import asyncio

# pseudo-code:
# - confirm MCP transport/server config first
# - use v1.2.7 official MCP integration docs to select concrete classes/functions


async def main() -> None:
    raise NotImplementedError("Fill from official v1.2.7 MCP docs after config is confirmed")


if __name__ == "__main__":
    asyncio.run(main())
```

When MCP server details are unknown, keep MCP code as `pseudo-code` and ask for server transport/config first.
