# compliance-poc

A minimal proof-of-concept for firm-level AI compliance checking via Claude Projects + GitHub.

## Architecture

```
GitHub (SKILL.md)
      │
      │  GitHub connector syncs knowledge
      ▼
Claude Project (compliance-poc)
      │
      │  Project instructions: "Follow SKILL.md"
      │  Knowledge base: SKILL.md (from this repo)
      ▼
Compliance Check Output
```

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | The active compliance rule (currently v1.1.0) |
| `sample-doc.txt` | Test document for the POC |
| `.github/workflows/skill-tracker.yml` | Logs every SKILL.md update to main |

## How updates propagate

1. Edit `SKILL.md` on `main`
2. GitHub Action fires → logs version + commit
3. Claude project re-syncs knowledge on next scheduled index (or manual re-sync)
4. Claude's behaviour reflects the new instructions

## Claude Project Instructions (paste into project settings)

```
You are a compliance checker. Follow the rules in SKILL.md exactly.
Do not summarise, rewrite, or comment on document content.
Only flag paragraphs that violate the citation rule as described in SKILL.md.
```

## Version history

| Version | Flag | Change |
|---------|------|--------|
| v1.0.0 | ⚠️ | Initial POC |
| v1.1.0 | 🚨 | Updated flag emoji |
