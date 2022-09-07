<h1 align="center">Välkommen (Welcome)</h1>
Hello, new (or returning developer)! To facilitate the smooth development of our project, please take a look at the instructions below.
skill issue- love omar
<br>

<details>
<summary><b>Git Instructions</b></summary>
<br>
## Personlig åtkomsttoken (Personal Access Token)
In August of last year, Github deprecated passwords when pushing code to a remote (a repository hosted on the cloud, e.g. someone else's computer). Instead, they want you to use a Personal Access Token (PAT). Think of a PAT like a password, but you can have more than once, and each has different permissions. Don't worry, for now, you can have a single PAT that controls everything (you may want to create a unique one for each computer, in case one gets compromised).

Here's how you may create a PAT:
1. Go to [your profile](https://github.com)

2. Go to [your settings](https://github.com/settings/profile)

3. Go to [developer settings](https://github.com/settings/apps), then to [Personal Access Tokens](https://github.com/settings/tokens)

4. Click [Generate New Token](https://github.com/settings/tokens/new)

5. Change the note to your computers name (e.g. "School Computer")

6. Set the expiration to never. This is not very secure, but you can always revoke your token if someone breaks into your account.

10. Check the boxes you want this PAT to control. At the very minimum, include `repo`, and everything under it.

11. Click Generate Token.

12. **Do not exit this page, and make sure to copy your key to your clipboard for now.**

Your token should like roughly like this (I have since revoked this token, it will not work on my account):
```
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
```

 13. After that, open your terminal, and type `git config --global credential.helper`. This will store your PAT (albeit in plain text), so you won't have to type it in again.

 14. To save your password, try performing a "restricted action," e.g. cloning a private repository.

 15. Enter your username, and paste in your PAT.

 16. If all goes well, your PAT is saved! If not, contact me at [milobanks@rowlandhall.org](mailto:milobanks@rowlandhall.org).

### Notera (Note)
Please make all your changes on a separate branch that describes what you are doing, prefixed with your name (e.g. `milo-fixing-issue-420`, `attenborough-Gradle-dep-update`). Don't make these too long, though.

## Praktiska kommandon (Handy commands)
Git has many commands, but some you will use more than others. Here are a select few.
```bash
# Creates a repository, but only on your local computer, not on Github
git init

# Downloads a repository
git clone <repository>

# Add a file for Git to track
git add <file>

# Stop tracking a file (does not actually delete the file)
git rm <file>

# Create a commit (a snapshot of the projects currently saved changes)
git commit -m "your commit message"

# We need to tell Git where our remote repository is located. This is what a remote is.
# Origin is your fork; upstream is the original repository.
# Create remote
git remote add <name> <url.git>

# Change url of remote
git remote set-url <name> <new-url.git>

# Push your changes (you only need to supply the arguments from -u onward the first time)
git push -u <where to push, origin> <the branch to push from, branch your changes are on>

# Pull changes
git pull <where to pull, origin> <the branch to pull too, master>
```

---

Let's look at an example of how you might fix a spelling mistake in the README.

First, fork the repository. Go to the official repository [here](https://github.com/Rowland-Hall-Iron-Lions/ARC), and press the fork button in the upper right-hand corner. You only need to do this once.

Obviously, you need to grab your forked repository so you have code to work on. You only need to do this once.
```bash
git clone https://github.com/Rowland-Hall-Iron-Lions/ARC.git
cd ARC;

# Here, we do something a bit strange. Origin is the name of the remote for your fork, while upstream is the name of the remote for the main repository. Think of your repository being downstream (changes flow downstream) to you.
git remote add upstream https://github.com/Rowland-Hall-Iron-Lions/ARC.git
```

You might be wondering why we don't set the `origin` remote. After all, isn't that our fork? Yes, it is! But since we cloned it from there, our origin is already set up for us. Thanks git!

If this is not your first change, it is **highly recommended** that you fetch the latest changes to your main fork. You can do this from the command line or the Github website. On the website, you can click "fetch upstream" and follow the instructions. If, however, you want to do this from the command line (recommended, as you learn mode), you can do this:
```bash
# We are fetching and merging the changes from upstream (the original repository) to your fork. Master is the name of the main branch your fork has.
git pull upstream master

# If you fetched from upstream on the website, you must do this (overwise, don't)
git pull origin master
```

After this, you will want to create a separate branch for your changes.
```bash
# Obviously replace the branch name with <your-username>-<fixing>
git checkout milo-readme-typo
```

Make your changes (maybe correct Rowland to Rowland), and add the files you changes.
```bash
git add .
```

Create a commit to push.
```bash
git commit -m "Fix readme typo."
```

Set your origins (you only have to do this the first time).
```bash
git remote add origin https://github.com/<your-username-where-the-fork-is>/ARC.git
git remote add upstream https://github.com/Rowland-Hall-Iron-Lions/ARC.git
```

And push the `isacc-barker-readme-typo` branch!
```bash
git push -u Isacc-barker-readme-typo origin
```

If you get an error about not having local changes, fetch the latest changes.
```bash
git pull origin Isacc-barker-readme-typo 
```

You may get a merge conflict. Go into all the files, remove all the "merge conflict markers" (discussed later), and add the files again. Create a new commit (maybe "fixed merge conflict"), and try to push again.

You may be wondering, but Author, I don't have the changes I made on my new branch on my master branch! Well, that's still fine. In fact, it's excellent! You can see from this diagram:
```
isacc-barker-readme-typo(local,origin) -> isacc-barker-readme-type(remote,origin) -> master(remote,upstream) -> master(local,origin)
```

All you have to do is submit a PR to the main repository, fetch the changes to your own fork once it goes through, and sync your local repository with `git pull`!

## Bidragande kod (Contributing code)
What good is pushing to the central repository when it rejects it? You might get an error like the following when pushing:
```
! [remote rejected] master -> master (protected branch hook declined)
error: failed to push some refs to [and so on]...
```

You shouldn't have gotten this error if you took my advice, but let's use this as a learning opportunity.

### Vad är ett förvar (What is a repository)
A repository is a group of branches. That's it. Granted, it also contains metadata about your repository, but its primary purpose is just to hold branches. Branches are the things that have the files, and by default, the primary branch name is "main" (because we are basing this repo of FtcRobotController, and they use the main branch called "master"), we use master instead of main. Main is considered newer, and master is considered [legacy](https://github.com/github/renaming).

### Vad är en gren (What is a branch)
Think of a branch as a snapshot of your changes. You can switch to a snapshot and write your changes. Whenever you create a new feature or fix something, big or small, you should create a new branch to reflect this. Below is a cheat sheet of handy git branch commands.
```bash
# Rename the current branch
git branch -m <new-name>

# List all branches
git branch

# Change branches
git checkout <branch-name>

# Delete a branch
git branch -d <branch-name>

# Create a branch (and switch to it)
git checkout -b <new-branch>

# Create a branch (and don't switch to it)
git branch <new-branch>
```

### Vad är en skyddad gren (What is a protected branch)
A protected branch is a branch that is... well... protected. The idea of this is to make sure that the protected branch only has the best code we have to offer. To push code into this branch (which people will `clone`), you must fork the repository (you only need to do this once), create a PR (for every *one* significant change that you make), get someone to look over your code, and merge it! This process may not sound straightforward, but it should seem pretty intuitive with a bit of explanation.

### Vad är en gaffel (What is a fork)
Imagine having a friend with a repository that contains pictures of [cats](https://en.wikipedia.org/wiki/Cat) (for those of you who do not know what a cat is, a link has been provided for your convenience). Now, your friend doesn't have a picture of *your* cat. How dare they‽ You decide you must get your cat photo there, but how? This is where everything comes in handy. If you fork your friend's repository, you get a copy. You can do whatever you want with this copy, but most importantly, you can submit your changes (or "open a pull request").

Think of each repository as a dot. Let's graph the relation between your two repositories.

```
[Friends repo] ---------------------------- [Your fork]
```

Simple, right? But what happens if someone else forks your friend's repo, but this time to submit a picture of their [dog](https://en.wikipedia.org/wiki/Dog) (again, a link has been provided). The graph would now look like this:

```
                            [-------------- [Dog fork]
[Friends repo] -------------]
                            [-------------- [Your fork]
```

Note that the resemblance to a fork in this diagram is *entirely coincidental* (no conspiracy theories, please). Remember these two forks; they will come in handy later.

Ok, so you made your changes; how do you push your changes back to your friend's repo? This is where "pull requests" come in handy.

### Vad är en dragbegäran (What is a pull request)
Contrary to the name, a pull request (PR) is requesting the original repository (called the upstream) pulls the changes from your fork (called the origin). The reason for this contradictory name is explained [here](https://stackoverflow.com/questions/21657430/why-is-a-git-pull-request-not-called-a-push-request), if anyone is interested. Anyways, once you try and push your changes, you will be met by a window asking what you want to title your pull request. It will also ask you for a description, in which you should **always** state what you changed. After that, press create pull request!

Depending on how the "upstream" (remember back to the first part of this section) handles pull requests, it may be sent to be reviewed by other people, and it may run through automated testing. In our case (the `ARC` repository), both of these will occur. Don't worry; you won't have to do anything, save for if something goes wrong. After this process is finished, you may be asked to change your code or merge. Merging means "merging" or inserting the changes in your pull request into upstream.

This pull request process and associated checking may seem silly but remember to the person who wants to insert their dog. While we do love dogs, there is a strict rule about no dogs where the cats are. A review may be left, saying "move your dog photos to a directory/folder marked dog", and the person would fix that. After this, Github will merge the pull request!

### Vad är en sammanslagningskonflikt (What is a merge conflict)
You have just wandered upon one of the most feared outcomes of Git (or any VCS in general): **a merge conflict**! But don't scream in horror, like I'm sure your peers are doing, and instead follow these instructions. Somewhere on the PR page, it will say you cannot merge due to a merge conflict and that you must fix them before you can merge. How can you fix them? Well, you have two options.

 1. Github might give you the option to solve the conflict online, which you will want to do. Github will walk you through it, but if it doesn't, you will see "conflict markers" (`<<<<<<<` and `>>>>>>>`) in the affected files. In between, there are two conflicting versions of code (separated by `=======`). Figure out which one is better, and make the code valid again.

 2. Resolve them locally, on your computer, in case the conflict is too advanced.

In order to solve them on your computer, follow the instructions on Github.

# Frågor (Questions)
File a Github issue or contact me at my email, [milobanks@rowlandhall.org](mailto:milobanks@rowlandhall.org).
</details>
