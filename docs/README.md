# demonstration_repo
This repository serves as a reference to using Git in the Severson Research Group and provides a tutorial on the typical Git workflow used in the Severson Group. 

Links to background reading material on Git is provided and participants are guided through best-practice-based example of making commits and resolving merge conflicts.


# Git Usage Reference Material and Guidelines

## Basics of Git:
Review the [Pro Git book](https://git-scm.com/book/en/v2/). Chapters 1-3 and 6.1 - 6.3 are especially important.
Specifically, please familiarize yourself with the following basic Git concepts:

1. Basic command line operations. At a bare minimum, familiarize yourself with each of these commands: `git clone`, `git add`, `git commit`, `git pull`, `git push`, `git branch`, `git checkout`, and `git merge` (these are all covered in the first 3 chapters of the Pro Git book).

2. Familiarize yourself with the concepts of commits, the staging area, branches, and merging.

3. In most repositories, we will use a hybrid of [Branching Workflows](https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows) and [GitHub Flow](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project#ch06-github_flow).

4. Typically repositories will be hosted in GitHub within the Severson Group (https://github.com/severson-group). This means that in a typical workflow a repository will have one remote, which will be the GitHub server.

## Proper Commit Messages
Review *Commit Guidelines* in Section 5.2 of the Pro Git book (https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project) and  https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53.

Key aspects of a commit message:

 * The maximum line length should be 72 characters. 
 * Insert a blank line between paragraphs and bulleted lists.
 * Use the imperative present tense in your subject line. 
 
...As the Git patch guidelines (https://git.kernel.org/pub/scm/git/git.git/tree/Documentation/SubmittingPatches) state: 
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

I recommend Notepad++ https://notepad-plus-plus.org/

If you install this prior to Git, the Git installation tool will give you an option to use Notepad++ as your default editor. If you would like to make Notepad++ your default editor after you have installed Git, you can run this command from Git Bash: `git config --global core.editor “’C:/Program Files (x86)/Notepad++/notepad++.exe’ -multiInst -nosession”`

## Graphical Git Interface
Git comes with GitGUI, which many people are happy with. I personally use and recommend Atlassian SourceTree https://www.sourcetreeapp.com/

This is an alternative to Git GUI. To ensure you comply with the commit message maximum line length, you way wish to configure SourceTree as follows:
 1. In SourceTree go to Tools -> Options
 2. Click the General Tab and scroll down to Commit Settings.
 3. Check the following options: 
..*`Use fixed-width font for commit messages`
..*`Spell check commit messages in English (US)`
..*`Display a column guide in commit message at 72 characters`
When complete, your settings should look like this:
![SourceTree Settings](../images/SourceTreeConfig.png)

## External Diff and Merge Tools

External tools for Diff and Merge operations are useful when working in repositories with several collaborators. These tools can be linked into Git so that you can invoke them from the command line or from a graphical GUI interface such as SourceTree. 

Here are recommended tools that support both Diffs and three way merges (use just one of these) for Windows:
 * Kdiff3: http://kdiff3.sourceforge.net/ _free tool_
 * P4merge: http://www.perforce.com/product/components/perforce-visual-merge-and-diff-tools _free tool_
 * Diffmerge: https://sourcegear.com/diffmerge/ _free tool_
 * Exam Diff Pro: https://www.prestosoft.com/edp_examdiffpro.asp _paid tool_

These tools can be linked to Git by editing the `diff`, `merge`, `difftool`, and `mergetool` settings as follows:

### Kdiff3

```git config --global merge.tool kdiff3
git config --global mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"

git config --global diff.guitool kdiff3
git config --global difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"```
 

 
