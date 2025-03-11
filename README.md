To set up passwordless push to a Git repository using SSH keys, follow these steps:

✅ 1. Generate an SSH Key (if not already generated)
On your EC2 instance, generate an SSH key:

bash
Copy
Edit
ssh-keygen -t rsa -b 4096
When prompted:
File location – Press Enter to accept the default (~/.ssh/id_rsa)
Passphrase – Just press Enter to skip (for passwordless access)
✅ 2. Add SSH Key to SSH Agent
Start the SSH agent and add the key:

bash
Copy
Edit
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
✅ 3. Copy SSH Key to Clipboard
Copy the SSH key to add it to your GitHub account:

bash
Copy
Edit
cat ~/.ssh/id_rsa.pub
It will look something like:

sql
Copy
Edit
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC5...your-key... user@host
✅ 4. Add SSH Key to GitHub
Go to GitHub → Settings → SSH and GPG keys → New SSH Key
Title – Add a meaningful title (e.g., "EC2 Instance")
Key – Paste the SSH key
Save
✅ 5. Test the SSH Connection
Test if the SSH connection to GitHub is working:

bash
Copy
Edit
ssh -T git@github.com
If it works, you should see:

bash
Copy
Edit
Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.
✅ 6. Set SSH as the Git Remote URL
Switch the Git remote from HTTPS to SSH:

Check existing remote:
bash
Copy
Edit
git remote -v
Update to SSH:
bash
Copy
Edit
git remote set-url origin git@github.com:<username>/<repo>.git
✅ 7. Push Without Password
Now you can push without a password:

bash
Copy
Edit
git push origin main
🚀 Done!
✅ You’ve now configured passwordless SSH-based Git push! 😎

