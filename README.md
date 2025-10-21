# The Weekend Out Git Exercise

---

_If you enjoy our interactive Weekend-Out repository, please share it with others!_
_Show your support by giving it a 🌟 using the ⭐-button at the top right of the page._

_By starring the repository, you help increase its visibility, making it easier for others to 🔍 discover and learn 👩‍🎓 how to handle merge conflicts and other scary 👻 Git topics with confidence!_

---

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

Your fiend Bob has asked you to add extra blankets to the list, as he is worried about the chilly nights.

Create a new **`feature/essentials`** branch and add the item Bob wants you to bring.

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
git push origin feature/essentials
```

- _Q.5._ What does the `origin` refer to in the `git push` command? Hint: `git remote -v`.
- _Q.6._ What would be the result of the `git push` command if you didn't specify the branch name? Think of a situation where you need to explicitly state the name of the remote and why this situation might be useful.
- _Q.7._ In which cases would it be useful to have multiple remote repositories?

### 2. Locally merge the feature branch into the main branch

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/essentials` branch into the `main` branch.

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

Merge the `feature/essentials` branch into the main branch.

```bash
git merge feature/essentials
```

- _Q.12._ How could you prevent a merge commit from being created when merging branches? Why would you want to do that?
- _Q.13._ What would have been the result if you had merged the `main` branch into the `feature/essentials` branch instead?

### 3. Resolve the merge conflict

Oops! It seems Carol beat you to it and has already added blankets to the list.

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
-  _Q.15_. Is avoiding a merge conflicts generally a good strategy?

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

- Once you’ve made your changes, commit them to the new branch on your remote repository.

- _Q.1._ How does the process of creating a new branch and committing changes differ between the local and remote environments? Which step is missing in the online process?

### 3. Create a Pull Request

Now that you've implemented the requested feature on the remote repository, you can create a pull request to formally propose merging your feature branch into `main`.

- Refresh your `Weekend-Out` Repository on **GitHub**. You should see a notification bar prompting you to open a Pull Request. If you don't see it, click on "Pull requests" and then "New pull request".

- Assign yourself to the Pull Request, and go ahead and create it.

- You will be redirected to your pull request's details. For now, ignore the "Checks", but take a look at the tabs "Commits" and "Files changed".

### 4. Merging the Feature Branch into Main

If you are satisfied with your edits, you can consider merging your feature branch into the healthy reference `main`.

- Remember, it's your responsibility to ensure the changes you introduce are compatible with the `main` branch at the time of merging - not based on a prior state!

- If everything looks good, merge your branch by clicking on the green "Merge pull request" button at the bottom of the Pull Request page. Confirm by clicking "Merge".

### 5. Inspect What Just Happened

You've just completed a Feature Branch cycle! 🥳🎈Congrats!

- Go to the `Issues` tab of your `Weekend-Out` repository and check the issue you created earlier.
  If everything went according to plan, your Issue should now be marked as closed.

  _Hint:_ If you want to close multiple issues with one pull request, you can use the [closing keywords](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) `closes`, `fixes`, or `resolves` followed by the issue number in the pull request description. E.g. `closes #1` (when you start typing `closes #`, GitHub will suggest the issue number).
  
- Now, head to the "Code" tab and have a look at the content of the repository.
  You should see the new file for Carol's drone list - so far, so good!

  But wait! **There is another file** named `Carols_drone_list.md` with the commit message: `"Adding Carols drone list"`.
  Click on the message, and you will be directed to the detailed view of the commit with which Alice added that file.

It seems not everyone was informed that you were in charge of the drone list and Alice went ahead and took care of it.

Now, without casting blame around, it would be helpful to understand how the healthy reference branch (`main`) ended up with two files for the same list.

- _Q.2._ Who was first to add the list to `main`?
- _Q.3._ What did you do wrong, if anything?
- _Q.4._ What did Alice do wrong, if anything?

- _Discussion:_ How can such a situation be avoided?

_Hints:_

  - The "Insights" tab in your `Weekend-Out` Repository has a `Network` view (Note: Only accessible in `public` Repositories).
    The `Network` view depicts a chronologically ordered graph with all commits.

    _Alternatively:_ If you prefer not to make your `Weekend-Out` repository public, you can view the "Network" in your command line:

    ```bash
    git checkout main
    git pull
    git log --all --decorate --oneline --graph
    ```
