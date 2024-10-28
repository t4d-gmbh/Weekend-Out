# The Weekend Out Git Exercise

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

### 1. Set up the repository and add items

First, create a new repository using the Weekend Out repository as a template, aka forking.
You can easily do this via the **Use this template** green drop-down list located on the top-right of this page or simply click [here](https://github.com/new?template_name=Weekend-Out&template_owner=t4d-gmbh).
_Note: For the rest of this exercise it is assumed that you also named your repository `Weekend-Out`!_

Clone the repository to your local machine and navigate to the project directory. Don't forget to **add your username** in the directory path!

```bash
git clone git@github.com:<username>/Weekend-Out.git
cd Weekend-Out
```

Create a new `feature/blankets` branch and add the items Bob wants to bring.

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
- _Q.1._ What is the status of the repository after the commit? On which branch are you now?


Play around with the log command to see the commit history in different formats.
Check the man page for an overview of the available options. Some examples are:

```bash
git log --oneline --graph
git log --oneline --author="Alice"
git log --oneline --since="2 days ago"
```

- _Q.2._ What information is displayed for each commit?
- _Q.3._ What is the commit hash and what is its purpose?
- _Q.4._ What's the difference between `git log` and `git reflog`?

Push the branch to the remote repository.

```bash
git push origin feature/blankets
```

- _Q.5._ What does the `origin` refer to in the `git push` command? Hint: `git remote -v`.
- _Q.6._ What would be the result of the `git push` command if you didn't specify the branch name? Think of a situation where you need to explicitly state the name of the remote and why this situation might be useful.
- _Q.7._ In which cases would it be useful to have multiple remote repositories?

## 2. Add items on the main branch on the remote repository

Make changes in the `packing_list.md` file on the main branch on the remote repository directly in the browser.

Go to the repository on the remote server and open the `packing_list.md` file. Add some items and commit the changes.

## 3. Locally merge the feature branch into the main branch

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/blankets` branch into the main branch.

On your local machine, switch to the main branch and pull the latest changes from the remote repository.

```bash
git checkout main
git pull origin main # or simply `git pull`
```

Before you continue, think about the following questions:
- _Q.8._ What is the purpose of the `git pull` command?
- _Q.9._ What is the difference between `git pull` and `git fetch`?
- _Q.10._ What would happen if you tried to push changes to a branch that has new commits on the remote repository? Try it out!
- _Q.11._ What is the difference between `git pull origin main` and `git pull`?

Merge the `feature/blankets` branch into the main branch.

```bash
git merge feature/blankets
```

- _Q.12._ How could you prevent a merge commit from being created when merging branches? Why would you want to do that?
- _Q.13._ What would have been the result if you had merged the `main` branch into the `feature/blankets` branch instead?

## 4. Resolve the merge conflict

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


## 5. Push the changes to the remote repository

Push the changes to the remote repository.

```bash
git push origin main
```

Now the `feature/blankets` branch is merged into the main branch, and the conflict are resolved. The packing list is updated with the items from both branches.

- _Q.14._ Which strategy would you have had to use to merge the feature branch into the main branch without creating a merge conflict?
-  _Q.15_. Is avoiding a merge conflicts generally a good strategy?

## Part 2: Feature Branch Development Cycle and Conflict Resolution Online

Now that you've set up the repository and added items locally, it's time to step through a feature branch development cycle using the project management tools provided by the remote services. 
This part will focus on working entirely online in the remote IDE.

### 1. Creating a Project Board and Tasks

Carol, the tech enthusiast, wants to add a drone to the packing list. 
She will start by creating a project board and adding tasks/issues for the items she wants to bring.

- Go to the repository on the remote server: [Weekend Out](https://github.com/t4d-gmbh/Weekend-Out/)
    - [Create your own Weekend-Out Repository](https://github.com/new?template_name=Weekend-Out&template_owner=t4d-gmbh) using this repository as a template OR continue on the repository you used to complete Part 1.
      _Note: For the rest of this exercise it is assumed that you also named your repository `Weekend-Out`!_
- Go to "Projects" and create a new project board called "Drone Feature".
- Add tasks/issues to the project board:
  - **Task 1**: Add drone to packing list.
  - **Task 2**: Add extra batteries to packing list.
  - **Task 3**: Add camera to packing list.
  - **Task 4**: Review changes and resolve conflicts.

### 2. Creating a New Feature Branch Online

Carol will create a new feature branch directly on the remote repository.

- Go to your forked repository on the remote server (GitHub or GitLab).
- Create a new branch called `feature/drone` from the main branch.

### 3. Adding Items to the Feature Branch

Carol will add her items to the `packing_list.md` file directly in the browser.

- Navigate to the `packing_list.md` file in the `feature/drone` branch in the remote repository. Open the file for editing in the remote IDE.
- Add the first item that Carol wants to bring (e.g., drone).
- Commit this first added item with a descriptive message. Link the commit to the respective task on the project board. Hint: When you start typing `#`, you will see a list of tasks from the project board to link to the commit.
    - Why is it useful to link commits to tasks on the project board?

### 4. Using Project Management Tools

Carol will use the project management tools to track her progress.

- After completing the first task, move it manually on the project board as she completed it.
For the other tasks, Carol will use automatic project board updates.
- Think about how you can track the progress of a project by automatically updating the project board based on commit messages?
- Add the other items to the `packing_list.md` file and commit them with descriptive messages. Link the commits to the respective tasks on the project board.

### 5. Merging the Feature Branch into the Main Branch with a Pull Request

Once Carol has added all the items to the `packing_list.md` file, she will merge her `feature/drone` branch into the `main` branch.

- Create a pull request from `feature/drone` to `main`. Link the pull request to the tasks on the project board with [closing keywords](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue).

### 6. Identifying and Resolving Conflicts

While Carol was working on her feature branch, Alice made changes to the main branch that conflict with Carol's changes.

- Resolve the conflicts in the `packing_list.md` file directly in the browser.
- Commit the changes with a descriptive message. Remember to link the commit to the respective task on the project board.

### 7. Completing the Pull Request

After resolving the conflicts, Carol will request a review of her changes to the packing list from another team member.

- Request a review from another team member on the pull request.
- Start the review process by adding comments to specific lines in the `packing_list.md` file.
    - Propose changes to some lines in the `packing_list.md` file.
    - Accept the changes and approve the pull request.
- Merge the pull request and delete the `feature/drone` branch.
- Check the project board to see the status of the tasks. They should all be marked as "Done".

### 7. Reflecting on the Process

- Discuss the benefits of using feature branches and project management tools.
- Reflect on the experience of resolving conflicts online.
- Consider how these practices can improve collaboration and project management in a research setting.
