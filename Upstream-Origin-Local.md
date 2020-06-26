# Workflow between Upstream-Origin-Local Computer

# Concepts explanation
**1. Fork a repo:**
   - A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project
   - It uses someone else's project as a starting point for your own idea
   - How to fork? In the top-right corner of the page, click **Fork**. ![Fork](https://github.com/chunxia2020/Github-Configuration/blob/master/Images/fork_button.jpg)

**2. Workflow between Upstream-Origin-Local Computer:**

The relationship between the three is shown below:
<img src="https://github.com/chunxia2020/Github-Configuration/blob/master/Images/WorkFlow.png" width="300" height="300">
1. **Fork a repository** from Upstream to My repository copy. This is done in GitHub Web
  - Public: Just fork it
  - Private: Get invitation link, then fork it
2. **SSH key setup**
  - Git command（Windows）:
  ```python
  $ cd ..          # Go to the main directory
  $ ssh-keygen -t rsa -b 4096 -C "chunxia@knights.ucf.edu" # include my GitHub email address
  $ cat .ssh/id_rsa.pub
  ```
  Copy all the output from the last command, go to my GitHub Web--Settings(Top right corner)--SSH and GPG keys--`New SSH key`--paste

  - Git command（Linux）:

  ```Python
  # Check first whether git command is installed
  $ git --version  # Check if git has been installed and check its version
  $ ssh-keygen -t rsa -b 4096 -C "chunxia@knights.ucf.edu" # include my GitHub email address
  # This line in the output: Your identification has been saved in /home/ubuntu/.ssh/id_rsa. Your public key has been saved in /home/ubuntu/.ssh/id_rsa.pub.
  $ cat /home/ubuntu/.ssh/id_rsa.pub
  ```
  The other procedures needed are the same as setting up for windows
3. **Clone to local PC**
  - ATOM : `ctrl+shift+p`, then `GitHub: Clone`. Put down the SSH or HTML of the repository copied from the previous step and the local folder directory
  - Git command: Open **Git Bash**
  ```ruby
  # ---- Navigate to a desired directory ------
  $ cd ..          # Go to the main directory
  $ cd Documents   # Navigate to a targeted folder
  $ ls             # List all the files
  # ---- Clone with git  ----------------------
  $ git clone git@github.com:chunxia2020/chips.git # clone from this SSH
  # ---- Go to the cloned folder  -------------
  $ cd chips       # !!!Very important!!!!
  $ ls             # Show visible files
  $ ls -la         # Show visible and invisible files
  # ---- Go to the cloned folder  -------------
  $ git remote     # Manage set of tracked repositories !!! This only works when you are at the [chips] folder !!!
  origin
  $ git remote -v  # Shows URLs of remote reps when listing your current remote connections
  origin  git@github.com:chunxia2020/chips.git (fetch)
  origin  git@github.com:chunxia2020/chips.git (push)
  ```
 4. **Interact with the Upstream**
    - Change in local PC, push to the forked repo
       - ATOM : save-commit-comment-push
       - Git command:
     ```ruby
     # --- Before using commit command ---
     $ git add            # Add changes
     $ git rm             # remove files from the working tree and the index
     $ git status         # Track changes in the branch to commit
     # --- commit ------------------------
     $ git commit -a      # stage all files
     # --- push --------------------------
     $ git push
     $ git status         # Track changes in the branch to commit
     ```
    Then submit pull request to the upstream in GitHub Web

    - Merge changes from the Upstream: This has to be done with git commands and ATOM
       1. Pull from Upstream using git commands:
       ATOM needs to be open
       ```ruby
       # ----- Add remote upstream --------------
       $ git remote add upstream git@github.com:jetouma/chips.git # pull from upstream SSH
       # ----- Check remotes --------------------
       $ git remote -v
       origin       git@github.com:chunxia2020/chips.git (fetch)
       origin       git@github.com:chunxia2020/chips.git (push)
       upstream        git@github.com:jetouma/chips.git (fetch)
       upstream        git@github.com:jetouma/chips.git (push)
       # ----- Pull from the remote upstream -----
       $ git pull upstream master
       # ----- Show all the history --------------
       $ git log
       ```
       2. Merge changes in ATOM:
          - In ATOM, simply choose the change one wants, stage changes
          - Then, save file again to get rid of formatting issue, stage changes
          - Commit all the changes and push to my repository
