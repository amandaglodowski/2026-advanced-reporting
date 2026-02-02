# A Beginner’s Guide to Setting Up SSH Keys for GitHub

GitHub authentication has evolved over time, and passwords are no longer
considered secure enough for daily Git operations.

SSH (Secure Shell) allows you to securely connect and authenticate to GitHub
without repeatedly entering your credentials.

An SSH key acts like a digital identity for your machine.

Your machine keeps a **private key** (secret), and GitHub stores a **public key**
(safe to share).



---

## Step 1: Open Git Bash

Open **Git Bash** on your computer.

---

## Step 2: Check if an SSH Key Already Exists

Before creating a new key, check if your system already has one.

```bash
ls ~/.ssh
```

If the folder doesn’t exist, it simply means no SSH key has been created yet.
This is normal and expected behaviour. Proceed to Step 3.

If the `.ssh` folder already exists, you may see:

- `id_ed25519` (Private Key)
- `id_ed25519.pub` (Public Key)

You may reuse the existing key or create a new one.

---

## Step 3: Generate a New SSH Key

Create a new SSH key using the following command:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

When prompted for the file location, press **Enter** to use the default.

You may also set a passphrase for extra security, but this step is optional.

Once the key is generated, the `.ssh` folder will be created automatically.

Check again by running:

```bash
ls ~/.ssh
```

You should see:

- `id_ed25519`
- `id_ed25519.pub`

Never share your private key (`id_ed25519`).

---

## Step 4: Start the SSH Agent

The SSH agent allows Git to use your key.

```bash
eval "$(ssh-agent -s)"
```

You should see output similar to:

```
Agent pid 1234
```

---

## Step 5: Add the SSH Key to the Agent

Run the following command:

```bash
ssh-add ~/.ssh/id_ed25519
```

If you set a passphrase, you will be prompted to enter it now.

---

## Step 6: Copy the Public SSH Key

Run:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire line that starts with `ssh-ed25519`.

---

## Step 7: Add the SSH Key to GitHub

1. Go to github.com
2. Click your profile photo → **Settings**
3. Click **SSH and GPG keys**
4. Click **New SSH key**
5. Fill in:
   - **Title:** My Windows Laptop
   - **Key type:** Authentication Key
   - **Key:** Paste the copied key
6. Click **Add SSH key**
7. Enter your GitHub password if prompted

Your SSH key will now appear in your GitHub account.

---

## Step 8: Test the SSH Connection

Run:

```bash
ssh -T git@github.com
```

If asked to continue connecting, type `yes`.

A success message will appear:

```
Hi <username>! You've successfully authenticated...
```

Congratulations! SSH is working.

