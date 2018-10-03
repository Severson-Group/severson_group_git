# demonstration_repo
This repository serves as a reference to using Git in the Severson Research Group and provides a tutorial on the typical Git workflow used in the Severson Group. 

Links to background reading material on Git is provided and participants are guided through best-practice-based example of making commits and resolving merge conflicts. This project is also intended to be an example of how to follow these guidelines.


# Git Usage Reference Material and Guidelines

## Basics of Git:
Review the [Pro Git book](https://git-scm.com/book/en/v2/). Chapters 1-3 and 6.1 - 6.3 are especially important.
Specifically, please familiarize yourself with the following basic Git concepts:

1. Basic command line operations. At a bare minimum, familiarize yourself with each of these commands: `git clone`, `git add`, `git commit`, `git pull`, `git push`, `git branch`, `git checkout`, and `git merge` (these are all covered in the first 3 chapters of the Pro Git book).

2. Familiarize yourself with the concepts of commits, the staging area, branches, and merging.

3. In most repositories, we will use a hybrid of [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) and [GitHub Flow](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow).

4. Typically repositories will be hosted in GitHub within the Severson Group (https://github.com/severson-group). This means that in a typical workflow a repository will have one remote, which will be the GitHub server.

## Proper Commit Messages
Review *Commit Guidelines* in [Section 5.2 of the Pro Git book](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) and this helpful [Gist](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53).

Key aspects of a commit message:

 * The maximum line length should be 72 characters. 
 * Insert a blank line between paragraphs and bulleted lists.
 * Use the imperative present tense in your subject line.  A helpful example can be found in the [Git patch guidelines](https://git.kernel.org/pub/scm/git/git.git/tree/Documentation/SubmittingPatches): 
>Describe your changes in imperative mood, e.g. "make xyzzy do frotz" instead of "[This patch] makes xyzzy do frotz" or "[I] changed xyzzy to do frotz", as if you are giving orders to the codebase to change its behavior.

# Setup and Tools for Git:
_Note:_ Check whether these tools are installed first! Several of these programs are already installed and configured on the Severson Group computers.

## Git Installation
At a minimum, you'll need to install Git on your PC: https://git-scm.com/

After installing Git, configure your user name and email:
```
git config --global user.name “First Last”
git config --global user.email myemail@wisc.edu
```

### Text Editor
You may optionally want to install an advanced text editor. This may be useful for commit messages and general text editting that comes up with Matlab and C development. 

I recommend Notepad++ https://notepad-plus-plus.org/.

If you install this prior to Git, the Git installation tool will give you an option to use Notepad++ as your default editor. If you would like to make Notepad++ your default editor after you have installed Git, you can run this command from Git Bash: `git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"`

## Graphical Git Interface
Git comes with GitGUI, which many people are happy with. I personally use and recommend [Atlassian SourceTree](https://www.sourcetreeapp.com/)

This is an alternative to Git GUI. To ensure you comply with the commit message maximum line length, you way wish to configure SourceTree as follows:
1. In SourceTree go to Tools -> Options
2. Click the General Tab and scroll down to Commit Settings.
3. Check the following options: 
  * `Use fixed-width font for commit messages`
  * `Spell check commit messages in English (US)`
  * `Display a column guide in commit message at 72 characters`
When complete, your settings should look like this:

![SourceTree Settings](images/SourceTreeConfig.png?raw=true "AMDC Block Diagram")

## External Diff and Merge Tools

External tools for Diff and Merge operations are useful when working in repositories with several collaborators. These tools can be linked into Git so that you can invoke them from the command line or from a graphical GUI interface such as SourceTree. 

Here are recommended tools that support both Diffs and three way merges (use just one of these) for Windows:
 * [Kdiff3](http://kdiff3.sourceforge.net/) - _free tool_
 * [P4merge](http://www.perforce.com/product/components/perforce-visual-merge-and-diff-tools) - _free tool_
 * [Diffmerge](https://sourcegear.com/diffmerge/) - _free tool_
 * [Exam Diff Pro](https://www.prestosoft.com/edp_examdiffpro.asp) _paid tool_

These tools can be linked to Git by editing the `diff`, `merge`, `difftool`, and `mergetool` settings as follows:

### Kdiff3

```
git config --global merge.tool kdiff3
git config --global mergetool.kdiff3.cmd "\"C:/Program Files/Kdiff3/kdiff3\" --L1 \"\$MERGED (Base)\" --L2 \"\$MERGED (Local)\" --L3 \"\$MERGED (Remote)\" -o \"\$MERGED\" \"\$BASE\" \"\$LOCAL\" \"\$REMOTE\""
git config --global diff.guitool kdiff3
git config --global difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
```

Note that the path may need to be updated based on the install location of Kdiff3.

# Severson Group Git Usage
This section provide guidance for using Git on Severson Group projects. These are typical or recommended guidelines. Individual projects may have specific needs and deviate from these guidelines. _That is perfectly fine_, but should be documented within that project.

## Typical Repository Workflow

### Branches
In a typical repository, we will have two long running branches: 
 * `master`: Always points to the current stable release commit. If someone clones our repository, they should be able to check out the `master` branch and everything should "work" (whatever that means for the purposes of the repository). In public repositories, the current commit that the `master` branch points to is the latest _release_ of the project and should be accompanied with relevant documentation. Only the project maintainer(s) is/are allowed to commit to this branch. Commits will typical only be done by pull requests that merge the `develop` branch into the `master` branch.
 * `develop`: Always points to a stable commit. If someone clones our project, they should be able to check out the `develop` branch and everything should "work" (whatever that means for the purposes of the repository). View this branch as a _beta_ release. This is where the current development of a project is sitting at. While everything "works", features may be incomplete or not fully documented. Only the project maintainer(s) is/are allowed to commit to this branch. Commits will typical only be done by pull requests that merge topic branches into the `develop` branch.

The main code development will be done in "topic" branches. These branches can be created by any developer and are based off of either another topic branch or the develop branch. Developers create a topic branch when they want to add a new feature or fix a bug. The topic branch name should be informative based on the feature/bug they are addressing. When the topic branch is complete, it should be merged into the develop branch (or its parent topic branch) using a pull request.

### Typical Workflow
A developer checks out the `develop` branch (or another developers topic branch) and decides to add a new feature or fix a bug. The developer creates a new topic branch based off of `develop` and starts committing to this topic branch. The topic branch name should be informative based on the feature/bug they are addressing. The developer may keep the branch local (only on their PC) for a while but will ultimately need to push it to the online repository. Developers are encouraged to push it up to the server frequently as a means of a backup to avoid data loss and to allow other developers to follow the topic branch progress. If the developer needs to incorporate recent changes from another branch, they may periodically merge that branch into their topic branch (or use a more advanced Git feature like "Cherry pick". 

When ready, the developer creates a pull request for the topic branch to be merged back into the parent branch (`develop` or another topic branch). The project maintainer(s) and other developers notice this pull request and review and comment on it within GitHub. When ready, the project maintainer(s) complete the pull request, merging the topic branch into the parent branch and delete the topic branch. 

This workflow can be illustrated as the first figure of this [blog post](https://nvie.com/posts/a-successful-git-branching-model/), but without the `hotfixes` and `release` branches. This is a hybrid of the [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) and [GitHub Flow](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow).

One variant of this to be aware of is the case of public repositories. In public repositories, external developers can contribute by forking the repository to their private account and then initiating a pull request between their forked version and our hosted version.

### General Guidelines

* Users must be careful to avoid operations that rebase, squash, or amend any commits that have been pushed to the server. 
* See commit message guidelines that were previously described.
* Use simple but informative names for topic branches.
* Use tags to denote major releases.
* Place a `README.md` file in each repository (either at the root level or in docs/) that contains repository specific information. `.md` stands for Markdown. You can find guidelines on how to write in Markdown here: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet/.
* Check to see if a pull request can be cleanly merged. If not, please attempt to resolve the merge conflicts. _Hint:_ you may find the advice [here](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow) helpful.

## Git Tips and Tricks

* `git remote update origin --prune` - Useful if a branch has been removed from a remote server, but still appears in your repository as being on that server (for example, after a pull request has been merged).

* you will need to manually remove topic branches from your working copy that are no longer needed (i.e., a pull request has been completed).

* `git checkout -b cool_feature` will create `cool_feature` branch based on the current commit and switch to it at the same time.
 
