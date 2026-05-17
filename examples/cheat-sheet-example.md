# cheat-sheet — full example

**Topic:** Git daily commands — Stage/Commit, Branch, History, Remotes
**Width budget:** 95 cols
**Mode:** Unicode (default)

---

```
╔═════════════════════════════════════════════════════════════════════════════════════════════╗
║                                      GIT DAILY CHEAT SHEET                                  ║
╚═════════════════════════════════════════════════════════════════════════════════════════════╝
┌─ Stage / Commit ─────────────────────────────┬─ Branch ─────────────────────────────────────┐
│                                              │                                              │
│ git add <file>        · stage one file       │ git branch            · list local branches  │
│ git add .             · stage all changes    │ git branch <name>     · create new branch    │
│ git add -p            · stage hunks          │ git checkout <name>   · switch to branch     │
│ git commit -m "<msg>" · commit with message  │ git checkout -b <n>   · create + switch      │
│ git commit --amend    · edit last commit     │ git branch -d <name>  · delete merged branch │
│ git stash             · shelve dirty state   │ git branch -D <name>  · force-delete branch  │
│                                              │                                              │
├─ History ────────────────────────────────────┼─ Remotes ────────────────────────────────────┤
│                                              │                                              │
│ git log --oneline     · compact commit log   │ git remote -v         · list remotes         │
│ git log -p            · log with diffs       │ git fetch             · download refs        │
│ git log --graph       · branch graph         │ git pull              · fetch + merge        │
│ git diff              · unstaged changes     │ git push              · push current branch  │
│ git diff --staged     · staged changes       │ git push -u origin <b>· push + set upstream  │
│ git blame <file>      · line-by-line author  │ git remote add <n> <url> · add remote        │
│                                              │                                              │
└──────────────────────────────────────────────┴──────────────────────────────────────────────┘
```

---

## Why this works

- Four sections in a 2×2 grid give exactly one conceptual cluster per quadrant — Stage/Commit and Branch are the most-used pair so they occupy the top row for fastest eye-scan.
- The `·` separator aligns all definitions at the same column within each 44-char inner column, giving a dictionary-style layout that is faster to scan than a prose list.
- One entry ("git remote add") exceeds the typical line length but still fits within the 44-char inner column (the command is shortened to `git remote add <n> <url>`); no cell wraps.
