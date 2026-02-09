# Jupyter Notebook Workflow - Quick Reference

This guide shows you how to launch Jupyter Notebook using your `dataj-installs` environment.

---

## Daily Workflow

### 1. Open Terminal
- Press `Cmd + Space` → type "Terminal" → Enter
- Or: Applications → Utilities → Terminal

### 2. Activate environment
```bash
conda activate dataj-installs
```

Your prompt should change to show `(dataj-installs)` at the beginning.

### 3. Navigate to your work folder
```bash
cd ~/dataProjects
```

Or navigate to wherever you keep your notebooks:
```bash
cd ~/dataProjects/202x-demo-investigation
```

### 4. Launch Jupyter
```bash
jupyter notebook
```

Your browser will open automatically with Jupyter.

### 5. Create or open a notebook
- Click "New" → "Python 3 (ipykernel)" to create a new notebook
- Or click on an existing `.ipynb` file to open it

### 6. Do your work
Write code, run cells, save your notebook.

### 7. When done - stop Jupyter
In Terminal, press `Ctrl+C` (press it twice if needed)

### 8. Deactivate environment
```bash
conda deactivate
```

---

## Complete Command Sequence

```bash
# Open Terminal

# Activate environment
conda activate dataj-installs

# Navigate to work folder
cd ~/Desktop

# Launch Jupyter
jupyter notebook

# ... do your work in browser ...

# Stop Jupyter (in Terminal)
# Press Ctrl+C

# Deactivate environment
conda deactivate
```

---

## Troubleshooting

**Problem:** `conda: command not found`
- **Solution:** Restart Terminal or run: `source ~/.zshrc`

**Problem:** `python --version` shows wrong version
- **Solution:** Make sure you activated the environment first

**Problem:** Packages not found in Jupyter
- **Solution:** Make sure you launched Jupyter AFTER activating `dataj-installs`

**Problem:** Can't see my files in Jupyter
- **Solution:** Navigate to the correct folder BEFORE launching Jupyter

---

## Tips

- Always activate the environment BEFORE launching Jupyter
- Navigate to your work folder BEFORE launching Jupyter
- Save your notebooks frequently (`Cmd+S` in Jupyter)
- When done, properly stop Jupyter with `Ctrl+C`
