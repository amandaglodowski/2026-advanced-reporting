# Git Basics - Essential Commands

This guide covers the fundamental Git commands you'll use daily to save and sync your work with GitHub.

---

## The Basic Workflow

Think of Git like saving and backing up your work:
1. **Check status** - See what's changed
2. **Add files** - Choose what to save
3. **Commit** - Save a snapshot with a note
4. **Push** - Upload to GitHub

---

## Command 1: `git status`

### What it does:
Shows you what's changed in your project since your last commit.

### When to use it:
- Before adding/committing files (to see what changed)
- When you're confused about what's happening
- **Use it often!** It's your safety check.

### How to use it:
```bash
git status
```

### What you'll see:

**Example output:**
```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  
	modified:   data-analysis.ipynb
	modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  
	new-visualization.png

no changes added to commit (use "git add" and/or "git commit -a")
```

**What this means:**
- **Modified files** (red) - Files you changed but haven't staged
- **Untracked files** (red) - New files Git isn't tracking yet
- **Staged files** (green) - Files ready to commit

---

## Command 2: `git add filename`

### What it does:
Adds a specific file to the "staging area" - marking it ready to save.

### When to use it:
When you want to save **specific files only** (not everything).

### How to use it:
```bash
git add filename.txt
```

### Examples:

**Add a single file:**
```bash
git add analysis.ipynb
```

**Add multiple specific files:**
```bash
git add analysis.ipynb data.csv README.md
```

**Add all files of a certain type:**
```bash
git add *.ipynb    # All Jupyter notebooks
git add *.py       # All Python files
git add *.csv      # All CSV files
```

**Check what you staged:**
```bash
git status
```

You'll see staged files in **green**.

---

## Command 3: `git add .`

### What it does:
Adds **ALL changed and new files** in the current directory to staging.

### When to use it:
When you want to save **everything** you've changed.

### How to use it:
```bash
git add .
```

** Warning:** The `.` means "everything in this folder"
- Be careful - this adds ALL files
- Check `git status` first to see what you're adding

### When NOT to use it:
- If you have sensitive files (passwords, API keys)
- If you have large files you don't need to save
- If you're working on multiple unrelated changes

**Pro tip:** Use `git status` before `git add .` to see what you're about to add!

---

## Command 4: `git commit -m "message"`

### What it does:
Saves a snapshot of your staged files with a descriptive message.

### When to use it:
After you've added files with `git add` and are ready to save.

### How to use it:
```bash
git commit -m "Your descriptive message here"
```

### Good commit messages:

 **Good examples:**
```bash
git commit -m "Add data cleaning notebook"
git commit -m "Fix typo in README"
git commit -m "Update visualization with new color scheme"
git commit -m "Complete assignment 1 analysis"
```

 **Bad examples:**
```bash
git commit -m "update"           # Too vague
git commit -m "stuff"            # Not descriptive
git commit -m "asdfasdf"         # Meaningless
git commit -m "fixed it"         # What did you fix?
```

### Tips for commit messages:
- Start with a verb: "Add", "Fix", "Update", "Complete"
- Be specific but concise
- Describe WHAT changed, not why (save why for longer messages)
- Use present tense: "Add" not "Added"

---

## Command 5: `git push origin main`

### What it does:
Uploads your commits from your computer to GitHub.

### When to use it:
After you've committed your changes and want to back them up to GitHub.

### How to use it:
```bash
git push origin main
```

### What this means:
- `git push` - Upload commits
- `origin` - To GitHub (the remote repository)
- `main` - To the main branch

### What you'll see:

**Success:**
```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.23 KiB | 1.23 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To github.com:username/repository.git
   abc1234..def5678  main -> main
```

**First time (may need to set upstream):**
```bash
git push -u origin main
```

The `-u` sets "upstream" so future pushes only need `git push`.

---

## Complete Workflow Example

### Scenario: You just finished working on your data analysis

**Step 1: Check what changed**
```bash
git status
```

**Output:**
```
Changes not staged for commit:
	modified:   analysis.ipynb
	modified:   data.csv
```

**Step 2: Add files you want to save**
```bash
git add analysis.ipynb data.csv
```

**Or add everything:**
```bash
git add .
```

**Step 3: Check staging area (optional but good practice)**
```bash
git status
```

**Output:**
```
Changes to be committed:
	modified:   analysis.ipynb
	modified:   data.csv
```

**Step 4: Commit with descriptive message**
```bash
git commit -m "Complete exploratory data analysis"
```

**Output:**
```
[main abc1234] Complete exploratory data analysis
 2 files changed, 45 insertions(+), 12 deletions(-)
```

**Step 5: Push to GitHub**
```bash
git push origin main
```

**Output:**
```
To github.com:username/repository.git
   abc1234..def5678  main -> main
```

 **Done! Your work is saved and backed up to GitHub.**

---

## Daily Workflow Summary

```bash
# 1. Check what's changed
git status

# 2. Add files to staging
git add filename.txt        # Specific file
# OR
git add .                   # Everything

# 3. Commit with message
git commit -m "Descriptive message"

# 4. Push to GitHub
git push origin main
```

**Repeat these steps every time you finish a unit of work!**

---

## Common Patterns

### Pattern 1: Working on an assignment
```bash
# Do your work in Jupyter...

git status                           # See what changed
git add assignment1.ipynb            # Add your notebook
git commit -m "Complete assignment 1"
git push origin main                 # Upload to GitHub
```

### Pattern 2: Multiple files changed
```bash
git status                           # See all changes
git add .                            # Add everything
git commit -m "Update analysis and add visualizations"
git push origin main
```

### Pattern 3: Working session with multiple saves
```bash
# After making significant progress...
git add .
git commit -m "Add data cleaning section"

# Continue working...

# Made more progress...
git add .
git commit -m "Complete visualization section"

# End of work session...
git push origin main                 # Push all commits at once
```

---

## Quick Reference

| Command | What it does | When to use |
|---------|-------------|-------------|
| `git status` | Show what's changed | Before every add/commit |
| `git add filename` | Stage specific file | Saving selective files |
| `git add .` | Stage everything | Saving all changes |
| `git commit -m "msg"` | Save snapshot | After staging files |
| `git push origin main` | Upload to GitHub | Backup/share your work |

---

## Troubleshooting

### "Nothing to commit, working tree clean"

**Problem:** You ran `git commit` but nothing happens.

**Solution:** You either:
1. Haven't made any changes, OR
2. Haven't added files with `git add`

```bash
git status              # See what's changed
git add filename        # Add the files
git commit -m "message" # Now commit
```

---

### "Your branch is ahead of 'origin/main' by X commits"

**Problem:** You committed but forgot to push.

**Solution:**
```bash
git push origin main
```

Your work is saved locally but not on GitHub yet.

---

### "Permission denied (publickey)"

**Problem:** GitHub can't authenticate you.

**Solution:** Your SSH key isn't set up correctly. Refer to the SSH setup guide.

---



## Best Practices

 **DO:**
- Commit often (every time you complete a chunk of work)
- Write descriptive commit messages
- Use `git status` frequently
- Push at least once per work session
- Commit before closing your laptop

 **DON'T:**
- Commit passwords, API keys, or sensitive data
- Use vague commit messages like "update" or "fix"
- Wait days/weeks between commits
- Forget to push (your work isn't backed up until you push!)

---

## Commit Message Templates

Use these as starting points:

**Working on assignments:**
- `"Complete assignment [number]"`
- `"Add [assignment] analysis"`
- `"Fix [issue] in [assignment]"`

**Project work:**
- `"Add data cleaning section"`
- `"Create initial visualization"`
- `"Update README with project description"`

**Fixes:**
- `"Fix typo in [filename]"`
- `"Fix calculation error in [section]"`
- `"Correct data import issue"`

**Updates:**
- `"Update visualization colors"`
- `"Refine analysis methodology"`
- `"Add comments to code"`

---


## Remember

Think of this workflow as:
1. **Status** - Check your work
2. **Add** - Choose what to save
3. **Commit** - Save with a note
4. **Push** - Backup to cloud

**Do this cycle frequently!** Every time you complete a meaningful chunk of work, run through these four commands.

---

