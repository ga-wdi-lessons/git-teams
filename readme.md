# Git Teams & Workflow

![Voltron Team](https://i.ytimg.com/vi/tZZv5Z2Iz_s/hqdefault.jpg)

## Learning Objectives

- Distinguish between git workflow models to organize code changes and collaborate as a team
- Use branches and pull requests to isolate changes tied to specific features
- Efficiently and correctly resolve merge conflicts

## Framing: Review Basic Git Workflow

Although you've all been using Git and Github for a couple months, you've largely been doing so individually. In the wild, software development rarely takes place in this kind of workflow. When you are working in the industry, you will likely be part of a development team.

We'll be working in small teams for Project 3 to gain a sense of collaborative development. Clear, repeatable version control practices, combined with good communication make collaboration easier and more efficient. In order to build up to that, we need to make sure we're building on a solid foundation of Git basics.

### Why Use Version Control?

When you're working on a project, you sometimes want to be able to retrace your steps, or even revert your project to a previous state.  And often (particularly in the workplace) you need a way to effectively collaborate on a single project without stepping on each others' toes. Version control tools address all of these needs.

### Why Git?

Git, apart from being free and open source, is also in many ways a superior system to many older version control tools (such as Subversion) because it is a "distributed" version control tool. Distributed simply means that there will be 'redundant' copies of repositories held by multiple people. We've been just thinking of these as **forks**.

This means that there is no centralized approval structure for making changes to the project; instead, every student who clones the repository has their own **complete copy**, which they can then edit and change. This makes it much easier to use when working in groups, since each member can have an up-to-date and complete repository.

### Review Git Branching

A branch in `git` is just a label on a particular commit in a repository, along with all of its history (parent commits). When we commit, the current branch label moves forward to the new commit. Another way to say that is the branch label always stays at the tip of the branch.

> `HEAD` indicates the last commit on the currently checked out branch. When we run `git branch <new branch>`, new branches get added at wherever `HEAD` points. It is possible (and frequently desirable) to checkout a commit that is not the latest commit on a branch. When you do this, you have a _detached HEAD_; more [here](http://stackoverflow.com/a/2529982).

![Git Branch Diagram](https://www.atlassian.com/git/images/tutorials/collaborating/using-branches/01.svg)

> From [Atlassian - Git Branching Tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-branch)

#### Why is branching an important part of git?

Branches are useful for many reasons, but some of the most common ones:

1. To allow experimentation. By switching to a new branch, we can experiment, and if the experiment fails, we can easily switch back to master (or another branch of our choice). If it succeeds, we can merge those changes into master.

2. To allow work to proceed on multiple features (or by multiple people) without interfering. When a feature is complete, it can be merged back into master.

3. To allow easy bug fixes on a stable version while features are being developed.

## Single-Remote Workflows

### Centralized Workflow

The remote repo has one single branch on it, master. All collaborators have separate clones of this repo. They can each work independently on separate things. However, before they push, they need to run git fetch/git pull to make sure that their **local** copy of the `master` branch isn't out of sync with the **remote** `master` branch.

> [git fetch vs git pull](https://codeahoy.com/2016/04/18/10-git-pull-vs-git-fetch-%28and-stashing%29/)

![Centralized Workflow Diagram](https://www.atlassian.com/git/images/tutorials/collaborating/comparing-workflows/centralized-workflow/01.svg)

> From [Atlassian - Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow)

**(+)** Very simple

**(-)** Collaboration is kind of clunky.

### Feature Branch Workflow

This workflow is very similar to the 'Centralized' workflow. The biggest difference is that there are branches (which helps to keep feature-related commits isolated), and that instead of pushing changes up directly, collaborators (a) push up changes to a remote that ***is not*** `master`, and (b) submit a pull request from the feature branch to ask for them to be added to the remote repo's master branch.

![Feature Branch Workflow](https://wac-cdn.atlassian.com/dam/jcr:80d671b1-8a4b-4378-914c-e25fe3d2dcce/07.svg?cdnVersion=dj)

> From [Atlassian - Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)

**(+)** Better isolation than Centralized model, but sharing is still easy. Very flexible.

**(-)** Sometimes it's too flexible - it doesn't distinguish in any meaningful way between different branches, and that lack of structure can be problematic for larger projects.

## Exercise: Merging: The Good, The Bad, and The Ugly (Feature Branch Workflow)

Form pairs. Decide who will be Student 1, and who will be Student 2!

**Student 1**

- Create a new repo named `emergency_compliment`. Don't select the `Initialize this repository with a README` option on GitHub.
- Add the second student as a collaborator to your repo by going to the `Settings` tab then selecting `Collaborators & Teams` on the left.

1. `git clone <url>`
2. `cd emergency_compliment`
3. `create-react-app .`
4. `git add .`
5. `git commit -m "initial commit"`
6. `git push origin master`
7. `atom .`

**Student 2**

After Student 1 is done pushing his code:

1. `git clone <url>`
2. `cd emergency_compliment`
3. `npm install`
7. `atom .`

**Each Student**

* Check out a new feature branch and create a Hello component. It should take the users' name, and return `Hello {name}`. Keep it simple!

* Commit your changes and push them to the remote repo using this command `git push origin <branch name>`. Open a pull request on Github to merge the changes from your feature branch into `master`.

* Each student should add a comment to the PR! It should be an inline comment asking a question about the code, a suggestion or just adding an observation!

* If there are no conflicts, merge your pull request and delete your feature branches!

* If there are merge conflicts, WAIT to merge the conflicts until the next `Exercise`.  You will need to `git pull` the latest changes, resolve the conflict, then `commit` again.

Next, try to break it!!!!

## Resolving Merge Conflicts

When you encounter a `merge conflict`,instead of directly merging, Git asks the user to manually resolve the conflicts. In your project files, after trying to merge, those conflicts usually look something like this...

```js
<<<<<<< HEAD
var x = 1,
    y = 2;
=======
var x;
>>>>>>> other_branch
```

The first section is the version that exists on the `current branch`; the second section is the version that exists on the branch you're trying to pull in. Figure out which version of the code makes the most sense moving forward, delete the version that doesn't and all the extra stuff that Git adds (`<<<<<<<`, `=======`, etc.) and run `git commit` to finalize the merge.

For example, if we decided we only needed var x, delete the other "stuff":

```diff
- <<<<<<< HEAD
- var x = 1,
-     y = 2;
- =======
+ var x;
- >>>>>>> other_branch
```

Now, we have only the code we need and can commit the changes we made to resolve the merge conflict.

### Exercise: Merge Conflicts

**Both Students**

* First, make sure all remote `PRs` and branches have been merged together. Once your changes are successfully merged, delete your feature branches from GitHub and your local machines.

* **Locally**, make sure you are checked out to our `master` branch.

* Then, do a `git pull origin master` to receive the latest changes.

* **Note** If you encounter a merge conflict, work together to resolve it before continuing. Then push up the changes!

* Check out a new feature branch, and create a new `Compliment` component. It should return a random compliment from the list below:

```
var data  = ["Good effort!", "What a fine sweater!", "I appreciate all of your opinions.", "I like your style.", "Your T-shirt smells fresh.", "I love what you've done with the place.", "You are like a spring flower; beautiful and vivacious.", "I am utterly disarmed by your wit.", "I really enjoy the way you pronounce the word 'ruby'.", "You complete me.", "Well done!", "I like your Facebook status.", "That looks nice on you.", "I like those shoes more than mine.", "Nice motor control!", "You have a good taste in websites.", "Your mouse told me that you have very soft hands.", "You are full of youth.", "I like your jacket.", "I like the way you move.", "You have a good web-surfing stance.", "You should be a poster child for poster children.", "Nice manners!", "I appreciate you more than Santa appreciates chimney grease.", "I wish I was your mirror.", "I find you to be a fountain of inspiration.", "You have perfect bone structure.", "I disagree with anyone who disagrees with you.", "Way to go!", "Have you been working out?", "With your creative wit, I'm sure you could come up with better compliments than me.", "I like your socks.", "You are so charming.", "Your cooking reminds me of my mother's.", "You're tremendous!", "You deserve a compliment!", "Hello, good looking."];
```

**Student 1**

* Rename the component `Compliment` into `Compliments`.

**Student 2**

* Rename `var data` into `const compliments`

**Student 1**

* Commit your changes and push them to the remote repo. Open a pull request on Github, and merge the changes on your feature branch into `master`.

**Student 2**

* Commit your changes, and still on your `feature` branch, pull the `master` changes from GitHub by using `git pull origin master`.

**Both Students**

On `Student 2's computer`, look over the merge conflicts, resolve it locally, commit, and push.

**Student 2**

Push your feature branch to GitHub using `git push origin <branch>`. Then create a PR, and merge your branch into master.

**Student 1**

Pull down the changes to `master`


#### Further Reading

Checkout the [GitHub docs on resolving a merge conflict](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/)

### Think/Pair/Share - 5/5

Discuss with your partner and write down the answers to the following questions below. Afterwards, we will discuss your ideas together as a class.

Some things to consider:

1. How did you go about resolving merge conflicts? What process did you take?
2. What were the necessary commands to run to incorporate those changes?
3. What kind of system and channels best allow developers to prevent, and resolve merge conflicts most effectively?

## Rebasing

Rebasing allows us to rearrange and effectively rewrite our commit history! Rather than combining the most recent commits from two different branches via a single commit, it combines the two branches themselves, rearranging their commits while ***re-writing*** the repo's commit history. For that reason, it can be dangerous.

## Git Merge

![Git Pull/Merge](https://git.generalassemb.ly/storage/user/6376/files/aee6a68e-81b6-11e7-9fb7-31c12053681f)

## Git Rebase

![Git Rebase](https://git.generalassemb.ly/storage/user/6376/files/c6f3d54e-81b6-11e7-9f1b-c5a81d1e0207)

[Document Dive](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/)

***Example Scenario:***

Here's what a rebase looks like. Suppose we have two branches, a master and a feature branch.

One day, someone makes a commit onto the master branch. We want to include those changes into our feature branch, so that our code doesn't conflict with theirs. From our feature branch, if we run the command `git pull --rebase <remote> <branch>`, we can tell git to rewrite the history of our feature branch as if the new commit on master had always been there.

Rebase is extremely useful for cleaning up your commit history, but it also carries risk; when you rebase, you are in fact discarding your old commits and replacing them with new (though admittedly, similar) commits, and this can seriously screw up a collaborator if you're working in a shared repo. **The golden rule for git rebase is "Only rebase before sharing your code, never after."**

Like git merge, git rebase also sometimes runs into merge conflicts that need to be resolved. The procedure for doing this is almost the same; once you fix the conflicts, run `git rebase --continue` to complete the rebase.

## Optional Practice: Resolve Merge Conflicts w/ Rebase

**Both Students**

- Check out a new feature branch.
- Create a `Compliment.css` file and add CSS to our emergency compliment page
- Import your stylesheet into `Compliment.js`.
- Each add unique CSS styling of your choosing.
- Both students should add and commit changes.

**Added Bonus**

For a bonus, **both students** should work on functionality to display **all** of the compliments instead of one.

**Student 1**
push branch and make a pr, and merge your changes.

**Student 2**
grab the necessary changes with `git pull --rebase <remote> <branch> `, fix any merge conflicts, run `git add` then resolve with `git rebase --continue`.


## Integration Manager Workflow (Distributed Workflow)

These approaches all use multiple remote repos; typically, everyone has their own fork of the 'original' project (the version of the repo that's publicly visible and is managed by the project maintainer), and changes are submitted via pull request.

How It Works: One collaborator plays the role of 'Integration Manager'. This means that they are responsible for managing the official repository and either accepting or rejecting pull requests as they come in.

**(+)** One student integrates all changes, so there's consistency.

**(-)** Could get overwhelming for large projects.

## Git Workflow Tips

### Using `git-fetch` and `git-diff`

What if you are a little out of sync with your teammates and are worried that a `git pull` will result in hours of working through merge conflicts?

Use `git-fetch` and `git-diff` to see the changes instead!

```bash
$ git fetch <remote> <branch>
$ git diff <remote>/<branch>
```

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to try that commit again, you can run `git commit --amend` with the `--amend` option...

```sh
$ git commit --amend
```

### Deleting Branches: Locally VS Remote

Locally...

`git branch -d <branch>` Deletes local branch

`git branch -D <branch>` Forces delete for un-merged branches

Remote...

`git push origin :<branch>` Deletes Remote Branch

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

Example Aliases...

```
[alias]
  g = git
	current = rev-parse --abbrev-ref HEAD
	gl = git log --all --oneline --graph --decorate
```

If you are adding an Alias to your bash profile you might have to reload to see your updates by running `$ source ~/.bash_profile`

### Additional Tools

[`git-wtf`](http://git-wt-commit.rubyforge.org/): Script that displays the state of your repository in a readable and easy-to-scan format

[`git-create`](https://www.viget.com/articles/create-a-github-repo-from-the-command-line): Bash function that creates a github repo from the command line


[`hub`](https://github.com/github/hub): "is a command line tool that wraps git in order to extend it with extra features and commands that make working with GitHub easier." Hub is built and maintained by GitHub

## Software Development and Collaboration

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

## Closing

### Review Questions
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
- [Git Alias](https://githowto.com/aliases)
