# The Weekend Out

Imagine this: A group of friends, tired from their busy university schedules, decides to take a much-needed break.
They plan a weekend getaway to the mountains, where they can relax, hike, and enjoy nature. 
To make sure they don’t forget anything important, they create a shared packing list in a Git repository called “Weekend Out.”

Each friend has their own ideas about what to bring.
Bob thinks they need extra blankets for the chilly nights, while Alice insists on packing a portable grill for a barbecue. 
Carol, the group’s tech enthusiast, wants to bring a drone to capture stunning aerial shots of their adventure.

To keep things organized, they decide to use Git to manage their packing list. 
They create branches for different categories of items: `feature/blankets`, `feature/grill`, and `feature/drone`. 
Each friend adds their items to the list and commits their changes.

However, as they merge their branches into the main list, they encounter a problem: merge conflicts! 
Bob and Alice both added items to the same line in the `packing_list.md` file. 
Now, they need to resolve these conflicts to ensure everyone’s items are included.

Thanks god they have learned about Git and how to resolve conflicts through the following exercises:

## 1. Setting Up the Repository and Adding Items

Clone the repository to your local machine and navigate to the project directory.

```bash
git clone git@github.com:t4d-gmbh/Weekend-Out.git
cd Weekend-Out
```

Create a new branch for the blankets feature and add the items Bob wants to bring.

```bash
git checkout -b feature/blankets
```

open the `packing_list.md` file, add some items and save the file.


Commit your changes and look at the log to see the commit history.

```bash
git add packing_list.md
git commit -m "Add blankets to the packing list"
git log --oneline
```

Get a feeling for the repository and its commit history. 
- What is the status of the repository after the commit? On which branch are you now?
Solution: The repository is clean, and you are on the `feature/blankets` branch.

Play around with the log command to see the commit history in different formats.
Check the man page for an overview of the available options. Some examples are:

```bash
git log --oneline --graph
git log --oneline --author="Alice"
git log --oneline --since="2 days ago"
```

- What information is displayed for each commit?
Solution: The commit hash, the commit message, and the author.

- What is the commit hash and what is its purpose?
Solution: The commit hash is a unique identifier for each commit. It is used to reference commits in Git commands.

- What's the difference between `git log` and `git reflog`?
Solution: `git log` shows the commit history of the current branch including merges and commits which are not part of the current branch history (e.g. commits from other branches). It is useful for tracking changes in the repository over time. On the other hand, `git reflog` shows the history of HEAD movements. This includes branch checkouts, commits, and merges and is useful for recovering lost commits.

Push the branch to the remote repository.

```bash
git push origin feature/blankets
```

- What does the `origin` refer to in the `git push` command? Hint: `git remote -v`.
Solution: `origin` is the default name for the remote repository. It is a shorthand for the URL of the remote repository. You can have multiple remotes with different names. The `-v` flag shows the URLs of the remotes.

- What would be the result of the `git push` command if you didn't specify the branch name?
Solution: The default behavior of `git push` is to push the current branch to the remote repository. If you don't specify the branch name, Git will push the current branch to the remote repository. Think of a situation where you need to explicitly state the name of the remote and why this situation might be useful.

- In which cases would it be useful to have multiple remote repositories?
Solution: Having multiple remotes can be useful when working with different teams or repositories. For example, you might have a remote repository for your team's work (e.g. on a private enterprise server) and another remote repository for open-source contributions (e.g. on a public platform like GitHub, GitLab, or Bitbucket). You can push and pull changes from different remotes depending on the context.

## 2. Add Items on the main branch on the remote repository

Make changes in the `packing_list.md` file on the main branch on the remote repository directly in the browser.

Go to the repository on the remote server and open the `packing_list.md` file. Add some items and commit the changes.

## 3. Merge the Feature Branch into the Main Branch Locally

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/blankets` branch into the main branch.

On your local machine, switch to the main branch and pull the latest changes from the remote repository.

```bash
git checkout main
git pull origin main # or simply `git pull`
```

Before you continue, think about the following questions:
- What is the purpose of the `git pull` command?
Solution: The `git pull` command fetches changes from the remote repository and merges them into the current branch. It is a combination of `git fetch` and `git merge`.

- What is the difference between `git pull` and `git fetch`?
Solution: `git pull` fetches changes from the remote repository and merges them into the current branch. It is a combination of `git fetch` and `git merge`. On the other hand, `git fetch` only fetches changes from the remote repository without merging them. It is useful for checking for updates without affecting your local branch.

- What would happen if you tried to push changes to a branch that has new commits on the remote repository? Try it out!
Solution: If you try to push changes to a branch that has new commits on the remote repository, Git will reject the push and ask you to pull (= fetch + merge) the changes first. This is because the remote branch has new commits that are not in your local branch, and Git wants you to first locally merge the remote with your local changes before pushing you local changes to the remote (remember: the goal is to always keep a healthy reference).

- What is the difference between `git pull origin main` and `git pull`?
Solution: `git pull origin main` fetches changes from the remote repository (origin) and merges them into the current branch (main). It is useful when you want to pull changes from a specific branch on the remote repository. On the other hand, `git pull` fetches changes from the remote repository and merges them into the current branch. It is a shorthand for `git pull origin <current-branch>`.

Merge the `feature/blankets` branch into the main branch.

```bash
git merge feature/blankets
```

- How could you prevent a merge commit from being created when merging branches? Why would you want to do that?
Solution: By default, `git merge` performs a fast-forward merge if possible which is equal to `git merge --ff`. This means that if the branch being merged is directly ahead of the current branch, Git will simply move the branch pointer forward to the latest commit, avoiding the creation of a merge commit. For example, if your current branch is `main` and you want to merge `feature/blankets`: `git merge feature/blankets` if `main` can be fast-forwarded to include all commits from `feature/blankets`, Git will do so without creating a merge commit. If there are divergent commit on both branches, Git will create a merge commit to combine the histories.
Non-default merge scenarios could be:
- *Merge with no fast-forward*: You want to ensure a merge commit is always created, even if a fast-forward merge is possible: `git merge --no-ff feature/blankets`. Git creates a merge commit to preserve the context of the feature branch. This can be useful for maintaining a clear project history, where each feature or bug fix is encapsulated in its own branch and merge commit, e.g., a merge commit clearly indicates that a feature or bug fix branch was integrated into the main branch. This helps in understanding the development history and the context of changes.
- *Rebase before merge*: Remember that `git pull` first fetches the lates changes from the remote with `git fetch` and then either calls `git merge` to fast-forward ahead of the current branch or rebases your current branch of top of those changes. You want to rebase your current branch on top of the branch you are merging from to maintain a linear history: `git pull --rebase`
Note: Read the manuals of `git merge` and `git pull` to understand how different arguments affect each other.

## 4. Resolve the Merge Conflict

Open the `packing_list.md` file and resolve the merge conflict.

1. The file will contain conflict markers `<<<<<<<`, `=======`, and `>>>>>>>` to indicate the conflicting changes. For example when Bob and Alice both added items to the same line in the `packing_list.md` file. Bob added "Extra blankets" directly on the main branch, and Alice added "Sleeping bags" on the `feature/blankets` branch, the file might look like this:
    
    ```plaintext
    Blankets
    <<<<<<< HEAD
    - Extra blankets
    =======
    - Sleeping bags
    >>>>>>> feature/blankets
    ```

2. Edit the file to keep the changes you want to include. In this case, you can keep both items.
    
    ```plaintext
    Blankets
    - Extra blankets
    - Sleeping bags
    ```

3. Save the file and commit the changes.
    
    ```bash
    git add packing_list.md
    git commit -m "Resolve merge conflict"
    ```

_Note_: You can also use a merge tool to resolve the conflict. E.g.: `git mergetool` or in IDEs like Visual Studio Code, you can use the built-in merge tool to resolve the conflict. It will show you the changes from both branches side by side, and you can choose which changes to keep.

## 5. Push the Changes to the Remote Repository

Push the changes to the remote repository.

```bash
git push origin main
```

Now the `feature/blankets` branch is merged into the main branch, and the conflict are resolved. The packing list is updated with the items from both branches.

- Which strategy would you have had to use to merge the feature branch into the main branch without creating a merge conflict?
Solution: To merge the feature branch into the main branch without creating a merge conflict, you could have used a rebase strategy. This would have applied the changes from the feature branch on top of the main branch, avoiding the conflict. However, rebasing changes the commit history and should be used with caution, especially in shared repositories.
-  Is avoiding a merge conflicts generally a good strategy?
Solution: Avoiding merge conflicts is generally not a good strategy. Merge conflicts are a natural part of collaborative development and can help identify conflicting changes early. Resolving conflicts allows team members to communicate and understand each other's changes, leading to better code quality and collaboration. It is important to embrace conflicts as an opportunity to improve the codebase and the team's communication. Avoiding them with rebase invents a history that looks as if the developers never concurrently worked on a same branch. If you value the "logbook" character of a git history (which is often the case in academia) rebases are a no-no!