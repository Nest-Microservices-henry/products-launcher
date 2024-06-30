#Dev

1. clone the repository
2. create .env base in the .env.template
3. run the command `docker compose up --build`


Steps to Create Git Submodules


1. Create a new repository on GitHub
2. Clone the repository to the local machine
3. Add the submodule, where repository_url is the url of the repository and directory_name is the name of the folder where you want the sub-module to be saved (it must not exist in the project)
git submodule add <repository_url> <directory_name>

4. Add the changes to the repository (git add, git commit, git push)
Ex:
git add .
git commit -m "Add submodule"
git push

5. Initialize and update Sub-modules, when someone clones the repository for the first time, they must execute the following command to initialize and update the sub-modules
git submodule update --init --recursive

6. To update sub-modules references
git submodule update --remote



## Important
If you are working on the repository that has the sub-modules, **first update and push** to the sub-module and **then** to the main repository.

If it is done the other way around, the references of the sub-modules in the main repository will be lost and we will have to resolve conflicts.

