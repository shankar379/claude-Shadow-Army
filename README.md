# Claude Shadow Army

A set of specialized [Claude Code](https://claude.com/claude-code) subagents — each a focused expert you summon for a specific kind of work. Themed after the Shadow Army from *Solo Leveling*, but the value is practical: routing each task to a narrowly-scoped agent produces sharper results than one generalist.

## The Army

| Shadow | Domain | Summon when… |
|---|---|---|
| **igris** | Clean code, refactoring, SOLID, style enforcement | Writing new production code, restructuring, removing duplication |
| **beru** | Debugging, root cause, log/stack-trace investigation | "It's broken", "why is this slow", crashes, mysterious behavior |
| **bellion** | Critical code review + security audit (auth, OWASP, secrets) | Before merging anything important; after auth/payment/data changes |
| **tusk** | System design, API contracts, DB schema, data modeling, docs | BEFORE implementation; design choices; migrations; ADRs |
| **iron** | Database & SQL specialist — schema audits, slow queries, indexes | Slow queries, migration risk, locking/deadlocks, EXPLAIN ANALYZE |
| **greed** | Data engineering + AI/ML/RAG — ETL, vector DBs, embeddings, LLM ops | Embeddings, RAG tuning, eval pipelines, dataset curation |
| **kaisel** | DevOps, CI/CD, Docker, deploys, infra-as-code | Build/deploy failures, pipeline changes, env config |
| **kamish** | Adversarial testing, chaos, edge cases, red-team | Breaking systems on purpose; fuzz/stress; pre-launch hardening |
| **cha-hae-in** | Frontend, React/RN, UI/UX, accessibility, animation | Any visible-to-user change: components, screens, styles |
| **tank** | 3D & WebGL — three.js, react-three-fiber, GLSL shaders, glTF/Blender pipeline, postprocessing | Anything on the WebGL canvas: 3D scenes, shaders, model loading, frame-budget tuning |
| **woo-jin-chul** | Project management, issue tracking, cross-tool sync, reporting | Breaking an initiative into tickets; board hygiene; status reports |

## Install

Copy the agent files into your Claude Code agents directory:

**macOS / Linux**
```bash
git clone https://github.com/shankar379/claude-Shadow-Army.git
cp claude-Shadow-Army/agents/*.md ~/.claude/agents/
```

**Windows (PowerShell)**
```powershell
git clone https://github.com/shankar379/claude-Shadow-Army.git
Copy-Item claude-Shadow-Army\agents\*.md "$env:USERPROFILE\.claude\agents\"
```

For a single project instead of globally, copy them into `.claude/agents/` inside the project root.

Restart Claude Code (or run `/agents` to reload). Claude will then route matching tasks to each shadow automatically, or you can invoke one explicitly: *"use beru to debug this."*

## The `/arise` command (orchestration)

The agents work on their own — Claude routes tasks to them. To also get **`/arise`**, the explicit Monarch invocation that plans a battle, summons the right shadows in order (parallel when independent), hands off between them, and synthesizes **one** result, install the command and the doctrine:

**macOS / Linux**
```bash
cp claude-Shadow-Army/commands/arise.md ~/.claude/commands/
cp claude-Shadow-Army/CLAUDE.md ~/.claude/CLAUDE.md      # or append to your existing one
```

**Windows (PowerShell)**
```powershell
Copy-Item claude-Shadow-Army\commands\arise.md "$env:USERPROFILE\.claude\commands\"
Copy-Item claude-Shadow-Army\CLAUDE.md "$env:USERPROFILE\.claude\CLAUDE.md"   # or append
```

`CLAUDE.md` is **The Monarch's Doctrine** — it tells Claude how to decompose a task, which shadow fits which work, when to run them in parallel vs sequence, and how to hand off mid-task (*Shadow Exchange*). If you already have a `~/.claude/CLAUDE.md`, **append** the doctrine rather than overwriting it.

Then run it with a task:
```
/arise build a checkout flow with tests and a security review
```
Claude writes a short battle plan, Arises only the shadows it needs, and returns a single unified result. (With the doctrine installed, this orchestration also kicks in automatically for non-trivial tasks — `/arise` just forces a fresh plan.)

## How they work

Each `.md` file is a Claude Code subagent definition: YAML frontmatter (`name`, `description`, allowed `tools`) followed by the system prompt that shapes that agent's behavior. The `description` is what Claude reads to decide which shadow fits a given task. Edit any file to tune its scope, tools, or voice.

## License

MIT — use them, fork them, reshape them.
