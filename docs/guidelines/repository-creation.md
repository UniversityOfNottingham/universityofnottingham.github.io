## 1. Create the Repository

In the Azure DevOps menu, navigate to the **Repos** page. From the drop-down where you can select an existing repository, select **New Repository** (or from the + menu next to **ProductCentre.Main**, select **New repository**).

Name the repo appropriately
!!! note "TODO - Standards for Naming Repos"

Check the box to add a README, and add a .gitignore (e.g. for Visual Studio projects, select Visual Studio from the dropdown).

Click **Create**.


## 2. Set Branch Policies for `master`

With your new repo still selected, navigate to the **Branches** sub-menu.

On the row for the `master` branch, from the **More Actions** context menu (next to the Commit number), select **Branch Policies**. Tick the following options:

* **Require a minimum number of reviewers** (set the minimum number to 2)
* **Reset code reviewer votes when there are new changes**
* **Check for linked work items** (select **Optional**)
* **Check for comment resolution** (select **Required**)

Under **Automatically include code reviewers**, click the button to **Add automatic reviewers**. Under **Reviewer(s)**, search for `Application Development` and choose the search result with the `[UniversityofNottingham]` prefix. Select a **Policy requirement** of **Required** for this reviewer, and click **Save**.


## 3. Create a Pipeline

In the Azure DevOps menu, navigate to the **Pipelines** page, and at the top right click the **New pipeline** button.

Click on **Azure Repos Git**, then filter and select your repository. Select **Starter pipeline**.

Replace the pipeline YAML with the following:

```yaml
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml

trigger:
- master

pool:
  name: Default

steps:
- script: '|'
```

Click the button at top right to **Save and run** the pipeline. Keep the default commit message. Select the option to **Create a new branch for this commit and start a pull request**, and keep the default name, then click the button to **Save and run**.

The build will fail, because of the change we made to the pipeline YAML file. This is by design: at this point, we want a failing pipeline build in order to ensure that later, when a project is created, a suitable, passing, code-reviewed pipeline build step, appropriate for the project type (rather than the default, generic, always-passing pipeline build steps) must be added to the pipeline YAML in order to merge the project into master.

The pull request now needs to be reviewed and approved, to merge the pipeline YAML to master.


## 4. Add a Build Policy for merges to master

In Azure DevOps, navigate to the **Repos** menu, make sure your new repo is still selected, and navigate to the **Branches** sub-menu.

On the row for the `master` branch, from the **More Actions** context menu (next to the Commit number), select **Branch Policies**.

Under the **Build validation** section, click the button to **Add build policy**.

Select the Build Pipeline you created in the previous step (the name should be the same as the name of the repo).

Keep the default options:

* **Trigger: Automatic**
* **Policy requirement: Required**
* **Build expiration: After 12 hours if master has been updated**


## 5. Create your solution

Clone the Repo.

Create a branch called `create-solution`.

Create your initial bare-bones solution within that branch.

Make sure to edit the pipeline YAML file to define the appropriate build step(s) and demands.

For example, for a .Net project, this specifies a dotnet build step, and demands that the server chosen from the `Default` pool to perform the build must have `dotnet`:

```yaml
trigger:
- master

pool:
  name: Default
  demands: dotnet

steps:
- script: 'dotnet build'
```

Finally, push all your changes and make a pull request to merge the `create-solution` branch to `master`.
