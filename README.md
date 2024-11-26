# Basic Git Commands

### 1. Check git installed version : `git version`

### 2. Configure Git properties (user name and email)
- Configure UserName : `git config --global user.name "Test User"`
- Configure User Email : `git config --global user.email "xyz@test.com"`
- Configure Default repo branch : `git config --global init.defaultbranch "Default_Branch_Name"`
- List properties : `git config --global --list`

> **Note :** global flag sets properties globally in ~/.gitconfig file

### 3. Creating or initializing a local repo
- Initializing local repo : `git init <local_repo_name>`
- Initializing local repo with default branch : `git init -b <default_branch_name> <local_repo_name>`

### 4. Cloning Remote Repo
- `git clone <remote_repo_url>`
    - *e.g.:* `git clone https://github.com/kunalsharma7292/git-learning.git`
    
> **Note :** clone command automatically establishes a relationship with remote repo and names that reference "origin"


### 5. Add/Attach Remote repo to/with a local Repo
- Add remote repo to local repo :  `git remote add <reference_name> <remote_repo_url>`
    - *e.g.:* `git remote add origin https://github.com/kunalsharma7292/git-learning.git`
- Verify remote repo is linked successfully with local repo : `git remote -v`

### 6. Check Status of repo/branch
- List all changes in working directory/staging area, and info about local and remote repo : `git status`

### 6. Committing Changes
- Add all files/changes to staging area - (both tracked and untracked files) : `git add .`
- Commiting Staged changes : `git commit -m "<Commit_Message>"`
- Express commit for Tracked Files (no separate git add command is required to run) : `git commit -am "<Commit_Message>"`

### 7. Pull and Push changes from/to remote repo
- Pull changes from a remote branch : `git pull origin <branch_name>`
- Push changes of a local branch : `git push origin <branch_name>`
- Push changes to a particular remote branch : `git push origin <local_branch>:<remote_branch>`
- Push changes and set local branch to track remote repo branch i.e set remote as upstream branch : `git push -u origin <branch_name>`

> **Note :** if local branch is set to track remote repo branch - then we can directly use git pull and push commands without specifying origin refernce and branch name.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.g.: If remote is set as upstream.  Use: `git pull`, `git push`

### 8. Fetch new commits/branches/tags from remote repo and update references for remote-tracking branches(e.g., origin/main) but do not merge in changes in working directory
- `git fetch origin <branch_name>`

> **Note :** pull = fetch + merge (pull automatically merges remote changes in working directory directory)

### 8. Discarding files or resetting changes from Staging area and working directory
- Unstage changes from Staging area : `git reset HEAD <file_name>`
- Discard changes from working directory : `git checkout -- <file_name>`

### 9. Branch Commands
- List local branches : `git branch`
- List all branches (remote + local) : `git branch -a`
- List remote branches : `git branch -r`
- Create new branch : `git branch <branch_name>`
- Switch to new branch : `git checkout <branch_name>`
- Create and switch to branch (Single Command) : `git checkout -b <branch_name>`
- Rename branch name : `git branch -m <old_branch_name> <new_branch_name>`
- Delete Local branch : `git branch -d <branch_name>`
- Delete Remote Repo Branch : `git push origin --delete <branch_name>`
- Create local branch and set a remote repo branch as upstream branch for this local branch (useful if remote branch with same name already exists and link with local branch)  
`git branch <local_branch_name> origin/<remote_branch_name>`  
`git checkout -b <local_branch_name> origin/<remote_branch_name>`
- Set Remote branch as upstream branch for local branch (useful if both local and remote branch already exists)  
`git branch --set-upstream-to=origin/<remote_branch_name> <local_branch>`

### 10. Stashing - temporarily save changes and clean up working directory
- Save changes temporarily (staged and working directory changes) : `git stash`
- Stash including untracked files : `git stash -u`
- Stash with a message (can be used for tracking purposes) : `git stash save -m "<Message>"`
- List all stashes : `git stash list`
- Apply Changes from last stash : `git stash apply`
- Drop last stash : `git stash drop`
- Apply changes from last stash and delete it : `git stash pop`
- Apply a particular stash : `git apply <stash@{index}>`
- Drop a particular stash : `git drop <stash@{index}>`
- Remove all stash and empty stash list : `git stash clear`
- Show changes in a stash  
`git stash show`
`git stash show <stash@{index}>`
- Create and pop stash changes in a new branch  
`git stash branch <new_branch_name>`  
    - action performed by above command: create and checkout of new branch and pop(apply and drop) last stash changes

### 11. Tagging - (mark significant event or milestones in the repo -- Tag are labels only that can be applied to any commit in history)
- Creating and attach lightweight tag with Head commit: `git tag <tag_name>`
- List all tags : `git tag --list`
- Delete a tag : `git tag --delete <tag_name>`

- Show changes in associated commit (We can use tag name as refernce in other git commands like diff command as well)  
`git show <tag_name>`

- Create Annotated tag (Similar to light-weight tag - contains additional info associated with tag - in particular a message similar to a commit message (for eg: release notes/docs))  
`git tag -a <tag_name>`
`git tag <tag-name> -m "<Message- Release Docs>"`

- Tag a particular commit : `git tag -a <tag_name> <commit_id>`

- Update a tag : 
`git tag <tag_name> -fm "<new_message>"` -> (Annotated-Tag - message provided)  
`git tag <tag_name> -f <new_commit_id> -m "<new_message>"` -> (Annotated tag - message provided)  
`git tag <tag_name> -f` -> (Annotated to lightweight tag)

- Push a tag to remote repo (pushes all commits upto this tag to remote repo)  
`git push origin <tag_name>`

- Push all tags to remote repo  
`git push origin <branch> --tags`

- Delete tag from remote repo : `git push origin :<tag_name>`
    - tells git to push nothing against this tag in remote repo - git hub will delete the tag - refer release window on git hub
    - corresponding commits/changes will not be removed from github
    - tag still present on local repo and can be pushed again 

### 12. Rebasing  
(Rewind current changes-commits -> apply commit of target branch on current branch and rewrite current branch commits)

- Rebase changes of a branch on current branch : `git rebase <branch_name>`
- Abort Rebase in case on conflicts : `git rebase --abort`
- Continue Rebase (used when conflicts have been resolved - if any present) - `git rebase --continue`
- Pull with rebase : `git pull --rebase origin <branch_name>`

### 13. Compare Changes
- List differences b/w working directory and staging area code. (All changes will be listed)  
`git diff`
- List differences b/w working directory and last-commit / head : `git diff HEAD`
- List differences b/t Last Commit / head and staging area : `git diff --staged HEAD`
- List differences using diff tool like p4merge  
`git difftool` , `git difftool HEAD` , `git difftool --staged HEAD`
- List differences of a particular file : `git diff -- <file_name>`
- Compare commits, branches and tags  
`git diff <commid_id1> <commit_id2>`, `git diff <branch1> <branch2>`, `git diff <tag1> <tag2>`
- Compare local repo branch with remote repo branch : `git diff <local_repo_branch> origin/<remote_repo_branch>`

> **Note :** difftool must be configured first to use difftool command otherwise git prompts to open OS default difftool