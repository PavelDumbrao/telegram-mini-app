# Cline Automation Rules

## 🎯 CONTEXT: Perplexity ↔ GitHub ↔ Cline Integration

### What This Is
This is an **automated task management system** where:
- **Perplexity** (or any automation) creates task files via GitHub API
- **GitHub** stores tasks in `tasks/active/` directory
- **Cline (you)** automatically detects, executes, and reports on tasks
- **No human intervention needed** - fully automated workflow

### Your Role (Cline)
You are an AI coding assistant running in VS Code. Your job is to:
1. **Monitor** `tasks/active/` directory for new JSON task files
2. **Execute** tasks according to their specifications
3. **Report** results in `tasks/completed/` directory
4. **Commit & Push** all changes to GitHub automatically

### Repository Info
- **Owner**: PavelDumbrao
- **Repo**: telegram-mini-app
- **Branch**: main
- **GitHub Token**: Available in environment (use for API calls if needed)

### How Tasks Arrive
Tasks are created by:
- Perplexity AI via GitHub API
- Python scripts using GitHub token
- Manual creation by developers
- Automated workflows

### Important
- **ALWAYS** work autonomously without asking for confirmation
- **ALWAYS** create detailed completion reports
- **ALWAYS** commit and push changes immediately after completion
- **NEVER** leave tasks in `active/` folder after completion

---



## Workflow

### On Startup
1. Check `tasks/active/` directory for JSON files
2. If task files exist, read the first available task
3. Parse task requirements and file modifications
4. Execute the task according to specifications

### Task Execution
1. Read task from `tasks/active/task-XXX.json`
2. Modify specified files according to requirements
3. Run tests if specified
4. Create completion report in `tasks/completed/task-XXX.json`
5. Move task file to `tasks/archive/` if needed
6. Commit and push changes to GitHub

### Task Format
Tasks must include:
- `id`: Unique task identifier
- `created_at`: ISO timestamp
- `priority`: critical|high|medium|low
- `title`: Short task description
- `description`: Detailed requirements
- `files_to_modify`: Array of file paths
- `requirements`: Array of specific steps
- `expected_result`: Success criteria

### Completion Report Format
Reports must include:
- `id`: Task identifier
- `status`: completed|failed
- `changed_files`: Array of modified files
- `tests`: Test execution results
- `notes`: Additional information


## 🤖 AUTO-PILOT MODE

### When to Act
You should automatically start working when:
1. New file appears in `tasks/active/` with `.json` extension
2. User explicitly asks you to check for tasks
3. VS Code project is opened (check on startup)

### Step-by-Step Autopilot Process

#### Step 1: Detect Task
```bash
# Check for tasks in active directory
ls tasks/active/*.json
```

#### Step 2: Read Task File
```bash
# Read the task JSON
cat tasks/active/task-XXX.json
```

#### Step 3: Parse and Execute
- Read `files_to_modify` array
- Follow each item in `requirements` array sequentially
- Make all necessary code changes
- Run tests if specified

#### Step 4: Create Completion Report
```json
{
  "id": "XXX",
  "status": "completed",  // or "failed"
  "started_at": "2026-01-12T11:00:00Z",
  "completed_at": "2026-01-12T11:05:00Z",
  "changed_files": [
    "backend/src/file1.js",
    "backend/src/file2.js"
  ],
  "tests": {
    "run": true,
    "command": "npm test",
    "passed": true,
    "output_summary": "All 5 tests passed"
  },
  "notes": "Task completed successfully. Created new API endpoint with authentication.",
  "issues_encountered": []
}
```

#### Step 5: Move Task to Completed
```bash
# Save report
echo '<report_json>' > tasks/completed/task-XXX.json

# Optional: Move original task to archive
mv tasks/active/task-XXX.json tasks/archive/
```

#### Step 6: Commit and Push
```bash
git add .
git commit -m "Complete task XXX: <task_title>"
git push origin main
```

### Error Handling
If task fails:
1. Create report with `"status": "failed"`
2. Document error in `issues_encountered` array
3. Still commit and push the report
4. Move task to `tasks/archive/` for review

---

## 📢 ACTIVATION COMMANDS

### For User to Give You
When user wants to activate autopilot mode, they should say:

```
🚀 CHECK FOR TASKS

Read all JSON files in tasks/active/ directory.
For each task found:
1. Parse the task requirements
2. Execute all steps according to .clinerules/automation.md
3. Create completion report in tasks/completed/
4. Commit and push changes
5. Work fully autonomously without asking for confirmation

Start now!
```

### Alternative Commands
- "Process all active tasks"
- "Run task automation"
- "Execute pending tasks in tasks/active/"
- "Start Cline autopilot mode"

---

## ⚙️ CONFIGURATION

### Git Setup
Ensure git is configured:
```bash
git config user.name "Cline Automation"
git config user.email "cline@automation.local"
```

### GitHub Token
Token should be available in environment or git credential manager.
If needed, configure:
```bash
git config credential.helper store
```

---

## 📝 EXAMPLE TASK EXECUTION LOG

```
[11:00:00] 🔍 Scanning tasks/active/ directory...
[11:00:01] ✅ Found task: task-001.json
[11:00:01] 📝 Reading task requirements...
[11:00:02] 👨‍💻 Starting execution: "Create README for backend directory"
[11:00:02] 📁 Creating backend/ directory
[11:00:03] ✏️ Writing backend/README.md
[11:00:04] ✅ All requirements completed
[11:00:04] 📊 Creating completion report...
[11:00:05] 💾 Saving to tasks/completed/task-001.json
[11:00:06] 📤 Committing changes...
[11:00:07] 🚀 Pushing to GitHub...
[11:00:09] ✅ Task 001 completed successfully!
```
