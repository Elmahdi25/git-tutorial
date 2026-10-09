<div align="center">
  <h1>My First Steps with Git 🌱</h1>
  <p><strong>Edit. Review. Save. Learn. Repeat.</strong></p>
  <p>A beginner-friendly learning journal about saving versions of my code and understanding what Git does.</p>

  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" alt="Git">
  <img src="https://img.shields.io/badge/Terminal-PowerShell-5391FE?style=for-the-badge" alt="PowerShell">
  <img src="https://img.shields.io/badge/Project-Learning%20by%20Practicing-2563EB?style=for-the-badge" alt="Learning project">

  <p>
    <a href="#preview">Preview</a> ·
    <a href="#what-you-can-explore">Topics</a> ·
    <a href="#run-it-locally">Practice locally</a> ·
    <a href="#commands-from-the-video">Video commands</a> ·
    <a href="#extra-commands-i-practiced">Extra commands</a> ·
    <a href="#what-i-learned">What I learned</a>
  </p>
</div>

## Why I built this

While learning web development, I wanted a better way to save my progress than creating folders named `final`, `final-2`, and `final-really-final`. 😄

This learning journal records the Git fundamentals I practiced while following a tutorial by **Simon from SuperSimple.dev**. The main exercise recreates a document's version-history experience for code: save versions, inspect previous versions, and restore old content.

I also collected the useful commands I practiced separately so I can revisit them without mixing them up with the lesson.

**Scope:** the supplied video transcript covers local Git. It mentions GitHub and further branching lessons as the next steps, but does not demonstrate GitHub upload commands. Publishing this README on GitHub does not mean those later lessons are covered here.

## Preview

A typical checkpoint after saving a version:

```text
On branch main
nothing to commit, working tree clean
```

A short history might look like this:

```text
c3d4e5f Version 1 restored
b2c3d4e Version 3
a1b2c3d Version 2
123abcd Version 1
```

These are illustrative outputs, not the actual commit IDs of this repository. A clean working tree describes local changes; it does not confirm an upload to GitHub.

![git log](docs/1.png)

<br>

![git log --all --graph](docs/2.png)

## What you can explore

| Topic | What I practiced |
| --- | --- |
| Repository setup | Starting Git inside a project folder |
| Identity | Setting the author name and email for future commits |
| Staging | Selecting the versions of files to save next |
| Commits | Saving a snapshot with a useful message |
| History | Reading commits and understanding `HEAD` |
| Undoing | Separating unstaging from discarding edits |
| Earlier versions | Viewing old commits and restoring old file contents |
| Shortcuts | Creating Git aliases |
| Ignored files | Keeping selected untracked files out of commits |
| VS Code | Reviewing, staging, and unstaging through Source Control |

### The three places to remember 🎒

Imagine doing homework:

| Real life | Git |
| --- | --- |
| The notebook you are still editing | Working tree: your current files |
| A photo you selected to hand in | Staging area: the snapshot prepared for the next commit |
| Your album of previously saved photos | Commit history |

`git add` prepares a snapshot. `git commit` records it in history. If you change the file after staging, the prepared snapshot stays the same until you stage the updated content again.

## Built with

- **Git** — local version control.
- **PowerShell** — terminal commands on Windows.
- **VS Code** — editing and reviewing changes with Source Control.
- **Markdown** — this learning journal.

Git is the tool that manages history. GitHub is a service that can host repositories online. They are connected ideas, but they are not the same thing.

## Run it locally

### 1. Prepare a practice folder

Use a separate exercise folder, not a project with important unsaved work. Git must already be installed.

```powershell
New-Item -ItemType Directory -Path "$HOME/git-video-practice"
Set-Location "$HOME/git-video-practice"
New-Item -ItemType Directory -Path "src"
```

If the folder already exists, enter it instead of creating it again.

### 2. Create the example files

```powershell
@(
    'console.log("config.js");'
    'console.log("Version 1");'
) | Set-Content -Encoding utf8 config.js

@(
    'console.log("src/index.js");'
    'console.log("Version 1");'
) | Set-Content -Encoding utf8 src/index.js
```

These are practice snippets based on the lesson's example. You do not need to execute the JavaScript to practice Git.

### 3. Save the first version

Replace the example identity with your own. These commands run locally.

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git init
git status
git add .
git commit -m "Version 1"
git log
```

The initial branch may be named `main` or `master`. Use its actual name when returning to it later. The extra-command section shows how to explicitly start on `main`.

### 4. Build the history

Edit both files in VS Code: change `Version 1` to `Version 2`, save, then run:

```powershell
git add .
git commit -m "Version 2"
```

Repeat with `Version 3`:

```powershell
git add .
git commit -m "Version 3"
git log --all --graph
```

You now have versions to inspect and restore. Press **`q`** if the history opens in a scrolling viewer.

## Commands from the video

Examples use the lesson's `config.js`, `change.js`, and `src` paths. Use paths that actually exist in your exercise. Commands in the tables are alternatives to understand, not a script to run from top to bottom.

### 1. Navigate and initialize

| Command | What it does |
| --- | --- |
| `git` | Displays Git's general usage information; the lesson uses it to check installation |
| `ls` | Lists items in the current folder; in PowerShell it aliases `Get-ChildItem` |
| `cd ~/Desktop/git-tutorial` | Enters the example project folder; adapt the path to your computer |
| `git init` | Creates `.git` and initializes the current folder as a repository |
| `git status` | Shows the current branch and staged, unstaged, and untracked changes |

`git init` does not automatically stage files, create a commit, or upload anything. `.git` contains the repository's metadata and history; your working files stay outside it.

### 2. Configure the author

```powershell
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

`--global` sets defaults for repositories used by your account. This is commit identity, not a GitHub login. Changing these settings does not automatically rewrite old commits.

### 3. Stage and save

| Command | What it does |
| --- | --- |
| `git add config.js` | Stages the current content of one file |
| `git add src` | Stages eligible changes under that folder, including subfolders |
| `git add .` | Stages eligible changes in the current folder and below |
| `git commit -m "Version 1"` | Saves staged content with a message |
| `git commit -m "Version 2"` | Saves the next staged snapshot |
| `git commit -m "Version 3"` | Saves another staged snapshot |

The dot means **the current folder**. Run from the repository root when you intend to include changes throughout the project. Ignored untracked files are normally excluded.

For a real project, a message such as `Add responsive navigation` describes the work better than `Version 2`.

### 4. Correct the latest commit

After creating a forgotten `change.js`, stage it and amend:

```powershell
git add change.js
git commit -m "Version 1" --amend
```

This replaces the latest commit with a new commit containing the correction. It can also correct the message. The commit ID changes; practice this with your own unpublished commits.

### 5. Unstage or discard edits

| Command | Effect |
| --- | --- |
| `git reset config.js` | Unstages that file's changes; keeps edits in the working file |
| `git reset src` | Unstages changes under `src`; keeps working files |
| `git reset .` | Unstages changes in the current folder and below |
| `git checkout -- config.js` | Replaces the working file with its staged version |
| `git checkout -- change.js` | Does the same for `change.js` |
| `git checkout -- .` | Discards unstaged edits to tracked files in the current folder and below |

**Unstaging means “not ready to save.” Discarding means “remove these edits.”**

The `--` separates options from paths. The checkout commands above can lose unstaged work, so review changes first. They restore from the staging area, which may differ from the latest commit. They do not delete ordinary untracked files.

### 6. Read commit history

| Command | What it shows |
| --- | --- |
| `git log` | History reachable from the current `HEAD`, newest first |
| `git log --all` | History reachable from all refs, plus `HEAD` |
| `git log --graph` | The current history with a text graph of ancestry |
| `git log --all --graph` | The graph across refs and `HEAD` |

Each commit has an ID, author, date, and message. **`HEAD` indicates your current position**: normally the current branch, or a particular commit when detached.

`--all` does not mean every commit ever created, including abandoned commits. It expands which references Git starts from.

### 7. Visit an earlier version

Copy a real commit ID from `git log`. Replace `COMMIT_ID` below; it is a placeholder.

```powershell
git checkout COMMIT_ID
```

This updates tracked files to that commit and enters **detached HEAD** mode. It lets you inspect the old version without moving your existing branch backward. Start with a clean working tree to avoid mixing in local edits.

Return to the branch used by the tutorial:

```powershell
git checkout master
```

Or, if your branch is named `main`:

```powershell
git checkout main
```

The lesson also demonstrates editing from an old commit and saving:

```powershell
git add .
git commit -m "Version 1 updated"
```

That creates a new line of history from the old version. It does not restore old content on your original branch. In detached HEAD, the new commit is not automatically attached to a named branch, so this is a lesson demonstration rather than the normal workflow to keep using.

### 8. Restore old content without moving HEAD

First return to `main` or `master`. Replace `COMMIT_ID` with the earlier version you want to use.

| Command | Content restored |
| --- | --- |
| `git checkout COMMIT_ID -- config.js` | One file from the earlier commit |
| `git checkout COMMIT_ID -- src` | Tracked paths from that version under `src` |
| `git checkout COMMIT_ID -- .` | Tracked paths from that version in the current folder and below |

These commands copy selected old content into **both the working tree and staging area**, while keeping `HEAD` on the current branch. The explicit `--` makes the path selection clear.

They overwrite selected local content. Also, this form normally uses overlay behavior: files absent from the chosen old version are not automatically removed, so it may not reproduce that entire old directory exactly.

Review and save the restored content:

```powershell
git status
git commit -m "Version 1 restored"
git log --all --graph
```

**Viewing an old commit changes where you are looking. Restoring old file content changes what you will save next.**

### 9. Create Git shortcuts

```powershell
git config --global alias.s "status"
git config --global alias.cm "commit -m"
git config --global alias.co "checkout"
```

After configuring them:

| Shortcut | Equivalent |
| --- | --- |
| `git s` | `git status` |
| `git cm "Add introduction"` | `git commit -m "Add introduction"` |
| `git co main` | `git checkout main` |

These are Git aliases. They do not create PowerShell aliases such as `cd` or `pwd`.

### 10. Ignore selected files

The lesson creates a `.gitignore` file containing:

```gitignore
secrets.txt
```

This keeps an untracked `secrets.txt` out of normal staging and status output. Save the ignore rules themselves:

```powershell
git add .
git commit -m "Add gitignore"
```

`.gitignore` does not stop tracking files already tracked, and it does not erase content from older commits.

### 11. Remove Git from a disposable copy

The video copies the project first, then deletes `.git` **in the copy**.

In Bash or Git Bash:

```bash
rm -rf .git
```

In PowerShell:

```powershell
Remove-Item -LiteralPath .git -Recurse -Force
```

**This deletes that copy's local history, branches, and repository settings.** Working project files remain. It does not delete a repository hosted on GitHub. The Bash `-rf` syntax does not work with PowerShell's `rm` alias.

Afterward, `git log` should report that you are not in a repository, unless the folder is inside another repository. This is a removal demonstration, not a routine step in the practice workflow.

## Extra commands I practiced

These commands came from my separate practice, rather than the supplied video segment. Examples are references; choose only the command that matches your goal.

### Setup, help, and status

| Command | Purpose |
| --- | --- |
| `git --version` | Check the installed Git version |
| `git init -b main` | Initialize a new repository with the initial branch named `main` |
| `git config --global user.name` | Read the configured global author name |
| `git config --global user.email` | Read the configured global author email |
| `git help -a` | List available Git commands |
| `git status -h` | Show brief status help |
| `git commit -h` | Show brief commit help |
| `git status -s` | Show compact status output |
| `git remote -v` | List configured remote addresses; a URL does not prove an upload |

For Windows installation or updating, I also practiced these PowerShell commands:

```powershell
# Install if Git is not installed
winget install --id Git.Git -e --source winget

# Update an installation recognized by winget
winget upgrade --id Git.Git -e --source winget
```

Run the appropriate one, then reopen the terminal and check `git --version`.

### Review changes before saving

| Command | Comparison |
| --- | --- |
| `git diff` | Working tree versus staging area: unstaged changes |
| `git diff --cached` | Staging area versus latest commit: staged changes |

`git diff` does not show the contents of untracked files. Stage a new file before reviewing its content with `git diff --cached`.

My review routine for an already tracked `index.html`:

```powershell
# After editing and saving index.html
git diff
git add index.html
git diff --cached
git commit -m "Add project introduction"
git status
```

If I edit after `git add`, I need to stage again to include that newer version. The same file can have both staged and unstaged changes.

### Use clearer undo commands

| Older form from the video | Modern form I practiced | Result |
| --- | --- | --- |
| `git reset index.html` | `git restore --staged index.html` | Unstage; keep working edits |
| `git reset .` | `git restore --staged .` | Unstage within the current folder |
| `git checkout -- index.html` | `git restore index.html` | Discard unstaged edits; restore staged content |
| `git checkout -- .` | `git restore .` | Do the same for tracked files within the current folder |

The option is **`--staged`**, with a final `d`. These pairs cover these particular jobs; `reset` and `checkout` have other uses too.

### Customize history output

| Command | Purpose |
| --- | --- |
| `git log --oneline` | One short commit ID and message per line |
| `git log -3` | Latest three commits in the current history |
| `git log --oneline -3` | Latest three in compact form |
| `git log --stat` | File change statistics for each commit |
| `git log -p` | Patches showing changes made by commits |
| `git log --oneline --graph --all` | Compact history graph across refs |
| `git log -- README.md` | History affecting this path |
| `git log --all --format="%an"` | Author names without emails or dates |
| `git log --all --format="%h \| %an \| %s"` | Short ID, author name, and message |

In the last command, the pipes belong inside the quoted format string. Use the following copyable form:

```powershell
git log --all --format="%h | %an | %s"
```

### Manage ignored files and deletions

```powershell
# Append rules without replacing existing .gitignore content
".env" | Add-Content .gitignore
"node_modules/" | Add-Content .gitignore
"*.log" | Add-Content .gitignore

# Check ignored files and the rules responsible
git status --ignored
git check-ignore -v .env debug.log
```

`*.log` matches names ending in `.log`. `node_modules/` targets directories. Use fake values, such as `FAKE_TOKEN=practice-only`, for exercises.

For an already tracked file you want to ignore:

```powershell
"notes.txt" | Add-Content .gitignore
git rm --cached -- notes.txt
git add .gitignore
git commit -m "Stop tracking local notes"
```

`git rm --cached` removes the file from Git's index but keeps your working copy. Older commits still contain it.

For a tracked file you actually want to delete:

```powershell
git rm index.html
git commit -m "Remove index.html"
```

That deletes the working file and stages its deletion. Use it only when deletion is intended.

### PowerShell commands that helped me

These manage files and folders; they are not Git commands.

| Command | Purpose |
| --- | --- |
| `New-Item -ItemType Directory -Path "practice"` | Create a folder |
| `New-Item -ItemType File -Path "notes.txt"` | Create an empty file |
| `Set-Location "practice"` or `cd "practice"` | Enter a folder |
| `cd ..` | Go up one folder |
| `cd ../..` | Go up two folders |
| `Get-Location` or `pwd` | Show the current location |
| `Rename-Item -Path "practice" -NewName "git-practice"` | Rename a folder from its parent |
| `Get-Content index.html` | Display a file's content |
| `"New content" \| Set-Content index.html` | Replace a file's content, or create it |
| `"Extra content" \| Add-Content index.html` | Append content, or create the file |
| `code index.html` | Open the file in VS Code if the `code` command is available |
| `Remove-Item notes.txt` | Delete a file directly, without the Recycle Bin |
| `Test-Path .git` | Check whether `.git` exists at the current location |

`$HOME` means your user home folder. Quote paths containing spaces. `@(...)` creates a PowerShell array, and the pipe `|` passes output to the next command.

**My useful correction:** `Set-Content` replaces text; `Add-Content` adds text. When I want a specific edit inside an HTML document, VS Code makes it easier to place it correctly.

### A first look at feature branches

We also discussed this simple workflow separately. It goes beyond the video segment's brief introduction to branching. Start from a committed project on `main` with a clean working tree.

```powershell
git switch -c new-navbar
# Edit and save the navbar
git add .
git commit -m "Improve navbar"
git switch main
git merge new-navbar
```

`switch -c` creates and enters a branch; `switch main` returns to the starting branch; `merge` brings the feature's history into it. If both branches change overlapping content, resolving a merge conflict may be necessary. That is a future learning topic.

## What I learned

- **Saving a file is not committing it.** The editor saves working content; Git records a version only when I commit.
- **Staging is a choice.** I select the content I want in the next commit.
- **Unstaging keeps my edits.** Discarding unstaged edits removes them.
- **History has structure.** A commit ID identifies a snapshot, a branch points to a line of development, and `HEAD` tells Git where I am.
- **Viewing and restoring differ.** I can inspect an old commit or copy its content into my current branch.
- **A repository contains branches.** Creating a branch does not create another project folder.
- **Ignore rules are not history erasers.** They normally affect untracked files.
- **Local commits are local.** Git does not automatically send them to GitHub.

### How the practice project changed

| Stage | Change made | What happened in Git |
| --- | --- | --- |
| Version 1 | Added the initial JavaScript snippets | Created the first saved snapshot |
| Amend demonstration | Added a forgotten file or corrected the message | Replaced the latest commit with a corrected one |
| Version 2 | Updated the version text in the example files | Recorded a new snapshot |
| Version 3 | Updated the version text again | Extended the current history |
| Viewing earlier versions | Checked out an earlier commit | Changed the viewed snapshot without rewriting the original branch |
| Restoration | Copied Version 1 content into the current branch | Prepared old content as a new change, then committed it |
| Ignore rules | Added a practice secret filename to `.gitignore` | Excluded matching untracked files from normal staging |
| Removal demonstration | Deleted `.git` in a disposable copy | Removed that copy's repository metadata and local history |

This table describes the lesson's exercise. The repository's actual `git log` is the record of which steps were committed here.

## Next improvements

- [ ] Learn how to connect a local repository to GitHub and publish commits.
- [ ] Practice fetching and pulling remote changes.
- [ ] Explore feature branches more deeply and resolve merge conflicts.
- [ ] Learn pull requests and collaboration workflows.

These are future goals, not skills demonstrated by the supplied video segment.

## Feedback and contributions

If an explanation is confusing or you notice an incorrect command, feedback is welcome. Include the command, your terminal type, and what happened so the explanation can be improved.

## Credits and license

Learning notes compiled by **[Elmahdi Benabbou](https://github.com/Elmahdi25)**.

The local Git exercise is based on the supplied transcript of a tutorial by **Simon from [SuperSimple.dev](https://supersimple.dev)**. Explanations here are rewritten as personal study notes. Additional commands come from my separate practice.


## Support the project

If these notes help you understand Git, a star or a useful correction is appreciated. You can find my other learning projects on **[my GitHub profile](https://github.com/Elmahdi25)**.

---

<div align="center">
  <strong>One change, one commit, one step forward. 🚀</strong>
</div>
