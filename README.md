# telegram-mini-app
Telegram Mini App with Cline automation - project management via GitHub tasks


## Project Structure

```
telegram-mini-app/
├── tasks/
│   ├── active/          # Active tasks for Cline to process
│   ├── completed/       # Completed task reports
│   └── archive/         # Archived old tasks
├── scripts/
│   ├── check-tasks.js          # Script to check for new tasks
│   ├── cline-read-task.js      # Script for Cline to read tasks
│   └── cline-write-report.js   # Script to write completion reports
├── .clinerules/
│   └── automation.md    # Cline automation rules and workflow
├── examples/
│   ├── perplexity-create-task.py    # Example: Create task via Perplexity
│   └── perplexity-check-result.py   # Example: Check task results
├── backend/
│   └── src/             # Backend application code
├── .gitignore
└── README.md
```

## Setup

### 1. Repository Setup
Repository: `PavelDumbrao/telegram-mini-app`
Branch: `main`

### 2. GitHub Token
Create a GitHub Personal Access Token with:
- `repo` (full control)
- `workflow` permissions

Generate at: https://github.com/settings/tokens

### 3. Workflow

#### Creating Tasks (via Perplexity or manually)
1. Create JSON file in `tasks/active/task-XXX.json`
2. Cline automatically detects and processes the task
3. Task results appear in `tasks/completed/task-XXX.json`

#### Task Format Example
```json
{
  "id": "001",
  "created_at": "2026-01-12T10:30:00Z",
  "priority": "critical",
  "title": "Fix HMAC validation",
  "description": "Remove timestamp check, keep hash validation",
  "files_to_modify": ["backend/src/utils/crypto.js"],
  "requirements": [
    "Find validateInitData() function",
    "Remove timestamp validation",
    "Keep hash check only"
  ],
  "expected_result": "All tests pass with hash-only validation"
}
```

## Integration

This project enables seamless automation between:
- **Perplexity** → Task creation via GitHub API
- **GitHub** → Task storage and version control  
- **Cline (VS Code)** → Automated task execution

## Next Steps

1. Create GitHub token
2. Configure local VS Code with Cline
3. Test with sample task
4. Integrate with Perplexity workflows
