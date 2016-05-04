# Git Workflow

## Setup

1. One team member creates a repo, and adds others as collaborators.
2. Everyone clones the repo (no forking necessary).

## Everyday Feature Workflow

1. Switch to the master branch and get the lastest version
  * `git checkout master`.
  * `git pull origin master`.
2. Checkout a feature branch
  * `git checkout -b my_branch_name`
3. Do your work
  * `git add`
  * `git commit -m "your message"`
4. Periodically, push your branch to master so others can see it
  * First time: `git push -u origin my_branch_name`
  * Subsequent pushes of that branch: `git push`
5. Your partners can checkout that branch to view your progress and give intermediate feedback.
  * `git fetch`
  * `git checkout your_branch_name`

## Reviewing and Merging in Features

1. Push the latest version of your branch:
  * switch to that branch and `git push`
2. Go to the github page for that repository
3. Click create a new pull request
4. Everyone sits down and reviews the PR for bugs, style, readability, etc.
5. If any changes need to be made, they can be made on that branch and then pushed up.
6. Once the branch is approved, someone clicks the `merge` button.

## Getting the Latest Updates

1. Switch to *master* branch
  * `git checkout master`
2. Pull in the lastest changes that have been merged:
  * `git pull`
3. Option: merge those changes into any feature branches you've been working on:
  * `git checkout your_branch_name`
  * `git merge master`

## Fixing Merge Conflicts

1. Identify that you're in a merge conflict:
  * `git status` - note the files that are listed as *both modified*
2. Open those files in your text editor.
3. Identify areas tagged with `>>>>>>>>>`, `==========`, and `<<<<<<<<<<`.
```
<<<<<<< HEAD:file.txt
This is the original code in your current branch
=======
This is the modified code
>>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt

```
4. Fix all the code between those lines, and remove the lines.
  * Ideally, run the code locally and confirm it works.
5. Commit your changes:
  * `git add file1 file2`
  * `git commit -m "your message describing how you fixed conflict"`
6. Push your updated branch:
  * `git push origin branch_name`

![workflow](github_workflows.jpg)
