# Git Commands / terminal commands <br>

## Git submodules
Remove the existing submodule and re-add it with the correct remote URL:
First, remove the existing submodule:
```bash
git submodule deinit -f public
git rm -f public
rm -rf .git/modules/public
```
Then, add the submodule again with the correct remote URL:
```bash
git submodule add -b main https://github.com/pauliusuk/pauliusuk.github.io.git public
```
Use the existing local git directory with the correct remote URL:
If you want to use the existing local git directory named "public" with the correct remote URL, you should manually update the remote URL for the submodule:
```bash
git submodule set-url public https://github.com/pauliusuk/pauliusuk.github.io.git
```

## Git config
| Command | Description |
| :--  | :-- |
| `git config --global user.name "user1"`              | Set user name |
| `git config --global user.email "user1@example.com"` | Set user email |
| `git config --global core.editor "nvim"`             | Set editor to nvim |
| `git log -4`                                         | shows 4 last commits |
| `git rm --cached -r .`                               | remove unstage commits |
|`git commit --amend -m "New commit message"`          | change commit message if not pushed yet |

## SSH remote
| Command | Description |
| :--  | :-- |
|  `git remote -v`                                            | check remote link |
|  `git remote add origin git@github.com:user1/.dotfiles.git` | add ssh remote link |
| `git remote set-url origin https://github.com/Paulobox/gitcommands.git`| set https remote link |
|  `git remote set-url origin git@github.com:Paulobox/gitcommands.git` | set ssh remote link |

## Just pull files from remote repo
| Command | Description |
| :--  | :-- |
| git fetch origin  | # Fetch the latest changes from the remote repository |
| git reset --hard origin/master  | choose origin or master |

## Git Rebase
| Command | Description |
| :--  | :-- |
|  `git rebase -i --root`                             | open rebase and edit commits |
|  `git add .`                                        | add commit changes |
|  `git rebase --continue`                            | change description of commit |
|  `git push -u origin -f main`                       | force push |

## Full list of git — Rebase Commands:
| Command | Description |
| :-- | :-- |
| `p, pick <commit>` | Use commit |
| `r, reword <commit>` | Use commit, but edit the commit message |
| `e, edit <commit>` | Use commit, but stop for amending |
| `s, squash <commit>` | Use commit, but meld into previous commit |
| `f, fixup [-C \| -c] <commit>` | Like "squash" but keep only the previous commit's log message, unless -C is used, in which case keep only this commit's message; -c is same as -C but opens the editor |
| `x, exec <command>` | Run command (the rest of the line) using shell |
| `b, break` | Stop here (continue rebase later with 'git rebase --continue') |
| `d, drop <commit>` | Remove commit |
| `l, label <label>` | Label current HEAD with a name |
| `t, reset <label>` | Reset HEAD to a label |
| `m, merge [-C <commit> \| -c <commit>] <label> [# <oneline>]` | Create a merge commit using the original merge commit's message (or the oneline, if no original merge commit was specified); use -c <commit> to reword the commit message |
| `u, update-ref <ref>` | Track a placeholder for the <ref> to be updated to this position in the new commits. The <ref> is updated at the end of the rebase |

<br><br>

## Generating SSH key
1. Check for Existing SSH Keys
Open your terminal and check if SSH keys already exist:

```
ls -al ~/.ssh
```
if none exist create .ssh in home directory "mkdir ~/.ssh"

```
mkdir ~/.ssh
cd ~/.ssh
```
Look for files like id_rsa and id_rsa.pub. If they exist, you can use them instead of creating a new key.

2. Generate a New SSH Key
Use the following command to create a new key pair (replace your_email@example.com with your GitHub email):
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Press Enter to save the key in the default location (~/.ssh/id_rsa). You can also specify a custom name.

Optionally, set a passphrase for added security.

3. Add the Key to the SSH Agent
Start the SSH agent:

```
eval "$(ssh-agent -s)"
```

Add your private key to the agent:
```
ssh-add ~/.ssh/id_rsa
```
4. Copy the Public Key
Copy the contents of your public key (id_rsa.pub) to your clipboard:

```
cat ~/.ssh/id_rsa.pub
```
5. Add the Key to Your GitHub Account
Log in to GitHub.

Navigate to Github Settings > SSH and GPG Keys.

Click New SSH Key.

Paste your public key into the "Key" field and give it a descriptive title.

Click Add SSH Key.

6. Test Your Connection
Verify the setup by running:
```
ssh -T [email protected]
```
If successful, you'll see a message like: "Hi username! You've successfully authenticated."

<br><br>


## Linux🐧 add SSH Agent
To use `eval` with `ssh-agent` in Linux, you can follow these steps:
1. Start the `ssh-agent` by running the following command in the terminal:
   ```
   eval $(ssh-agent)
   ```
2. Add your SSH private key to the `ssh-agent` by running the following command (ssh usually is located in home directory ~/.ssh):
   ```
   ssh-add /path/to/your/private/key
   ```
   Replace `/path/to/your/private/key` with the actual path to your SSH private key file.
3. Enter the passphrase for your SSH private key when prompted.
By running the `eval $(ssh-agent)` command, you start the `ssh-agent` and set up the necessary environment variables. Then, by using `ssh-add`, you add your SSH private key to the agent, allowing you to use it for authentication without having to enter the passphrase each time.

# WINDOWS🪟 SSH
```ps1
$env:GIT_SSH_COMMAND = "ssh -i 'C:\Users\yourusername\.ssh\yourPrivateSSH_KEY'"
git push -u origin main -f -v
```

- make sure open ssh is not disabled in winows services.<br>

check if ssh-agent is running
```
Get-Service ssh-agent
```

Adding SSH-KEY make sure you have uploaded .pub key to github SSH keys
```
ssh-add path/to/your/key
```

- Troubleshooting:

test ssh connection
```
ssh -T git@github.com
```

check added list of ssh keys
```
ssh-add -l
```

remove ssh identities
```
ssh-add -D
```
