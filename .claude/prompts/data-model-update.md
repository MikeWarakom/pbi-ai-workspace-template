# Prompt Template: Data Model Update

## Claude
```
@file .claude/skills/data-modeler.md
@file .ai-context/data-model.md
@file .ai-context/outputs/requirements.md
@file .ai-context/decisions.md

I need to update the data model.

Change requested: [describe what needs to change — new table, new column, new relationship]
Reason: [what requirement or discovery triggered this]
Source system info: [table/column names from the source if known]

Please:
1. Propose the model change with full table/column/relationship details
2. Flag any impacts on existing measures or relationships
3. Output the updated data-model.md section ready to paste
```

## GitHub Copilot
```
#file:.claude/skills/data-modeler.md
#file:.ai-context/data-model.md

Data model change needed: [describe change]
Reason: [why]
Source info: [table/column names from source]

Propose the change and show the updated data-model.md section.
```
