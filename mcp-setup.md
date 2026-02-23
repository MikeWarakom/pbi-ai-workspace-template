# MCP Setup Guide — Power BI Modeling MCP Server

## What This Gives You
Instead of manually maintaining `data-model.md`, the MCP server connects
directly to your live Power BI model and lets AI agents read and write
to it in real time.

```
Before MCP:
You update data-model.md manually → Claude reads it → suggests DAX → you paste it

After MCP:
MCP connects to live PBI Desktop → Claude reads live model → writes DAX directly into model
```

---

## Prerequisites
- VS Code installed
- GitHub Copilot extension installed (recommended client)
- Power BI Desktop installed
- Your `.pbix` open in Power BI Desktop during sessions
OR
- Your report saved as PBIP format (`.pbip`)
OR
- A Fabric workspace with your semantic model

---

## Installation

### Option A — VS Code Extension (Recommended)
1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X`)
3. Search: `Power BI Modeling MCP`
4. Install the extension by Microsoft (publisher: `analysis-services`)
5. Open GitHub Copilot Chat
6. Confirm `powerbi-modeling-mcp` appears in the MCP tools list

### Option B — Manual Install (for Claude or other MCP clients)
1. Download the `.vsix` from:
   `https://marketplace.visualstudio.com/_apis/public/gallery/publishers/analysis-services/vsextensions/powerbi-modeling-mcp/0.1.8/vspackage?targetPlatform=win32-x64`
2. Rename downloaded file from `.vsix` to `.zip`
3. Unzip to a folder e.g. `C:\MCPServers\PowerBIModelingMCP`
4. Run `\extension\server\powerbi-modeling-mcp.exe`
5. Add to your MCP client config (see below)

**MCP config for VS Code (`mcp.json` or workspace settings):**
```json
{
  "servers": {
    "powerbi-modeling-mcp": {
      "type": "stdio",
      "command": "C:\\MCPServers\\PowerBIModelingMCP\\extension\\server\\powerbi-modeling-mcp.exe",
      "args": ["--start"],
      "env": {}
    }
  }
}
```

---

## Connecting to Your Model

### Power BI Desktop (most common)
Open your `.pbix` in Power BI Desktop first, then in Copilot Chat:
```
Connect to '[YourFileName]' in Power BI Desktop
```

### PBIP Project Files
```
Open semantic model from PBIP folder '[path to your /definition or /TMDL folder]'
```

### Fabric Workspace
```
Connect to semantic model '[Model Name]' in Fabric Workspace '[Workspace Name]'
```

---

## What You Can Now Ask AI to Do

### Read your model (replaces data-model.md manual updates)
```
List all tables and columns in my model
Show me all measures and their DAX
Generate a data-model.md file documenting my entire semantic model
```

### Write DAX directly into your model
```
#file:.claude/skills/dax-expert.md
Create a measure called 'Sales YTD' using DATESYTD on the Calendar table
```

### Validate DAX
```
Execute this DAX query and show me the results:
EVALUATE SUMMARIZE(Fact_Sales, Dim_Customer[Region], "Total", [Total Sales])
```

### Bulk operations
```
Rename all measures to use Title Case
Add descriptions to all measures explaining their business logic
Apply naming conventions from #file:.ai-context/conventions.md to the entire model
```

### Generate documentation automatically
```
#file:.claude/skills/documenter.md
Generate a complete data-model.md documenting all tables, columns, 
relationships and measures in my model
```

---

## Recommended Workflow with MCP

### Session Start
```
Connect to '[YourFile]' in Power BI Desktop
@file .claude/session-handoff.md
Continuing from last session. Today I want to [task].
```

### DAX Task (MCP writes directly — no copy/paste)
```
@file .claude/skills/dax-expert.md
Create a measure for [describe metric].
Follow the skill file rules. Write it directly into the _Measures table.
```

### Sync data-model.md from live model (run periodically)
```
@file .claude/skills/data-modeler.md
Read the current model structure and update data-model.md 
to reflect the current state of all tables, columns, and measures.
Output the full updated data-model.md ready to save.
```

---

## Important Warnings

⚠️ **Always back up your model** before letting AI write directly to it.
The MCP server will ask for confirmation before the first write operation.

⚠️ **Copilot is the recommended client.** For Claude MCP support in VS Code,
use the manual install option above.

⚠️ **Public Preview** — this tool is still evolving. Check the
[GitHub repo](https://github.com/microsoft/powerbi-modeling-mcp) for updates.

---

## Safe Mode Option
If you want AI to read but not write to your model:
```json
"args": ["--start", "--readonly"]
```

## Skip Confirmation (advanced — only if you have backups)
```json
"args": ["--start", "--skipconfirmation"]
```

---

## Impact on Your Template Files

| File | With MCP |
|------|---------|
| `data-model.md` | Auto-generate from live model instead of manual updates |
| `skills/dax-expert.md` | Still used — provides quality rules for AI to follow |
| `session-handoff.md` | Still used — MCP has no memory between sessions |
| `decisions.md` | Still used — MCP doesn't know what was agreed |
| `prompts/dax-task.md` | Still used — but output goes directly to model |

---

## Useful MCP Prompts (built-in)
Type `/` in Copilot Chat to access:
- `/ConnectToPowerBIDesktop` — connect to open Desktop file
- `/ConnectToPBIP` — connect to PBIP folder
- `/ConnectToFabric` — connect to Fabric workspace
- `/CreateDAXQuery` — generate DAX from natural language
- `/AnalyzeDAXQuery` — performance analysis
