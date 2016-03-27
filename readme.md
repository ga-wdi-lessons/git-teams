# Git Teams & Workflow

## Learning Objectives
- Distinguish between git workflow models to organize code changes and collaborate as a team
- Use branches and pull requests to isolate changes tied to specific features
- Efficiently and correctly resolve merge conflicts
- Explain the difference between `rebase` and `merge`

## Framing: Review Basic Git Workflow (5 mins)

Although you've all been using Git and Github for over a month, you've largely been doing so individually. In the wild, software development rarely takes place in this kind of workflow. When you are working in the industry, you will likely be part of a development team. You will definitely be part of a development team as you complete Project 3. Clear, replicable version control practices, combined with good communication, can make collaboration easier and more efficient. In order to build up to that, we need to make sure we're building on a solid foundation of Git basics.

### Why Use Version Control?
When you're working on a project, you sometimes want to be able to retrace your steps, or even revert your project to a previous state.  And often (particularly in the workplace) you need a way to effectively collaborate on a single project without stepping on each others' toes. Version control tools address all of these needs.

### Why Git?
Git, apart from being free and open source, is also in many ways a superior system to many older version control tools (such as Subversion) because it is a "distributed" version control tool. This means that there is no centralized approval structure for making changes to the project; instead, every student who clones the repository has their own complete copy, which they can then edit and change. This makes it much easier to use when working in groups.

### Git Branching

A branch in git is just a label on a particular commit in a repository, along with all of its history (parent commits). When we commit, the current branch label moves forward to the new commit. Another way to say that is the branch label always stays at the tip of the branch.

> `HEAD` indicates the point on the repository that we're reading from. When we run `git branch`, new branches get added at wherever `HEAD` points. If 'HEAD' is pointing at the end of a branch, it also means that new commits will be added to that branch.

![Git Branch Diagram](https://www.atlassian.com/git/images/tutorials/collaborating/using-branches/01.svg)

> From [Atlassian - Git Branching Tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)

Q. Why is branching an important part of git?
---

> A. Branches are useful for many reasons, but some of the most common ones:

> 1. To allow experimentation. By switching to a new branch, we can experiment,
and if the experiment fails, we can delete it and easily switch back to master
(or another branch of our choice). If it succeeds, we can merge those changes
into master.
2. To allow work to proceed on multiple features (or by multiple people) without
interfering. When a feature is complete, it can be merged back into master.
3. To allow easy bug fixes on a stable version while features are being developed.

## You Do: Emergency Compliment Angular - Setup (5 min)

Form pairs. To start:
- One student should fork and clone the [starter-code](https://github.com/ga-wdi-exercises/emergency_compliment) to their GitHub
- Add the second student as a collaborator to this repository
- The second student should clone the newly-forked repo, so they have a local copy and can start working

```bash
$ git checkout git-teams-starter
```

## Single-Remote Workflows (15 min)

### Centralized Workflow

How It Works: The remote repo has one single branch on it, master. All collaborators have separate clones of this repo. They can each work independently on separate things. However, before they push, they need to run git fetch/git pull to make sure that their master branch isn't out of date. 

![Centrialized Workflow](https://www.atlassian.com/pt/git/workflows/pageSections/00/contentFullWidth/0/tabs/00/pageSections/07/contentFullWidth/02/content_files/file/git-workflow-svn.png)

>Who might use a Centrialized Workflow? 
>***A small team***

**(+)** Very simple

**(-)** Collaboration is kind of clunky.

### Feature Branch Workflow

How It Works: This workflow is very similar to the 'Centralized' workflow. The biggest difference is that there are branches (which helps to keep feature-related commits isolated), and that instead of pushing changes up directly, collaborators (a) push up changes to a new remote branch rather than master, and (b) submit a pull request to ask for them to be added to the remote repo's master branch.

![Feature Branch Workflow](https://www.atlassian.com/pt/git/workflows/pageSections/00/contentFullWidth/0/tabs/01/pageSections/07/contentFullWidth/0/content_files/file0/document/git-workflow-feature-branch-1.png)

>Who might use a Centrialized Workflow? 
>***GA WDI Instructional Team!***
>[Garnet](https://github.com/ga-dc/garnet)

**(+)** Better isolation than Centralized model, but sharing is still easy. Very flexible.

**(-)** Sometimes it's too flexible - it doesn't distinguish in any meaningful way between different branches, and that lack of structure can be problematic for larger projects.

## You Do: Merging: The Good, The Bad, and The Ugly (Feature Branch Workflow)

**Throughout today's exercises, we will use the `git-teams-starter` branch where we would usually use `master`.**

### PRs and Merging (10 min)

- **Student 1** Check out a new feature branch and create a `js/app.js` file. Then, work with your partner to write code for our first module in `js/app.js` to instantiate our `compliments` Angular App.

- Don't forget to add a Script Tag for `js/app.js` in our `index.html`!

  [See Solution](https://github.com/ga-wdi-exercises/emergency_compliment/commit/5fbb7c0e0a3dd71bc39bf188d2c30ec4f7447aeb?diff=unified)

- **Student 2**
Check out a new feature branch and add a `js/compliments` directory route and create a `js/compliments/compliments.controller.js` file in our directory.

Inside of our `compliments.controller.js` add in the following code to instantiate our controller for our main app:

```js

`use strict`;

(function(){
  var app = angular.module("compliments");
  app.controller("complimentsController", ComplimentsController);

  function ComplimentsController(){
    var vm = this;
  }

}());

```
Make sure to also add our Script tag in our `index.html`!

- **Both Students**
Commit your changes and push them to the remote repo. Open a pull request on Github to merge the changes from your feature branch into `git-teams-starter`.

- Each student should add a comment to the PR! It should be an inline comment asking a question about the code, a suggestion or just adding an observation!

- If there are no conflicts, merge your pull request. If there are, you will need to  `git pull` the latest changes, then `commit` again. 
- Once your changes are successfully merged, delete your feature branches, check out `git-teams-starter`, and `pull`.

**Reminders**:

1. If you already have an `emergency_compliment` repo, you can clone it down and give it a different name using: `git clone <repo url> <name for repo>`
2. Make sure you are starting your branches from an `git-teams-starter`
3. If you need to get more branches, or had forked previously, you are going to want to set the `ga-dc` version of `emergency-compliment` as your `upstream` remote.
4. Be mindful of the commands you are running, e.g. careful not to run `git checkout -b` when you are trying to switch between branches, this will create new branches.

Next, try to break it!!!!

### Merge Conflicts (15 min)

- **Both Students**
Check out a new feature branch and add code to our to `complimentsController` so we can use `ng-controller` in our views to see a a random compliment

- Then, add the code in our `index.html` outlined below. We will be creating a div with the directive `ng-controller`.

- Work to display the `text` of a random compliment in `data.js` by writing the code within the below div:

```js
<div data-ng-controller='complimentsController as vm'>
</div>
```

[See Solution](https://github.com/ga-wdi-exercises/emergency_compliment/commit/c54fa09c4b7a54ade8b746425a232e260425a9b1)

- **Student 1**
Change our Angular App name from `compliments` to `emergencyComp` and ALL instances of it referenced in our application!

- **Student 2**
Change the name of our `complimentsController` in `js/compliments/compliment.controller.js` AND `index.html` to  `mainController`

- **Both Students**
Commit your changes and push them to the remote repo. Open a pull request on Github to merge the changes on your feature branch into `git-teams-starter`.

- **Student 1**
Merge your changes into `git-teams-starter` on GitHub.

- **Student 2**
Check your PR -- there should be a merge conflict!

- **When you finish:**
Don't worry about writing any code to resolve the merge conflict now, instead, decide between your group how to think about and outline the steps for the next commit.

### Think/Pair/Share - 5/5 (10 min)

Discuss with your partner and write down the answers to the following questions below. Afterwards, we will discuss your ideas together as a class.

Some things to consider:

1. Who will resolve the conflict?
2. What are the necessary commands you will need to run to incorporate those changes?
3. What kind of system and channels best allow developers to prevent, and resolve merge conflicts most effectively?

## BREAK (10 min)

## Resolving Merge Conflicts (5 min)
In cases like the one we have created, instead of directly merging, Git asks the user to manually resolve the conflicts. In your project files, after trying to merge, those conflicts usually look something like this:
```
<<<<<<< HEAD
var x = 1,
y = 2;
=======
var x;
>>>>>>> other_branch
```
The first section is the version that exists on the current branch; the second section is the version that exists on the branch you're trying to pull in. Figure out which version of the code makes the most sense moving forward, delete the version that doesn't and all the extra stuff that Git adds (<<<<<<<, =======, etc.) and run `git commit` to finalize the merge.

For example, if we decided we only needed var x, delete the other "stuff":

`var x;`
Now, we have only the code we need and can git commit.

## You Do: `Git Pull (Merge Conflicts)` (10 min)

- **Student 2**
``` bash
git checkout git-teams-starter
git pull origin git-teams-starter
git push <remote> <your-branchname>
```
- **Both Students**
On `Student 2's computer`, look over the merge conflicts, resolve it locally, commit, and push.

- **Student 1**
Pull down the changes to `git-teams-starter`

## Rebasing (10 min)

Rebasing allows us to rearrange and effectively rewrite our `git commit` history! Rather than combining the finished data from two different branches via a single commit, it combines the two branches themselves, rearranging them and, effectively, re-writing history.

[Git Merge Versus Rebase](https://gist.github.com/beckybeauchamp1/51a805c61e8b30624cc1)

[Document Dive](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/)

### Turn and Talk - 2/3 (5 min)

 Turn to your neighbor and discuss why you might use a `rebase` instead of a `git merge`

***Example Scenario:***

Here's what a rebase looks like. Suppose we have two branches, a master and a feature branch.

One day, someone makes a commit onto the master branch. We want to include those changes into our feature branch, so that our code doesn't conflict with theirs. From our feature branch, if we run the command `git pull --rebase <remote> <branch>`, we can tell git to rewrite the history of our feature branch as if the new commit on master had always been there.

Rebase is extremely useful for cleaning up your commit history, but it also carries risk; when you rebase, you are in fact discarding your old commits and replacing them with new (though admittedly, similar) commits, and this can seriously screw up a collaborator if you're working in a shared repo. **The golden rule for git rebase is "Only rebase before sharing your code, never after."**

Like git merge, git rebase also sometimes runs into merge conflicts that need to be resolved. The procedure for doing this is almost the same; once you fix the conflicts, run `git rebase --continue` to complete the rebase.

## You Do: Resolve Merge Conflicts w/ Rebase (20 min)

**Both Students**
- Check out a new feature branch.
- Create a `styles.css` file and add CSS to our emergency compliment page
- Link to your stylesheet from the `<head>` of `index.html`.
- Each add unique CSS styling of your choosing.
- Feel free to modify the index.html as well.

- **Both students** 
Add and commit changes.

- **Added Bonus**
For a bonus, `Both students` should work on functionality to display `all` of the compliments instead of one.

[See Solution](https://github.com/ga-wdi-exercises/emergency_compliment/commit/397766964b0d69f063476422d65bd8f2aefe70a0)

- **Student 1**
push branch and make a pr, and merge your changes.

- **Student 2**
then try to do the same thing.

- **Student 2**
grab the necessary changes with `git pull --rebase` and resolve any merge conflicts with `git rebase --continue`.

## Break (10 min)

## Integration Manager Workflow (Distributed Workflow) (5 min)

These approaches all use multiple remote repos; typically, everyone has their own fork of the 'original' project (the version of the repo that's publicly visible and is managed by the project maintainer), and changes are submitted via pull request.

How It Works: One collaborator plays the role of 'Integration Manager'. This means that they are responsible for managing the official repository and either accepting or rejecting pull requests as they come in.

**(+)** One student integrates all changes, so there's consistency.

**(-)** Could get overwhelming for large projects.

## Git Workflow Tips (10 min)

### Using `git-fetch` and `git-diff`

What if you are a little out of sync with your teammates and are worried that a `git pull` will result in hours of working through merge conflicts?

Use `git-fetch` and `git-diff` to see the changes instead!

```sh
$ git fetch
$ git diff origin/master
```

### Amending Commits 
One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to try that commit again, you can run `git commit --amend` with the `--amend` option:

```sh
$ git commit --amend
```

### Git Blame

`git blame <file_name>`

Git blame allows you to see who has made changes to a file, or when the file was last changed by someone. This can be used to find out what feature(s) were added.

To find out who changed a file, you can run git blame against a single file, and you get a breakdown of the file, line-by-line, with the change that last affected that line.

Additionally, this feature is available to view on Github!

To use git blame on `GitHub`:

* Navigate to a repository, and click on a file that you're interested in.
* Click on the Blame button in the upper-right tab list.
* Browse the list of changes in a file.

### Git Aliases

Aliases allow us to configure shortcuts and can help speed up our workflow!

We can configure them in our `.gitconfig` or `.bash_profile`

Example Aliases:
```
[alias]
  g = git
	current = rev-parse --abbrev-ref HEAD
	gl = git log --all --oneline --graph --decorate
```

If you are adding an Alias to your bash profile you might have to reload to see your updates by running `$ source ~/.bash_profile`

[Git Alias](https://githowto.com/aliases)

### Git Bash Scripts

`git-wtf`: Script that displays the state of your repository in a readable and easy-to-scan format

[Open Source Scripts/Git Tools](http://git-wt-commit.rubyforge.org/)

`git-create`: Bash function that creates a github repo from the command line

[Create Github Repos From Command Line](https://www.viget.com/articles/create-a-github-repo-from-the-command-line)

## Software Development and Collaboration (5 min)

### Project Week: What does that mean for you?

Regardless of the `git` approach you decide to take for Project 3, it's important that you establish a workflow and plan!

Focus then on setting goals for yourself in small sprints, and working together to organize and create a schedule.

When planning these sprints, set concrete goals for yourself. I'm going to achieve X by 12:30 so that I can get started on Y after lunch. I will finish Y by close of business so that I can start on Z. You could scale even further than that.

It is VITAL that you guys schedule yourselves well.

### Why do code reviews?

Jeff Atwood (co-founder of Stack Exchange, and a smart dude) has written a
[great summary](http://blog.codinghorror.com/code-reviews-just-do-it/) which I
encourage you to read. The short version? Code reviews can reduce the number of
errors in our programs dramatically.

In addition we believe that learning to read code critically is an important
part of improving our own code. After all, to improve our own code, we must read
it, looking for ways to improve it.

Additionally, many work environments practice some form of code review, so it's
good to get practice in giving feedback to others now.

Furthermore, `Github` allows us to comment directly on `PRs`, so we can easily incorporate informal code reviews into our workflow.

Interested to read more about [code reviews?](https://github.com/ga-dc/project2-code-review/blob/master/code_review_primer.md)

## Closing (5 min)

### Quiz Questions
- Identify the syntax needed to create a new branch. How about creating a new branch and switching to it?
- Why should you never work on the same files on different branches?
- Explain the difference between rebase and merge

### Cheat Sheets
- [Github Official](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)
- [Interactive Git](http://ndpsoftware.com/git-cheatsheet.html#loc=stash;) (Uses slightly different terminology that we're used to, but nifty)

### Rebase vs Merge
![Rebase vs Merge](https://raw.githubusercontent.com/gitforteams/diagrams/master/flowcharts/rebase-or-merge.png)

### Further Reading
- [Jesse's blog post!](https://jesse.sh/rebases/)
- [Git Workflows Overview](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Git Teams](http://gitforteams.com/)
