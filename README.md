
# SSH guide

Setting up SSH with GitHub allows you to authenticate securely without needing to enter your username and password each time you push or pull code. 

## Step 1: Check for Existing SSH Keys

First, check if you already have an SSH key:

```
ls -al ~/.ssh
```

Look for files like id_rsa and id_rsa.pub (or other files ending in .pub). If you have a public key (like id_rsa.pub), you can skip to Step 3.

## Step 2: Generate a New SSH Key (if needed)
If you don’t have an existing key, create a new one:

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- t rsa: Specifies the key type. 
- b 4096: Sets the key size to 4096 bits (more secure).
- C: Adds a label (your email) to the key, helping identify it later.
You’ll be prompted to save the key to a location (default is ~/.ssh/id_rsa). You can hit Enter to confirm the default. When asked to create a passphrase, you can choose to add one or leave it blank for easier access (though a passphrase adds an extra layer of security).

## Step 3: Add SSH Key to the SSH-Agent
Start the SSH agent in the background:

```
eval "$(ssh-agent -s)"
```
Then add your private SSH key to the agent:

```
ssh-add ~/.ssh/id_rsa
```

## Step 4: Copy the SSH Public Key
Now, copy the SSH public key to your clipboard:

```
pbcopy ~/.ssh/id_rsa.pub 
```

## Step 5: Add SSH Key to GitHub

1. Log in to your GitHub account.
2. Go to Settings > SSH and GPG keys.
3. Click New SSH key.
4. Give the key a title (like "My Laptop" or "Work PC").
5. Paste the key from your clipboard into the Key field.
6. Click Add SSH key.

## Step 6: Test the SSH Connection to GitHub
To verify everything is working, run:

```
ssh -T git@github.com
```

You should see a message like: "Hi username! You've successfully authenticated, but GitHub does not provide shell access."

This confirms your SSH key is properly set up with GitHub.

## Step 7: Configure Git to Use SSH for GitHub (Optional)
By default, GitHub URLs may use HTTPS. You can update your Git repository to use SSH by changing the remote URL:

```
git remote set-url origin git@github.com:username/repository.git
```
Replace username and repository with your GitHub username and the repository name.
