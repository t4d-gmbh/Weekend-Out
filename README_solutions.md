# The Weekend Out

Imagine this: You and a group of friends (Alice, Bob and Carol), tired from your busy university schedules, decide to take a much-needed break.
You plan a weekend getaway to the mountains, where you can relax, hike, and enjoy nature. 
To make sure you don’t forget anything important, you create a shared packing list in a Git repository called “Weekend Out.”

Everyone has their own ideas about what to bring.
Bob thinks you will need extra blankets for the chilly nights, while Alice insists on packing a portable grill for a barbecue. 
Carol, the group’s tech enthusiast, wants to bring a drone to capture stunning aerial shots of your adventure.

To keep things organized, you decide to use Git to manage the packing list. 

The stategy you agree upon is to create branches for different categories of items: `feature/essentials`, `feature/food`, and `feature/tech`. 

The idea is that everyone adds their items to the list in the specific branch and commits their changes.

### 1. Set up the repository and add items

First, create a new repository using the Weekend Out repository as a template, aka forking.
You can easily do this via the **Use this template** green drop-down list located on the top-right of this page or simply click [here](https://github.com/new?template_name=Weekend-Out&template_owner=t4d-gmbh).

_Note: For the rest of this exercise it is assumed that you also named your repository `Weekend-Out`!_

Clone the repository to your local machine and navigate to the project directory. Don't forget to **add your username** in the directory path!

```bash
git clone git@github.com:<username>/Weekend-Out.git
cd Weekend-Out
```

Create a new `feature/essentials` branch and add the items Bob wants to bring.

```bash
git checkout -b feature/essentials
```

open the `packing_list.md` file, add some items and save the file.


Commit your changes and look at the log to see the commit history.

```bash
git add packing_list.md
git commit -m "Add blankets to the packing list"
git log --oneline
```

Get a feeling for the repository and its commit history. 
- _Q.1._ What is the status of the repository after the commit? On which branch are you now?

---
> **Solution Q.1**: The repository is clean, and you are on the `feature/essentials` branch.
---

Play around with the log command to see the commit history in different formats.
Check the man page for an overview of the available options. Some examples are:

```bash
git log --oneline --graph
git log --oneline --author="Alice"
git log --oneline --since="2 days ago"
```

- _Q.2._ What information is displayed for each commit?

---

> **Solution Q.2**: The commit hash, the commit message, and the author.

---

- _Q.3._ What is the commit hash and what is its purpose?
---
> **Solution Q.3**: The commit hash is a unique identifier for each commit. It is used to reference commits in Git commands.
---

- _Q.4._ What's the difference between `git log` and `git reflog`?
---
> **Solution Q.4**: `git log` shows the current branche's commit history, including merges and commits which are not part of the current branch history (e.g. commits from other branches). It is useful for tracking changes in the repository over time. On the other hand, `git reflog` shows the history of HEAD movements. This includes branch checkouts, commits, and merges, and is useful for recovering lost commits.
---

Push the branch to the remote repository.

```bash
git push origin feature/essentials
```

- _Q.5._ What does the `origin` refer to in the `git push` command? Hint: `git remote -v`.
---
> **Solution Q.5**: `origin`  is the default name for the remote repository and serves as a shorthand for its URL. You can have multiple remotes with different names. The `-v` flag displays the URLs of all remotes.
---

- _Q.6._ What would be the result of the `git push` command if you didn't specify the branch name? Think of a situation where you need to explicitly state the name of the remote and why this situation might be useful.
---
> **Solution Q.6**: The default behavior of `git push` is to push the current branch to the remote repository. If you don't specify the branch name, Git will push the current branch to the remote repository. 
---

- _Q.7._ In which cases would it be useful to have multiple remote repositories?
---
> **Solution Q.7**: Having multiple remotes can be useful when working with different teams or repositories. For example, you might have a remote repository for your team's work (e.g. on a private enterprise server) and another remote repository for open-source contributions (e.g. on a public platform like GitHub, GitLab, or Bitbucket). You can push and pull changes from different remotes depending on the context.
---

### 2. Locally merge the feature branch into the main branch

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/essentials` branch into the `main` branch.

On your local machine, switch to the main branch and pull the latest changes from the remote repository.

```bash
git checkout main
git pull origin main # or simply `git pull`
```

Before you continue, think about the following questions:
- _Q.8._ What is the purpose of the `git pull` command?
---
> **Solution Q.8**: The `git pull` command fetches changes from the remote repository and merges them into the current branch. It is a combination of `git fetch` and `git merge`.
---

- _Q.9._ What is the difference between `git pull` and `git fetch`?
---
> **Solution Q.9**: `git pull` fetches changes from the remote repository and merges them into the current branch. It is a combination of `git fetch` and `git merge`. On the other hand, `git fetch` only fetches changes from the remote repository without merging them. It is useful for checking for updates without affecting your local branch.
---

- _Q.10._ What would happen if you tried to push changes to a branch that has new commits on the remote repository? Try it out!
---
> **Solution Q.10**: If you try to push changes to a branch that has new commits on the remote repository, Git will reject the push and ask you to pull (= fetch + merge) the changes first. This is because the remote branch has new commits that are not in your local branch, and Git wants you to first locally merge the remote with your local changes before pushing you local changes to the remote (_Reminder_: the goal is to always keep a healthy reference).
---

- _Q.11._ What is the difference between `git pull origin main` and `git pull`?
---
> **Solution Q.11**: `git pull origin main` fetches changes from the remote repository (origin) and merges them into the current branch (main). It is useful when you want to pull changes from a specific branch on the remote repository. On the other hand, `git pull` fetches changes from the remote repository and merges them into the current branch. It is a shorthand for `git pull origin <current-branch>`.
---

Merge the `feature/essentials` branch into the main branch.

```bash
git merge feature/essentials
```

- _Q.12._ How could you prevent a merge commit from being created when merging branches? Why would you want to do that?
---
> **Solution Q.12**: By default, `git merge` performs a fast-forward merge if possible, which is equal to `git merge --ff`. This means that if the branch being merged is directly ahead of the current branch, Git will simply move the branch pointer forward to the latest commit, avoiding the creation of a merge commit. For example, if your current branch is `main` and you want to merge `feature/essentials`: `git merge feature/essentials` if `main` can be fast-forwarded to include all commits from `feature/essentials`, Git will do so without by creating a merge commit. If there are divergent commit on both branches, Git will create a merge commit to combine the histories.
> Non-default merge scenarios could be:
> - *Merge with no fast-forward*: You want to ensure a merge commit is always created, even if a fast-forward merge is possible: `git merge --no-ff feature/essentials`. Git creates a merge commit to preserve the context of the feature branch. This can be useful for maintaining a clear project history, where each feature or bug fix is encapsulated in its own branch and merge commit, e.g., a merge commit clearly indicates that a feature or bug fix branch was integrated into the main branch. This helps in understanding the development history and the context of changes.
> - *Rebase before merge*: Remember that `git pull` first fetches the lates changes from the remote with `git fetch` and then either calls `git merge` to fast-forward ahead of the current branch or rebases your current branch of top of those changes. You want to rebase your current branch on top of the branch you are merging from to maintain a linear history: `git pull --rebase`
> _Note_: Read the manuals of `git merge` and `git pull` to understand how different arguments affect each other.
---
- _Q.13._ What would have been the result if you had merged the `main` branch into the `feature/essentials` branch instead?
---
> **Solution Q.13**: If there is no merge conflict, or you resolve the merge conflict in the same way (i.e. chose the same content) then the resulting state would be the same. However, what changes is which branch gets moved forward to the new commit: If you merge `main` into `feature/essentials` the `main` will still point to the same commit, but `feature/essentials` will be updated.
---

### 3. Resolve the merge conflict

Open the `packing_list.md` file and resolve the merge conflict.

1. The file will contain conflict markers `<<<<<<<`, `=======`, and `>>>>>>>` to indicate the conflicting changes.
In this example Carol and you both added items to the same line in the `packing_list.md` file.
If you added `- [ ] some blankets` the file might look like this:
    
    ```plaintext
    ...
    - [ ] sleeping pad
    <<<<<<< HEAD
    - [ ] some blankets
    =======
    - [ ] extrawarm blankets
    >>>>>>> feature/essentials
    ```

2. Edit the file to keep the changes you want to include, for example:
    
    ```plaintext
    ...
    - [ ] sleeping pad
    - [ ] extrawarm blankets
    ```

3. Save the file and commit the changes.
    
    ```bash
    git add packing_list.md
    git commit -m "Resolve merge conflict"
    ```

_Note_: You can also use a merge tool to resolve the conflict. E.g.: `git mergetool` or in IDEs like Visual Studio Code, you can use the built-in merge tool to resolve the conflict. It will show you the changes from both branches side by side, and you can choose which changes to keep.

### 4. Push the changes to the remote repository

Push the changes to the remote repository.

```bash
git push
```

Now the `feature/essentials` branch is merged into the main branch, and the conflict are resolved. The packing list is updated with the items from both branches.

- _Q.14._ Which strategy would you have had to use to merge the feature branch into the main branch without creating a merge conflict?
---
> **Solution Q.14**: To merge the feature branch into the main branch without creating a merge conflict, you could have used a rebase strategy. This would have applied the changes from the feature branch on top of the main branch, avoiding the conflict. However, rebasing changes the commit history and should be used with caution, especially in shared repositories.
---

-  _Q.15._ Is avoiding a merge conflicts generally a good strategy?
---
> **Solution Q.14**: Avoiding merge conflicts is generally not a good strategy. Merge conflicts are a natural part of collaborative development and can help identify conflicting changes early. Resolving conflicts allows team members to communicate and understand each other's changes, leading to better code quality and collaboration. It is important to embrace conflicts as an opportunity to improve the codebase and the team's communication. Avoiding them with rebase invents a history that looks as if the developers never concurrently worked on a same branch. If you value the "logbook" character of a git history (which is often the case in academia) rebases are a no-no!
---

---
---


## Part 2: Feature Branch Development Cycle and Conflict Resolution Online

Now that you've set up the repository and added items locally, it's time to walk through a feature branch development cycle using the project management tools provided by **GitHub**. 
Part 2 will focus on working **entirely online in the remote IDE**.

### 1. Creating a Project Board and Tasks

Carol, the tech enthusiast, wants to bring a drone and suggests creating a dedicated packing list since the drone requires specific additional items.

She starts by creating an Issue to explain how she would like to reorganize your packing list.

- Go to the repository on the remote server: [Weekend Out](https://github.com/t4d-gmbh/Weekend-Out/)
    - [Create your own Weekend-Out Repository](https://github.com/new?template_name=Weekend-Out&template_owner=t4d-gmbh) using this repository as a template OR continue on the repository you used for Part 1.

      _Note: For the rest of this exercise, we assume that you've also named your repository `Weekend-Out`!_

- Go to your own `Weekend-Out` repository and open a new Issue for Carol.
  Name it **`Package list restructuring`** (please use this exact title!) and add a brief description of what Carol wants to do.

### 2. Creating a New Feature Branch Online

Carol has added the items she wants in the list as a comment to the Issue.
With that, you're ready to begin:

- Refresh the Issue page to see Carol's comment (actually posted by a GitHub bot) with the items she wants to add.

- Create a new branch directly from the Issue's web view.
  (You find this option on the right under "Development")

- Keep the suggested branch name as is, and checkout the newly created branch on your device.

- On the webinterface of your repository, first switch to the view of the newly created branch (in the same line as the "Code" button towards the very left, select the branch name from the dropdown).

- When viewing the content of the new branch, create a new markdown file for Carol's drone list (by clicking on the `+` button next to "Code") and add the items she mentioned in her comment.

- Once you’ve made your changes, push them to the remote repository.

### 3. Create a Pull Request

Now that you've implemented the requested feature and pushed your branch back to the remote repository, you can create a pull request to fromally propose merging your feature branch into `main`.

- Go back to your `Weekend-Out` Repository on **GitHub**. You should see a notification bar prompting you to open a Pull Request. If you don't see it, click on "Pull requests" and then "New pull request".

- Assign yourself to the Pull Request, and go ahead and create it.

- You will be redirected to your pull request's details. For now, ignore the "Checks", but take a look at the "Commits" and "Files changed" tabs.

### 4. Merging the Feature Branch into Main

If you are satisfied with you edits, you can consider merging your feature branch into the healthy reference `main`.

- Remember, it's your responsability to ensure the changes you introduce are compatible with the `main` branch at the time of merging - not based on a prior state!

- If everything looks good, merge your branch by clicking on the green "Merge pull request" button at the bottom of the Pull Request page. Confirm by clicking "Merge".

### 5. Inspect What Just Happened

You've just completed a Feature Branch cycle! 🥳🎈Congrats!

- Go to the `Issues` tab of your `Weeken-Out` repository and check the issue you created earlier.
  If everything went according to plan, your Issue should now be marked as closed.
  
- Now, head to the "Code" tab and have a look at the content of the repository.
  You should see the new file for Carol's done list - so far, so good!

  But wait! **There is another file** named `Carols_drone_list.md` with the commit message: `"Adding Carols done list"`.
  Click on the message, and you will be directed to the detailed view of the commit with which Alice added that file.

It seems not everyone was informed that you were in charge of the drone list and Alice went ahead and took care of it.

Now, without casting blame around, it would be helpful to understand how the healthy reference branch ended up with two files for the same list.

- _Q.1._ Who was first to add the list to `main`?
- _Q.2._ What did you do wrong, if anything?
- _Q.3._ What did Alice do wrong, if anything?

_Hints:_

  - The "Insights" tab in your `Weekend-Out` Repository has a `Network` view (Note: Only accessible in `public` Repositories).
    The `Network` view depicts a chronologically ordered graph with all commits.

    _Alternatively:_ If you prefer not to make your `Weekend-Out` repository public, you can view the "Network" in your command line:

    ```bash
    git checkout main
    git pull
    git log --all --decorate --oneline --graph
    ```

- _Q.1._ Who was first to add the list to `main`?

---

> **Solution Q.1**: Alice pushed changes to the `main` branch while you were still working on your feature branch, so Alice was first! 

---

- _Q.2._ What did you do wrong, if anything?

---

> **Solution Q.2**: This situation is a bit awkward, but it is always each person's responsibility to ensure their feature branch is up to date with `main` _before_ merging. In this case you should have checked if your changes were compatible with the state of the healthy reference branch.

---

- _Q.3._ What did Alice do wrong, if anything?

---

> **Solution Q.3**: Actually, Alice also contributed to this situation. She did not check that there was an ongoing feature branch cycle for the exact same edit that she intended to do. When working with remote services, such as **GitHub** or **GitLab** your first go-to place for questions, suggestions, and alike should always be the list of Issues (opened and closed). If Alice had checked before contributing she would have spotted your Issue, the related Pull Request and that you were assigned for that task. She could have left a comment on the Issue or Merge Request that she would like to contribute and the two of you could have decided how to distribute the work.

---
