# Crisp Mode — VS Code Copilot Token Optimizer

Ultra-compressed communication mode for GitHub Copilot. Cuts **65-75% of output tokens** while keeping full technical accuracy.

## Why Crisp Mode?

Every word in Copilot's response costs money. Crisp mode drops the filler without losing the signal.

**Before (69 tokens):**
```
Great question! There are several reasons why your React component 
might be re-rendering unnecessarily. Let me walk you through the most 
common causes and how to fix them.
```

**After (19 tokens):**
```
Common causes: parent re-render, new object/array refs each render, 
missing useMemo/useCallback. Fix:
```

Same answer. **73% fewer tokens.**

---

## What Gets Compressed

✅ **Compressed:**
- Conversational prose (explanations, walkthroughs)
- Introductions and pleasantries
- Filler words and hedging

❌ **NOT Compressed:**
- Code blocks (normal, idiomatic, well-commented)
- Commit messages (Conventional Commits format)
- Error messages and technical terms
- Security warnings (auto-reverts to clear language)

---

## Installation

### Option 1: Global (All Workspaces)

1. Copy `crisp.instructions.md` to your VS Code User prompts folder:
   ```bash
   # macOS/Linux
   ~/.config/Code/User/prompts/crisp.instructions.md
   
   # Windows
   %APPDATA%\Code\User\prompts\crisp.instructions.md
   ```

2. Restart VS Code Copilot

3. Done. Active automatically.

### Option 2: Workspace Only

1. Create `.github/copilot-instructions.md` in your repo root

2. Copy the content from `crisp.instructions.md`

3. Commit and push

---

## Usage

Type these in the Copilot Chat input box (no slash prefix needed):

| Command | Effect |
|---------|--------|
| `crisp lite` | Professional, full sentences, just no filler |
| `crisp full` | Default. Fragments, no articles |
| `crisp ultra` | Maximum compression. Abbreviations (DB/auth/config), arrows (X→Y) |
| `stop crisp` | Deactivate, return to verbose mode |
| `normal mode` | Same as stop crisp |
| `crisp mode` | Re-activate after deactivation |
| `less tokens` | Same as crisp mode |

---

## Examples

### React Question
**Input:** "Why is my React component re-rendering?"

**Crisp output:**
```
Common causes: parent re-render, new object/array refs each render, 
missing useMemo/useCallback. Check with React DevTools Profiler. Fix:
```

### Error Fix
**Input:** "How do I fix this error?"

**Crisp output:**
```
Error cause: [X]. Fix:
```

### Database Query
**Input:** "Optimize this query"

**Crisp output (ultra mode):**
```
DB → N+1 issue. Add JOIN not loop. Index on user_id. Query:
```

---

## Token Math

| Phase | Tokens |
|-------|--------|
| Session start (one-time) | ~110 |
| Average response (verbose) | ~2000 |
| Average response (crisp full) | ~500 |
| **Net savings per response** | **-1500** |
| **Cost of feature** | **-110** |

**Breakeven:** After 1 response. Everything after = pure savings.

---

## Intensity Levels

| Level | Use Case | Example |
|-------|----------|---------|
| **lite** | Professional contexts. Keep grammar. | "The bug is in the auth module. Token expiry check." |
| **full** | Default. Fast feedback. | "Bug in auth. Token expiry check use `<` not `<=`." |
| **ultra** | Max speed/savings. | "Bug: auth token expiry. Fix: `<` not `<=`." |

---

## Auto-Clarity (Safety)

Crisp mode automatically switches to normal prose when:
- ⚠️ Security warnings or vulnerability explanations
- 🚨 Irreversible action confirmations (delete, drop, force-push)
- ❓ User confusion detected (repeated questions)
- 🔀 Multi-step sequences where clarity is critical

Then resumes crisp after the critical section.

---

## Configuration

Edit `crisp.instructions.md` directly:

```yaml
---
description: "Compress output ~65-75%..."
applyTo: "**"  # Change this to scope differently
---
```

**Scope options:**
```yaml
applyTo: "**"                    # All files (current)
applyTo: ["**/*.ts", "**/*.js"]  # TypeScript/JavaScript only
applyTo: "src/**"                # Only src folder
```

---

## How It Works

Crisp Mode is a VS Code Copilot instruction file loaded into every session's system context.

**Rules applied:**
- Drop articles (a, an, the)
- Drop filler (just, really, basically, actually, simply)
- Drop pleasantries (sure, certainly, of course, happy to help)
- Drop hedging (I think, maybe, perhaps, it seems like)
- Allow fragments
- Use short synonyms (big → extensive, fix → implement solution)
- Keep technical terms exact
- Keep code/errors/paths exact

---

## Tips & Tricks

### Mix with Questions
```
"crisp ultra, explain this error"  ← Level switch + question in one message
```

### Activate Per-Session
```
Start conversation with: "crisp mode" or "less tokens"
Then ask questions normally
```

### Disable When Needed
```
"normal mode" → Returns to verbose for the rest of the session
"crisp mode" → Re-enable
```

### Works with All Copilot Features
- ✅ Chat panel
- ✅ Inline chat (`Ctrl+I`)
- ✅ Quick Chat (`Ctrl+Shift+I`)
- ✅ Copilot Edits

---

## FAQ

**Q: Does this affect code quality?**
A: No. Code output stays normal, idiomatic, and well-commented. Only conversational prose is compressed.

**Q: What about security warnings?**
A: Auto-clarity kicks in. Dangerous operations revert to clear, verbose English.

**Q: Will Copilot refuse to use this?**
A: No. This is a standard VS Code instruction file. Copilot respects it like any other system instruction.

**Q: How much will I actually save?**
A: Depends on your usage. At $3/1M tokens:
- 100 responses/month × 1500 saved tokens = 150K tokens = $0.45/month
- 1000 responses/month = $4.50/month

Not huge individually, but adds up fast at scale. Plus: faster responses, better UX.

**Q: Can I customize the rules?**
A: Yes. Edit `crisp.instructions.md` directly. YAML frontmatter controls scope (`applyTo`), the markdown body controls rules.

**Q: Does this work with other AI assistants?**
A: Only VS Code Copilot (GitHub Copilot in VS Code). For Claude/Cursor/other tools, see [caveman project](https://github.com/juliusbrussee/caveman).

---

## Inspiration

Built on the philosophy of [caveman](https://github.com/juliusbrussee/caveman) by [@JuliusBrussee](https://github.com/juliusbrussee), but simplified for VS Code's native instruction system.

