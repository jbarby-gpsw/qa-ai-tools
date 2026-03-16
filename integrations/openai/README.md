# OpenAI Integration

This directory contains a pre-built bundle of all QA tool definitions formatted for use with the [OpenAI Assistants API](https://platform.openai.com/docs/assistants/overview) and the [Chat Completions API with function calling](https://platform.openai.com/docs/guides/function-calling).

## Files

| File | Description |
|------|-------------|
| [`openai-tools.json`](openai-tools.json) | All tools wrapped in `{"type": "function", "function": ...}` objects, ready to pass as the `tools` parameter |

## Quick Start

### Chat Completions API

```python
import json
from openai import OpenAI

client = OpenAI()
tools = json.load(open("integrations/openai/openai-tools.json"))

response = client.chat.completions.create(
    model="gpt-4o",
    tools=tools,
    messages=[
        {"role": "user", "content": "Generate pytest unit tests for this function: ..."}
    ],
)
```

### Assistants API

```python
import json
from openai import OpenAI

client = OpenAI()
tools = json.load(open("integrations/openai/openai-tools.json"))

assistant = client.beta.assistants.create(
    name="QA Assistant",
    instructions="You are a QA engineer. Use the available tools to help with testing tasks.",
    model="gpt-4o",
    tools=tools,
)
```

## Keeping in Sync

`openai-tools.json` is generated from the source definitions in `tools/*.json`. To regenerate it after adding or updating a tool:

```bash
node -e "
const fs = require('fs');
const path = require('path');
const toolDir = path.join(__dirname, '../../tools');
const files = fs.readdirSync(toolDir).filter(f => f.endsWith('.json') && f !== 'tool.schema.json');
const tools = files.map(f => ({
  type: 'function',
  function: JSON.parse(fs.readFileSync(path.join(toolDir, f), 'utf8'))
}));
fs.writeFileSync(
  path.join(__dirname, 'openai-tools.json'),
  JSON.stringify(tools, null, 2)
);
console.log('Generated', tools.length, 'tools');
"
```
