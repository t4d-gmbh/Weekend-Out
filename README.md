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

### 2. Locally merge the feature branch into the main branch

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/blankets` branch into the `main` branch.

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

### 3. Resolve the merge conflict

Oops! It seems Carol beat you to it and has already added some blankets to the list.

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


### 4. Push the changes to the remote repository

Push the changes to the remote repository.

```bash
git push
```

Now the `feature/blankets` branch is merged into the main branch, and the conflict are resolved. The packing list is updated with the items from both branches.

- _Q.14._ Which strategy would you have had to use to merge the feature branch into the main branch without creating a merge conflict?
-  _Q.15_. Is avoiding a merge conflicts generally a good strategy?

---
---

## Part 2: Feature Branch Development Cycle and Conflict Resolution Online

Now that you've set up the repository and added items locally, it's time to step through a feature branch development cycle using the project management tools provided by the remote services. 
This part will focus on working entirely online in the remote IDE.

### 1. Creating a Project Board and Tasks

Carol, the tech enthusiast, wants to bring a drone and argues that it would be cleaner to create a dedicated package list, since the drone requires a few items to be brought along.

She start by creating an Issue the explain how she would like to reorganize your package list.

- Go to the repository on the remote server: [Weekend Out](https://github.com/t4d-gmbh/Weekend-Out/)
    - [Create your own Weekend-Out Repository](https://github.com/new?template_name=Weekend-Out&template_owner=t4d-gmbh) using this repository as a template OR continue on the repository you used to complete Part 1.

      _Note: For the rest of this exercise it is assumed that you also named your repository `Weekend-Out`!_

- Go to your own `Weekend-Out` repository and open a new issue for Carol.
  Call it `Package list restructuring` (Please keep the name as is!) and add a short descripion about what it is that Carol wants to do.

### 2. Creating a New Feature Branch Online

Carol added the items she wanted in the list as a comment to the Issue.
With this you have all you need to get started:

- Refresh the page of the Issue to find a comment Carol (actually a github bot) left with what it is that she wants to add.

- Create a new branch directly from the Web-View of the Issue.
  (You find it on the right under "Development")

- Keep the suggested branch name as is and checkout the newly created branch on you device.

- Create a new markdown file for Carol's drone list and add the items she wants to bring.

- Push your changes to the remote service once you are done.

### 3. Create a Pull Request

Now that you have implemented the required feature and pushed the branch back to the remote, you can create a pull request to formalise your intention to merge your feature branch into `main`.

- If you head back to your `Weekend-Out` Repository on **GitHub** you should get a notification bar asking you to open a Pull Request.
  In case you do not see such notification, click on "Pull requests" and then on "New pull request".

- Assign yourself to the Pull Request, go ahead an create it.

- You will be redirected to the view of your first pull request. For now ignore the "Checks", but have a look at the "Commits" panel and the "Files changed" panel.

### 4. Merging the Feature Branch into the Main

If you are satisfied with you edits you can think about merging your feature branch into the healthy reference, `main`.

- Remember that it is up to you to assert that the change you introduce are compatible with the healthy reference by the time you introduce the changes and not at some point before!

- If you think everything is fine, go ahead an merge your branch by clicking on the green "Merge pull request" button at the bottom of the page of the Pull Request. Confirm by hitting the "Merge" button.

### 5. Inspect what just happened

You have just finished a Feature Branch cycle, 🥳🎈Congrats!

- Go to the `Issues` tab of your `Weeken-Out` repository and check on the issue you had created earlier.
  If everything happened according to plan your issue should be in the state closed no.

- Now head over to "Code" and checkout the repository.
  You should find the newly created file holding the list for Carols done, so far so good!

  But wait! There is another file called `Carols_drone_list.md` with a commit message next to it: `"Adding Carols done list"`.
  Click on the text and you will be directed to the detail view of a commit in which Alice has added that new file.

It seems not everyone was informed that you were in charge of implementing this list and Alice went ahead and did the same.

Now, we do not want to blame anyone, but it would be nice to find out how it could happen that the healthy reference now contains two files for the same list.

- Go to the "Insights" panel in your `Weekend-Out` Repository and select `Network` (note that the repository needs to be `public` to access this feature).
  You will see a graph of what happened and will find that Alice has pushed changes to the `main` branch while you were working no your feature branch.

  This is a bit embarrassing but it would have been up to you to make sure that your feature branch is compatible with `main` by the time you merged it.

  _Note:_ In case you do not want to make your `Weekend-Out` public you can view the "Network" in your command line:

  ```bash
  git checkout main
  git pull
  git log --all --decorate --oneline --graph
  ```
