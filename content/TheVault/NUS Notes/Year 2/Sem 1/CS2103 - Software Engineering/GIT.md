---
title: GIT
Date Created: 2024-08-24
Last Updated: 2025-09-28
tags:
  - CS2103
  - Git
---
# GIT
---
GIT hub is a <span style='color:var(--mk-color-turquoise)'>revision control software</span> (**RCS**) which helps in revision control during development by <span style='color:var(--mk-color-yellow)'>managing multiple versions of the project</span>.

> [!info] Why Use RCS
> - Automatically track project history
> - Ease of collaboration with others (Conflict control)
> - Have a backup incase just in case
> - Enable work simultaneously on different functions and versions
## Saving Changes

In GIT, there are 2 steps to do before saving your progress. The first is to <span style='color:var(--mk-color-purple)'>stage</span> the changes and the second is to <span style='color:var(--mk-color-purple)'>commit</span>.

<span style='color:var(--mk-color-purple)'>Staging</span>, is the process of **choosing and adding the changes** before committing to the <span style='color:var(--mk-color-turquoise)'>main repository</span> (*Product versions are stored*).

<span style='color:var(--mk-color-purple)'>Committing</span>  on the other hand is to **save everything that has been staged** in the revision control history.

Each commit is its own history in the working directory and it is **uniquely identified by an auto-generated hash value**.
### Omitting Files or Changes

When creating a repository, there is a `.gitignore` file which tells GIT, to **ignore them** when tracking revision history. It also <span style='color:var(--mk-color-yellow)'>supports file patterns</span> (`temp/*.tmp` *ignores all .tmp files*).

> [!question] What to Omit from Version Control
> Not all files are needed for version control, for instance:
> - Binary files (`*.class`, `*.jar`, `*.exe`) as it can be regenerated and a **RCS is optimised for text files**
> - Tempoary Files (*logs files*)
> - Local files
> - Sensitive Content (*files that contain sensitive content which should not get leaked*)
### Naming Commits

GIT, uses <span style='color:var(--mk-color-purple)'>tagging</span> which is **useful in naming different versions** of the product. <b><mark style='background:var(--mk-color-yellow)'>Tags are different from commit messages</mark></b> as messages provide descriptions of the commit.

There are <span style='color:var(--mk-color-orange)'>2 types of tags</span>:
1) **Lightweight Tags**
>Only contains the tag checksum (*Author, date, commit ID*)
2) **Annotated Tags**
>Contains the tag data as well as the annotation along with the tag
### Retrieving a Specific Version

The command `checkout` can be used to <span style='color:var(--mk-color-yellow)'>get a specific version of history</span> in the working directory. However any <span style='color:var(--mk-color-red)'>uncommitted changes will be lost in the process</span>.
#### Shelving Changes Temporarily

A solution to the issue above is through the `stash` which <span style='color:var(--mk-color-yellow)'>saves changes in the working copy</span> into a temporary storage and can be retrieved later on.

Thus after <span style='color:var(--mk-color-purple)'>shelving</span>, a previous version can be retrieved without losing progress.
## Remote Repositories

They are basically repositories <span style='color:var(--mk-color-orange)'>hosted on remote computers</span>, which can be set up on a server.

To create a remote repository, the `colne` command is used. The term <span style='color:var(--mk-color-turquoise)'>upstream repo</span> refers to the <span style='color:var(--mk-color-yellow)'>original repository that was cloned from</span>. And these repos can **work with one another** as long as they <span style='color:var(--mk-color-yellow)'>have a shared history</span>.

There is also `pull` or `fetch` which **syncs any changes** from the upstream repo to another repository.

`push` allows one to **copy the new commits** onto the destination repo.

Using `fork` allows a user to **create a local copy of a repository**, even if the person has no write permissions, since the <span style='color:var(--mk-color-yellow)'>fork owner is different</span>.

Lastly a <span style='color:var(--mk-color-purple)'>pull request</span> is essentially <span style='color:var(--mk-color-yellow)'>merging 2 repositories together</span>. The owner of the original repository will **validate and fix merge conflicts** before pushing the changes into the main repository.
## Branching

In GIT, **branching** allows <span style='color:var(--mk-color-yellow)'>multiple versions of a product be worked on in parallel</span>. Each version is known as a <span style='color:var(--mk-color-turquoise)'>branch</span> and it can be merged into each other.

However when merging branches, there can be <span style='color:var(--mk-color-red)'>merge conflicts</span> within the code which has to be **resolved manually**. This can be done using the `merge` command.
## Pull Requests

The purpose of a pull request is to <span style='color:var(--mk-color-yellow)'>propose changes to a repository</span> which is not owned by the person.

**How does a pull request work**
1) Fork a repo
2) Clone & make changes 
3) Commit and push the changes
4) Now create a pull request to the appropriate repository

As the owner before accepting the <span style='color:var(--mk-color-purple)'>pull request</span>, **review the changes** and give comments as necessary. **Update the code based on the changes** and repeat the process. Only once everything is ok then the pull request can be accepted.

Any updates pushed to the fork will be <span style='color:var(--mk-color-yellow)'>auto updated</span> in the pull request.

To <span style='color:var(--mk-color-orange)'>review a pull request</span>, on the code base there will be a `+` symbol. Click to review that line of code. It will show a standard input box, but if you **want to recommend code** do the following:
```
'''suggestion
	//Code
'''
```

Once done, click on **"start a review"** and after revieing everything, **submit the review**.

Once everything is done, it <span style='color:var(--mk-color-orange)'>can be merged</span> by clicking on the **"merge pull request"**, if it cannot be clicked then:
- **The PR code is out-of-date** as it is possible for the `master` branch to be updated.
- **Merge conflicts**, resolve them before merging

Afterwards <span style='color:var(--mk-color-yellow)'>sync the local repositories</span> as the pull request merge <span style='color:var(--mk-color-yellow)'>just merges with the upstream</span> of the repository. Thus a pull to the new upstream is needed.
# Build Automation
---
<span style='color:var(--mk-color-turquoise)'>Integration</span>, is the process of **combining parts of a product to form a whole product**. This can be <span style='color:var(--mk-color-red)'>very tedious</span> and thus this is where automation comes in.

With <span style='color:var(--mk-color-turquoise)'>build scripts</span>, the build process can be automated. And some build tools also come with **dependency management tools** to mange library versions.
## GitHub Actions

One application of build automation is called <b><mark style='background:var(--mk-color-turquoise)'>continuous integration</mark></b> (*CI*) and <b><mark style='background:var(--mk-color-turquoise)'>continuous deployment</mark></b> (*CD*).

**CI** is the automation of integration, building and testing after every code change.

**CD** on the other hand is the automation to deploy the code to end-users at the same time as **CI**.