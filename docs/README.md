# 0. severson_group_git
This repository serves as a reference to using Git in the Severson Research Group and provides a tutorial on the typical Git workflow used in the Severson Group. 

Links to background reading material on Git is provided and participants are guided through best-practice-based example of making commits and resolving merge conflicts. This project is also intended to be an example of how to follow these guidelines.

## 0.1 Table of Contents
1. [Git Reference Material](#ref_material)
	1. [Basics of Git](#sub_basics)
	1. [Proper Commit Messages](#sub_commit_msg)
2. [Git Installation and Configuration](#setup-tools)
	1. [Git Installation](#sub_install)
	1. [Graphical Git Interface](#sub_git_gui)
	1. [Text Editor](#sub_text_editor)
	1. [External Diff and Merge Tools](#sub_ext_diff_merge)
		1. [Kdiff3](#sub_sub_kdiff3)
3. [Severson Group Git Workflow and Guidelines](#group-git)
	1. [Typical Repository Workflow](#sub_repo_workflow)
		1. [Branches](#sub_sub_branches)
		1. [Typical Workflow](#sub_sub_workflow)
	1. [GitHub Settings](#sub_github)
	1. [General Guidelines](#sub_guidelines)
	1. [Git Tips and Tricks](#sub_git_tips)
4. [Tutorial](#tutorial)
	1. [Tutorial Steps](#sub_tutorial_steps)

<a name="ref_material"></a>
# 1. Git Reference Material

<a name="sub_basics"></a>
## 1.i Basics of Git:
Review the [Pro Git book](https://git-scm.com/book/en/v2/). Chapters 1-3 and 6.1 - 6.3 are especially important.
Specifically, please familiarize yourself with the following basic Git concepts:

1. Basic command line operations. At a bare minimum, familiarize yourself with each of these commands: `git clone`, `git add`, `git commit`, `git pull`, `git push`, `git branch`, `git checkout`, and `git merge` (these are all covered in the first 3 chapters of the Pro Git book).

2. Familiarize yourself with the concepts of commits, the staging area, branches, and merging.

3. In most repositories, we will use a hybrid of [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) and [GitHub Flow](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow).

4. Typically repositories will be hosted in GitHub within the Severson Group (https://github.com/severson-group). This means that in a typical workflow a repository will have one remote, which will be the GitHub server.

<a name="sub_commit_msg"></a>
## 1.ii Proper Commit Messages
Review *Commit Guidelines* in [Section 5.2 of the Pro Git book](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) and this helpful [Gist](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53).

Key aspects of a commit message:

 * The maximum line length should be 72 characters. 
 * Insert a blank line between paragraphs and bulleted lists.
 * Use the imperative present tense in your subject line.  A helpful example can be found in the [Git patch guidelines](https://git.kernel.org/pub/scm/git/git.git/tree/Documentation/SubmittingPatches): 
>Describe your changes in imperative mood, e.g. "make xyzzy do frotz" instead of "[This patch] makes xyzzy do frotz" or "[I] changed xyzzy to do frotz", as if you are giving orders to the codebase to change its behavior.

<a name="setup-tools"></a>
# 2. Git Installation and Configuration:
_Note:_ Check whether these tools are installed first! Several of these programs are already installed and configured on the Severson Group computers.

<a name="sub_install"></a>
## 2.i Git Installation
At a minimum, you'll need to install Git on your PC: https://git-scm.com/

After installing Git, configure your user name and email:
```
git config --global user.name “First Last”
git config --global user.email myemail@wisc.edu
```

<a name="sub_git_gui"></a>
## 2.ii Graphical Git Interface
Git comes with GitGUI, which many people are happy with. I personally use and recommend [Atlassian SourceTree](https://www.sourcetreeapp.com/)

This is an alternative to Git GUI. To ensure you comply with the commit message maximum line length, you way wish to configure SourceTree as follows:
1. In SourceTree go to Tools -> Options
2. Click the General Tab and scroll down to Commit Settings.
3. Check the following options: 
  * `Use fixed-width font for commit messages`
  * `Spell check commit messages in English (US)`
  * `Display a column guide in commit message at 72 characters`
When complete, your settings should look like this:

![SourceTree Commit Settings](images/SourceTreeConfig.png?raw=true "SourceTree Commit Settings")

<a name="sub_text_editor"></a>
## 2.iii Text Editor
You may optionally want to install an advanced text editor. This may be useful for commit messages and general text editting that comes up with Matlab and C development. 

I recommend Notepad++ https://notepad-plus-plus.org/.

If you install this prior to Git, the Git installation tool will give you an option to use Notepad++ as your default editor. If you would like to make Notepad++ your default editor after you have installed Git, you can run this command from Git Bash: `git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"`


<a name="sub_ext_diff_merge"></a>
## 2.iv External Diff and Merge Tools

External tools for Diff and Merge operations are useful when working in repositories with several collaborators. These tools can be linked into Git so that you can invoke them from the command line or from a graphical GUI interface such as SourceTree. 

Here are recommended tools that support both Diffs and three way merges (use just one of these) for Windows:
 * [Kdiff3](http://kdiff3.sourceforge.net/) - _free tool_
 * [P4merge](http://www.perforce.com/product/components/perforce-visual-merge-and-diff-tools) - _free tool_
 * [Diffmerge](https://sourcegear.com/diffmerge/) - _free tool_
 * [Exam Diff Pro](https://www.prestosoft.com/edp_examdiffpro.asp) _paid tool_

These tools can be linked to Git by editing the `diff`, `merge`, `difftool`, and `mergetool` settings as follows:

<a name="sub_sub_kdiff3"></a>
### 2.iv.a Kdiff3

```
git config --global merge.tool kdiff3
git config --global mergetool.kdiff3.cmd "\"C:/Program Files/Kdiff3/kdiff3\" --L1 \"\$MERGED (Base)\" --L2 \"\$MERGED (Local)\" --L3 \"\$MERGED (Remote)\" -o \"\$MERGED\" \"\$BASE\" \"\$LOCAL\" \"\$REMOTE\""
git config --global diff.guitool kdiff3
git config --global difftool.kdiff3.cmd "\"C:/Program Files/Kdiff3/kdiff3\" \$LOCAL \$REMOTE"
```

Note that the path may need to be updated based on the install location of Kdiff3.

<a name="group-git"></a>
# 3. Severson Group Git Workflow and Guidelines
This section provide guidance for using Git on Severson Group projects. These are typical or recommended guidelines. Individual projects may have specific needs and deviate from these guidelines. _That is perfectly fine_, but should be documented within that project.

<a name="sub_repo_workflow"></a>
## 3.i Typical Repository Workflow

<a name="sub_sub_branches"></a>
### 3.i.a Branches
In a typical repository, we will have two long running branches: 
 * `master`: Always points to the current stable release commit. If someone clones our repository, they should be able to check out the `master` branch and everything should "work" (whatever that means for the purposes of the repository). In public repositories, the current commit that the `master` branch points to is the latest _release_ of the project and should be accompanied with relevant documentation. Only the project maintainer(s) is/are allowed to commit to this branch. Commits will typical only be done by pull requests that merge the `develop` branch into the `master` branch.
 * `develop`: Always points to a stable commit. If someone clones our project, they should be able to check out the `develop` branch and everything should "work" (whatever that means for the purposes of the repository). View this branch as a _beta_ release. This is where the current development of a project is sitting at. While everything "works", features may be incomplete or not fully documented. Only the project maintainer(s) is/are allowed to commit to this branch. Commits will typical only be done by pull requests that merge topic branches into the `develop` branch.

The main code development will be done in "topic" branches. These branches can be created by any developer and are based off of either another topic branch or the develop branch. Developers create a topic branch when they want to add a new feature or fix a bug. The topic branch name should be informative based on the feature/bug they are addressing. When the topic branch is complete, it should be merged into the develop branch (or its parent topic branch) using a pull request.

<a name="sub_sub_workflow"></a>
### 3.i.b Typical Workflow
A developer checks out the `develop` branch (or another developers topic branch) and decides to add a new feature or fix a bug. The developer creates a new topic branch based off of `develop` and starts committing to this topic branch. The topic branch name should be informative based on the feature/bug they are addressing. The developer may keep the branch local (only on their PC) for a while but will ultimately need to push it to the online repository. Developers are encouraged to push it up to the server frequently as a means of a backup to avoid data loss and to allow other developers to follow the topic branch progress. If the developer needs to incorporate recent changes from another branch, they may periodically merge that branch into their topic branch (or use a more advanced Git feature like "Cherry pick". 

When ready, the developer creates a pull request for the topic branch to be merged back into the parent branch (`develop` or another topic branch). The project maintainer(s) and other developers notice this pull request and review and comment on it within GitHub. When ready, the project maintainer(s) complete the pull request, merging the topic branch into the parent branch and delete the topic branch. 

This workflow can be illustrated as the first figure of this [blog post](https://nvie.com/posts/a-successful-git-branching-model/), but without the `hotfixes` and `release` branches. This is a hybrid of the [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) and [GitHub Flow](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow).

One variant of this to be aware of is the case of public repositories. In public repositories, external developers can contribute by forking the repository to their private account and then initiating a pull request between their forked version and our hosted version.

<a name="sub_github"></a>
## 3.ii GitHub Settings
To enforce branch protections (i.e. only allow a maintainer to commit to `develop` or `master`), follow the steps in [this article](https://help.github.com/articles/enabling-branch-restrictions/). This repository has example protections in place.

<a name="sub_guidelines"></a>
## 3.iii General Guidelines

* Users must be careful to avoid operations that rebase, squash, or amend any commits that have been pushed to the server. 
* See commit message guidelines that were [previously described](#sub_commit_msg).
* Use simple but informative names for topic branches.
* Use tags to denote major releases.
* Place a `README.md` file in each repository (either at the root level or in docs/) that contains repository specific information. `.md` stands for Markdown. You can find guidelines on how to write in Markdown [here]( https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet/).
* Check to see if a pull request can be cleanly merged. If not, please attempt to resolve the merge conflicts. _Hint:_ you may find the advice [here](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow) helpful.

<a name="sub_git_tips"></a>
## 3.iv Git Tips and Tricks

* `git remote update origin --prune` - Useful if a branch has been removed from a remote server, but still appears in your repository as being on that server (for example, after a pull request has been merged).

* you will need to manually remove topic branches from your working copy that are no longer needed (i.e., a pull request has been completed).

* `git checkout -b cool_feature` will create `cool_feature` branch based on the current commit and switch to it at the same time.
 
* `git commit --amend` will let re-write the commit message of your last commit. _CAUTION:_ Only do this to commits that have not been pushed up to the server (and have no branches based on them).

<a name="tutorial"></a>
# 4. Tutorial
This tutorial will guide you through creating a topic branch, making a commit, creating and resolving a merge conflict, and completing a pull request. You can use either Git Bash, SourceTree, GitGUI, or some other graphical Git tool to complete this tutorial. I will give some of the instructions as Git Bash commands, but there should be equivalent buttons to do these operations in your graphical Git tool. I recommend that you switch back and forth between the command line and your graphical Git tool to complete these steps.

This tutorial assumes that you have set up external Diff and Merge tools (see above).

<a name="sub_tutorial_steps"></a>
## 4.i Tutorial Steps:

1. `git clone` the repository to your computer (I recommend maintaining a `ProjectSpace` folder where all of your working copies of your repository reside)
2. Checkout the `develop` branch.
3. Create a new topic branch named `[your-first-name_tutorial]` based on the `develop` branch. The later part of this instruction will happen automatically, since you currently have `develop` checked out when you created your topic branch.
4. Now create a new topic branch named `make_merge_conf` based on your first topic branch. At this point, `develop`, `[your-first-name_tutorial]`, and `merge_conf` should all point to the same commit. You can verify this by typing `git log` and noting the text in the commit header line for the current commit has these branches labeled: `commit ff7524da1e02407f8e3798cd4e90613c391c7ec6 (HEAD -> make_merge_conf, origin/develop, eric_tutorial, develop)`. 
5. Navigate to `/source/lipsum_insanity.txt` and insert "I was here" as its own line at the start of the file. Somewhere in the third paragraph type "There are some english words here." 
6. Save the file and close it.
7. Refresh the status of your repository with `git status` and notice that Git indicates that changes have been made to `lipsum_insanity.txt`.
8. Investigate the changes to the file using a) `git diff source/lipsum_insanity.txt` and b) `git difftool source/lipsum_insanity.txt` (you could also simply run `git diff` and `git difftool` without specifying the file names).
9. Use Git's stage hunk feature to commit only the change to the first line of lipsum_insanity.txt. Use a commit message that follows our group guidelines. Help on using the command line to stage hunks can be found [here](https://git-scm.com/book/en/v2/Git-Tools-Interactive-Staging) under _Staging Patches_ -- not that you'll have to tell Git to split the file up into smaller hunks. A graphical Git tool (like SourceTree) makes this process much easier.
10. Notice that there are remaining changes in `lipsum_insanity.txt` because you have not yet committed line 3. Commit the entire file now (again, use a commit message that follows our group guidelines)
11. Checkout your original topic branch `[your-first-name_tutorial]`
12. Open `lipsum_insanity.txt` and notice that your changes are gone. 
13. Make the same changes as in step 5 but instead use these phases: "The correct answer is 5" and "More text to test".
14. Commit your changes to `lipsum_insanity.txt`
15. Merge `make_merge_conf` into your current branch. This will create a merge conflict.
16. Investigate the merge conflict by opening up the file in conflict `lipsum_insanity.txt` in a text editor. Note the `>>>>>>>` and `<<<<<<<` characters that Git uses to indicate a conflict. 
17. You have several options to resolve the conflict - [see here](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging). In this tutorial, I want you to practice using the MergeTool approach. To start it, you can execute the command `git mergetool` or, in SourceTree, you can right click on each file that has a merge conflict , `Resolve Conflicts` -> `Launch External Merge Tool`
18. This should now open up your external merge tool (i.e. Kdiff3). If it does not, that means you have an installation problem. Fix this before proceeding. 
19. Use your external merge tool to make the final `lipsum_insanity.txt` file have the text you added in step 13 (disregard your changes from `make_merge_conf`). Save  `lipsum_insanity.txt` and exit the merge tool. Your merge conflict is resolved when you have committed your changes into Git. At any point before you commit, you can restart your merge by issuing `git reset --hard HEAD`. _Caution:_ This will throw away uncommitted changes on your working copy! If you issue this command, you will be restored to step 15.
20. Commit your resolved merge conflict into Git to finish your merge. For merges, it is fine to use the default merge commit message the Git generates for you.
21. Restore `lipsum_insanity.txt` to the file that is located in the develop branch by using this command: `git checkout develop -- source/lipsum_insanity.txt`.
22. Your working copy should now be in the same state it was before you started the tutorial. Commit your working copy.
23. Add your full name to the end of `users.txt` and commit your changes.
24. Take a look at your commit graph and trace back the individual commits that have led you to this point. Do this via the command line with `git log --graph --oneline --all` and via your graphical Git tool. Match the commits the in command line and graphical Git tool. Commits can be identified by the first several digits of the commit ID. 
![Git Command Line Log](images/git_log_tutorial.PNG?raw=true "Git Command Line Log")
![SourceTree Log](images/sourcetree_log_tutorial.PNG?raw=true "SourceTree Log Screenshot")
25. Use Git's debugging capability to review who has most recently changed each line of `lipsum_insanity.txt` and `users.txt`. Instructions for doing this from the command line can be found [here](https://git-scm.com/book/en/v2/Git-Tools-Debugging-with-Git). You can also do this with SourceTree by right clicking on a file and choosing `Annotate Selected...`. To do this from the command line run `git blame source/users.txt` and `git blame source/lipsum_insanity.txt`. Each line of the file will be shown, prepended with the commit ID, user name, and date of the last commit that modified that line. Note the changes that you and others have made to each file. For example, in `lipsum_insanity.txt`, you should see my name next to the non-modified lines and your name next to the lines that you have modified (and restored) as part of the tutorial.
![Git Blame](images/git_blame_tutorial.PNG?raw=true "Git Command Line Blame Screenshot")
![SourceTree Blame](images/sourcetree_blame_tutorial.PNG?raw=true "SourceTree Blame Screenshot")
26. Push your `[your-first-name_tutorial]` branch to GitHub.
27. Log into GitHub and create a pull request to merge your topic branch into `develop`. 
28. I will inspect your pull request to see that you have completed the steps properly. If there is a problem, we'll chat via the comments and may have a meeting.
29. After I approve your pull request, I will delete your topic branch from the server. You should then do a `git remote update origin --prune` so that your local repository realizes the branch has been removed from `origin`. Finally, delete the two local topic branches you have created.
