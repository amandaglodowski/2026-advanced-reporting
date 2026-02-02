# Setting Up SSH Keys for GitHub - Mac Instructions

GitHub no longer accepts passwords for security reasons. Instead, you'll use SSH keys - a more secure way to prove your identity.

SSH uses two keys that work together:
- **Private key**: Secret file that stays on your computer only
- **Public key**: File you share with GitHub

When you try to access GitHub, these keys work like a secret handshake - GitHub checks if your keys match, and if they do, you're in! No password needed.

**Security benefit**: Even if someone steals your GitHub password, they can't access your account from their computer because they don't have your private key.

This guide will help you set up SSH authentication for GitHub. You'll do this **once** and never need to enter your GitHub password again when using Git.

---

## What is SSH and Why Do We Need It?

SSH (Secure Shell) is a secure way to authenticate with GitHub without typing your password every time.

**Benefits:**
-  Set up once, works forever
-  More secure than passwords
-  No tokens to manage or lose
-  Industry standard for data journalists and developers

---

## Part 1: Check if You Already Have SSH Keys

### Step 1: Open Terminal
- Press `Cmd + Space` → type "Terminal" → press Enter

### Step 2: Check for existing SSH keys
```bash
ls -al ~/.ssh
```

**Look for SSH key pairs (files that come in pairs):**

SSH keys come in pairs with the same base name:
- Private key: filename WITHOUT extension (e.g., `id_rsa`, `id_ed25519`, `github`)
- Public key: same filename WITH `.pub` extension (e.g., `id_rsa.pub`, `id_ed25519.pub`, `github.pub`)

**Common examples:**
- `id_rsa` and `id_rsa.pub` (older default)
- `id_ed25519` and `id_ed25519.pub` (newer default)
- `github` and `github.pub` (custom name)
- Any other matching pair

**What to do:**

**If you see MATCHING PAIRS** (like those above):
→ **You already have SSH keys! Skip to Part 3**

**If you see:**
- `No such file or directory` → **Continue to Part 2**
- Only `config` or `known_hosts` files (no pairs) → **Continue to Part 2**

---

## Part 2: Generate New SSH Keys

### Step 1: Generate your SSH key
Copy this command **exactly**, but replace `your-email@example.com` with your GitHub email:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

**Example:**
```bash
ssh-keygen -t ed25519 -C "jane.smith@university.edu"
```

### Step 2: Save the key
When prompted `Enter file in which to save the key`:
- **Just press Enter** (accepts default location)

**You'll see:**
```
Enter file in which to save the key (/Users/yourname/.ssh/id_ed25519):
```
Press `Enter`

### Step 3: Create a passphrase (optional but recommended)
When prompted `Enter passphrase`:
- Type a passphrase (you won't see characters - this is normal)
- Press `Enter`
- Type the same passphrase again
- Press `Enter`

**Tip:** Use a passphrase you'll remember, or press Enter twice to skip (less secure).

**You'll see:**
```
Your identification has been saved in /Users/yourname/.ssh/id_ed25519
Your public key has been saved in /Users/yourname/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:... your-email@example.com
```

 **Success! Your SSH key is created.**

### Step 4: Start the SSH agent
```bash
eval "$(ssh-agent -s)"
```

**You'll see:**
```
Agent pid 12345
```

### Step 5: Add your SSH key to the agent
```bash
ssh-add ~/.ssh/id_ed25519
```

**If you set a passphrase, enter it now.**

**You'll see:**
```
Identity added: /Users/yourname/.ssh/id_ed25519 (your-email@example.com)
```

---

## Part 3: Add SSH Key to GitHub

### Step 1: Copy your public SSH key
```bash
cat ~/.ssh/id_ed25519.pub
```

**You'll see something like:**
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJl3dIeudNqd0DPMRD6OIh65A9pu9p8POSqArqNQG3WE your-email@example.com
```

**Select and copy the ENTIRE output** (Cmd+A, then Cmd+C)

### Step 2: Go to GitHub
1. Open your browser and go to [github.com](https://github.com)
2. Log in to your GitHub account

### Step 3: Navigate to SSH settings
1. Click your profile picture (top right)
2. Click **Settings**
3. In the left sidebar, click **SSH and GPG keys**
4. Click **New SSH key** (green button)

### Step 4: Add your key
1. **Title:** Give it a name like "My MacBook" or "Personal Laptop"
2. **Key type:** Leave as "Authentication Key"
3. **Key:** Paste your SSH key (the one you copied)
4. Click **Add SSH key**
5. Enter your GitHub password if prompted

 **Success! Your SSH key is added to GitHub.**

---

## Part 4: Test Your SSH Connection

### Step 1: Test the connection
```bash
ssh -T git@github.com
```

### Step 2: First-time connection warning
**If this is your first time, you'll see:**
```
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

**Type `yes` and press Enter.**

### Step 3: Success message
**You should see:**
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

 **Perfect! SSH is working!**

**If you see an error**, see the Troubleshooting section below.

---

## Part 5: Using SSH with Git

### Cloning a repository
**Use the SSH URL (not HTTPS):**

```bash
git clone git@github.com:username/repository.git
```

**Example:**
```bash
git clone git@github.com:sandeepmj/data-journalism-course.git
```

### Finding the SSH URL on GitHub
1. Go to the repository on GitHub
2. Click the green **Code** button
3. Select **SSH** tab
4. Copy the URL (looks like `git@github.com:username/repo.git`)

### Already cloned with HTTPS?
If you already cloned a repo with HTTPS, switch it to SSH:

```bash
cd your-repo-folder
git remote set-url origin git@github.com:username/repository.git
```

Check it worked:
```bash
git remote -v
```

Should show URLs starting with `git@github.com:` 

---

## Verification Checklist

Before submitting your setup verification, confirm:

-  `ls ~/.ssh` shows `id_ed25519` and `id_ed25519.pub`
-  `ssh -T git@github.com` shows success message with your username
-  You can clone a repository using SSH URL
-  SSH key is visible in your GitHub Settings → SSH and GPG keys

---

## Daily Usage

**Good news: You don't need to do anything daily!**

SSH works automatically now. Just use Git commands as normal:

```bash
# Clone repositories
git clone git@github.com:username/repo.git

# Push changes
git push origin main

# Pull changes
git pull origin main
```

No passwords needed! 🎉

---

## Troubleshooting

### "Permission denied (publickey)"

**Problem:** Your SSH key isn't added to GitHub or the agent.

**Solution 1:** Make sure you added the key to GitHub (Part 3)

**Solution 2:** Add key to SSH agent:
```bash
ssh-add ~/.ssh/id_ed25519
```

**Solution 3:** Check which key is being used:
```bash
ssh-add -l
```

Should show your key. If empty, add it with Solution 2.

---

### "Could not open a connection to your authentication agent"

**Problem:** SSH agent isn't running.

**Solution:** Start the agent:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

### "Bad permissions" error

**Problem:** SSH key file has wrong permissions.

**Solution:** Fix permissions:
```bash
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

---

### Forgot which email I used

**Check your SSH key:**
```bash
cat ~/.ssh/id_ed25519.pub
```

The email is at the end of the output.

---

### Need to generate a new key?

**If you lost your key or need a new one:**

1. Generate new key:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

2. When prompted for filename, use a different name:
```
Enter file in which to save the key: /Users/yourname/.ssh/id_ed25519_new
```

3. Follow Part 3 to add the new key to GitHub

---

### Testing different keys

**See what keys are loaded:**
```bash
ssh-add -l
```

**Remove all keys:**
```bash
ssh-add -D
```

**Add specific key:**
```bash
ssh-add ~/.ssh/id_ed25519
```

---

## Multiple GitHub Accounts (Advanced)

If you have personal and school GitHub accounts, you'll need SSH config:

1. Create config file:
```bash
nano ~/.ssh/config
```

2. Add this content:
```
# Personal GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

# School GitHub
Host github-school
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_school
```

3. Save: `Ctrl+X`, `Y`, `Enter`

4. Clone with different hosts:
```bash
# Personal repos
git clone git@github.com:username/repo.git

# School repos
git clone git@github-school:username/repo.git
```

---

## Security Best Practices

 **DO:**
- Use a passphrase for your SSH key
- Keep your private key (`id_ed25519`) secret
- Add SSH key to each computer you use

❌ **DON'T:**
- Share your private key file
- Email or upload your private key anywhere
- Copy your private key to cloud storage
- Share your passphrase

**Remember:** 
- **Public key** (`id_ed25519.pub`) - Safe to share, add to GitHub
- **Private key** (`id_ed25519`) - Keep secret, never share

---

## What Did You Just Do?

1. **Generated an SSH key pair:**
   - Private key (stays on your computer)
   - Public key (goes to GitHub)

2. **Added public key to GitHub:**
   - GitHub can now verify it's you

3. **Tested the connection:**
   - Confirmed GitHub recognizes your key

4. **Now when you use Git:**
   - GitHub checks your private key
   - Matches it with your public key
   - Lets you in automatically!

**Think of it like:**
- Private key = Your house key
- Public key = Your door lock
- GitHub has a copy of your lock
- Your key opens it automatically

---

## Getting Help

If you encounter issues not covered here:
1. Take a screenshot of the error
2. Note what command you ran
3. Check GitHub's SSH troubleshooting: [docs.github.com/en/authentication/troubleshooting-ssh](https://docs.github.com/en/authentication/troubleshooting-ssh)
4. Come to office hours or post on the course discussion board

---

**Congratulations! You've set up SSH authentication for GitHub!** 🎉

No more typing passwords every time you push or pull code!
