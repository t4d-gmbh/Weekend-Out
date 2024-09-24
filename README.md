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


Commit your changes and push the branch to the remote repository.

```bash
git add packing_list.md
git commit -m "Add blankets to the packing list"
git push origin feature/blankets
```

## 2. Add Items on the main branch on the remote repository

Make changes in the `packing_list.md` file on the main branch on the remote repository directly in the browser.

Go to the repository on the remote server and open the `packing_list.md` file. Add some items and commit the changes.

## 3. Merge the Feature Branch into the Main Branch Locally

You want to include the additional items from the main branch in your feature branch. To do this, you need to merge the `feature/blankets` branch into the main branch.

On your local machine, switch to the main branch and pull the latest changes from the remote repository.

```bash
git checkout main
git pull origin main
```

Merge the `feature/blankets` branch into the main branch.

```bash
git merge feature/blankets
```

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

