# myskills — Agent Skills Repository & Operational Playbook

A structured repository of production-ready skills, agent configurations, and an automated post-code verification filter for AI coding assistants (Google Antigravity, Claude Code, Cursor, Codex).

---

## Overview

This repository provides:
- **49 Domain Skills**: Modular guidelines and templates located in `.agents/skills/` covering Python, FastAPI, RAG, Vector Databases, Testing, Security, and Observability.
- **Agent Playbook (`AGENTS.md`)**: A centralized reference manual ("Help Book") mapping every skill to its domain and trigger condition.
- **Mandatory Post-Code Verification Gate**: A 4-stage quality filter that forces agents to verify syntax, type safety, resilience, and tests before concluding any coding task.
- **Workspace Rules (`.agents/rules/post-edit-gate.md`)**: Automated workspace rules enforcing code quality checks and formatting standards.

---

## Setup & Skill Synchronization

### 1. Clone This Repository

```bash
git clone https://github.com/Sudhanshu3011/myskills.git
cd myskills
```

---

## How to Get Skills From This Repository

If you are a developer looking to integrate these 49 skills, the `AGENTS.md` playbook, and the post-code verification gate into your own project, use the methods below.

---

### Method 1: Install All Skills Into Your Existing Project (Recommended)

Run the following command from the root directory of your own project. It clones this repository into a temporary directory, copies the complete `.agents/` folder and `AGENTS.md` directly into your workspace, and cleans up the temporary files.

#### Windows (PowerShell)

```powershell
# Run from your project root:
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git temp_myskills; `
Copy-Item -Path temp_myskills\.agents -Destination . -Recurse -Force; `
Copy-Item -Path temp_myskills\AGENTS.md -Destination . -Force; `
Remove-Item -Recurse -Force temp_myskills
```

#### Linux / macOS (Bash)

```bash
# Run from your project root:
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git /tmp/myskills && \
mkdir -p .agents && \
cp -r /tmp/myskills/.agents/* .agents/ && \
cp /tmp/myskills/AGENTS.md . && \
rm -rf /tmp/myskills
```

---

### Method 2: Install Only Selected Skills

If you only need specific skills (for example, `fastapi-pro` and `faiss`) inside your project:

#### Windows (PowerShell)

```powershell
# Clone temporarily
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git temp_myskills

# Ensure destination exists
$dest = ".agents\skills"
if (!(Test-Path $dest)) { New-Item -ItemType Directory -Force -Path $dest }

# List the specific skills you want
$selectedSkills = @("fastapi-pro", "faiss", "python-anti-patterns", "pytest-skill")

foreach ($s in $selectedSkills) {
    if (Test-Path "temp_myskills\.agents\skills\$s") {
        Copy-Item -Path "temp_myskills\.agents\skills\$s" -Destination "$dest\$s" -Recurse -Force
        Write-Host "Installed: $s"
    } else {
        Write-Warning "Skill not found: $s"
    }
}

# Clean up
Remove-Item -Recurse -Force temp_myskills
```

#### Linux / macOS (Bash)

```bash
# Clone temporarily
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git /tmp/myskills

# Ensure destination exists
DEST=".agents/skills"
mkdir -p "$DEST"

# List the specific skills you want
SELECTED_SKILLS=("fastapi-pro" "faiss" "python-anti-patterns" "pytest-skill")

for s in "${SELECTED_SKILLS[@]}"; do
  if [ -d "/tmp/myskills/.agents/skills/$s" ]; then
    cp -r "/tmp/myskills/.agents/skills/$s" "$DEST/$s"
    echo "Installed: $s"
  else
    echo "Skill not found: $s"
  fi
done

# Clean up
rm -rf /tmp/myskills
```

---

### Method 3: Use With Claude Code (`.claude/skills`)

If your agent tool expects skills inside `.claude/skills` instead of `.agents/skills`, map the destination folder accordingly:

#### Windows (PowerShell)

```powershell
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git temp_myskills
if (!(Test-Path ".claude\skills")) { New-Item -ItemType Directory -Force -Path ".claude\skills" }
Copy-Item -Path temp_myskills\.agents\skills\* -Destination ".claude\skills\" -Recurse -Force
Remove-Item -Recurse -Force temp_myskills
```

#### Linux / macOS (Bash)

```bash
git clone --depth 1 https://github.com/Sudhanshu3011/myskills.git /tmp/myskills
mkdir -p .claude/skills
cp -r /tmp/myskills/.agents/skills/* .claude/skills/
rm -rf /tmp/myskills
```

---

## Upstream Synchronization (Maintainer Guide)

For maintainers who want to re-sync or pull updated core skills from upstream sources (`wshobson/agents` and `KalarisLabs/research-agent-skills`):

#### Windows (PowerShell)

```powershell
$dest = ".agents\skills"
if (!(Test-Path $dest)) { New-Item -ItemType Directory -Force -Path $dest }

$skills = @(
    "python-code-style", "python-anti-patterns", "python-type-safety",
    "python-project-structure", "python-error-handling", "python-configuration",
    "python-testing-patterns", "async-python-patterns", "python-resilience",
    "python-observability", "rag-implementation", "embedding-strategies",
    "hybrid-search-implementation", "vector-index-tuning"
)

git clone --depth 1 https://github.com/wshobson/agents.git temp_agents
foreach ($s in $skills) {
    $match = Get-ChildItem -Path temp_agents -Recurse -Directory -Filter $s | Select-Object -First 1
    if ($match) {
        Copy-Item -Path $match.FullName -Destination "$dest\$s" -Recurse -Force
        Write-Host "Updated: $s"
    }
}
Remove-Item -Recurse -Force temp_agents

git clone --depth 1 https://github.com/KalarisLabs/research-agent-skills.git temp_ras
if (Test-Path "temp_ras\skills\faiss") {
    Copy-Item -Path "temp_ras\skills\faiss" -Destination "$dest\faiss" -Recurse -Force
    Write-Host "Updated: faiss"
}
Remove-Item -Recurse -Force temp_ras
```

#### Linux / macOS (Bash)

```bash
DEST=".agents/skills"
mkdir -p "$DEST"

SKILLS=(
  "python-code-style" "python-anti-patterns" "python-type-safety"
  "python-project-structure" "python-error-handling" "python-configuration"
  "python-testing-patterns" "async-python-patterns" "python-resilience"
  "python-observability" "rag-implementation" "embedding-strategies"
  "hybrid-search-implementation" "vector-index-tuning"
)

git clone --depth 1 https://github.com/wshobson/agents.git temp_agents
for s in "${SKILLS[@]}"; do
  match=$(find temp_agents -type d -name "$s" | head -n 1)
  if [ -n "$match" ]; then
    cp -r "$match" "$DEST/$s"
    echo "Updated: $s"
  fi
done
rm -rf temp_agents

git clone --depth 1 https://github.com/KalarisLabs/research-agent-skills.git temp_ras
if [ -d "temp_ras/skills/faiss" ]; then
  cp -r temp_ras/skills/faiss "$DEST/faiss"
  echo "Updated: faiss"
fi
rm -rf temp_ras
```

---

## Directory Structure

```text
myskills/
├── .agents/
│   ├── rules/
│   │   └── post-edit-gate.md     # Mandatory verification rule loaded by coding agents
│   └── skills/                   # 49 individual skill packages
│       ├── ai-engineer/
│       ├── fastapi-pro/
│       ├── faiss/
│       ├── python-code-style/
│       ├── rag-implementation/
│       └── ...
├── AGENTS.md                     # Central agent playbook & skill reference directory
└── README.md                     # Setup instructions and command guide
```

---

## Mandatory Post-Code Verification Gate

Whenever an agent creates, modifies, or refactors source code, it must pass through the 4-stage filter documented in [`AGENTS.md`](AGENTS.md) before concluding:

1. **Stage 1: Static Hygiene & Anti-Patterns** (`python-anti-patterns`, `python-code-style`)
   - Checks for bare `except:`, mutable default arguments, resource leaks, and unawaited async calls.
2. **Stage 2: Type Safety & Contract Integrity** (`python-type-safety`, `pydantic-models-py`)
   - Checks for explicit function typing, return type annotations, and Pydantic V2 schemas.
3. **Stage 3: Error Handling & Resilience** (`python-error-handling`, `python-resilience`)
   - Checks for domain exception hierarchies, retries, backoff, and network/DB timeouts.
4. **Stage 4: Tests & Systematic Debugging** (`pytest-skill`, `python-testing-patterns`, `systematic-debugging`)
   - Ensures test suites execute cleanly and regression checks pass.

---

## Universal Formatting Policy

- **Strict No-Emoji Policy**: Emojis are strictly prohibited across all code, comments, docstrings, markdown documentation, commit messages, file names, terminal output, and conversational responses.

---

## Acknowledgments & Upstream Sources

- Core skill patterns adapted from [`wshobson/agents`](https://github.com/wshobson/agents).
- Vector search and research skills adapted from [`KalarisLabs/research-agent-skills`](https://github.com/KalarisLabs/research-agent-skills).
