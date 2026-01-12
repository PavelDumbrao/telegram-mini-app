# Cline Automation Rules

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
