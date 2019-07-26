---
layout: post
title:  "Git Wizardry"
date:   2019-07-24 10:08:57 +0530
categories: jekyll update
---

>The following is a monologue I have made to make learning git 
>a bit more interesting.
>
>Any resemblance to the some other story is purely coincidental.
>None of the git commands have been abused during the making of this blog :P

>In case you may get confused:
>
>Spells - Files
>
>Incantations - Commands
>
>Records/Magic Book - Repository

Hello there! I am your teacher at the School of Terminal Wizardry and I will be teaching you Git Magic. 
Terminals are all around us. Terminal Wizards are the ones who have the power to manipulate terminals for their own use. 
Git Magic was derived from the theory of [version control][what-is-version-control].

I will now give you an overview of Git Magic Incantations
This first incantation is for initiation of git magic in your own magic book. 

`git init`

_When used in the terminal with git installed, this incantation forces it to serve your version control demands by initiating a new magic book._

```bash
:~/magic-book$ git init
Initialized empty Git repository in /home/magic-book/.git/

```
And so your journey of git magic manipulation begins. . . 

## Getting Started

When you first create your magic book, it is empty. However, you can add new spells and other magic upon it. 
The adding incantation makes the git magic track changes in your spells as well prepare them for engraving. 

You can see which all spells are being modified or are untracked, the commits so far, as well as the current branch, using this command:

`git status`

_This incantation allows the user to see the status of the repository_

With so much info provided by this incantation, this will be the spell most used by you. 

```bash
:~/magic-book$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   basic-spell.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	basic-spell-multiple.txt
```

You can add spells to your book using this incantation: 

`git add <spell-name>`

_This incantation allows the user to add a new magic spell to the repository_

In case you want to add multiple spells to your magic book, you can use this command:
 
`git add - A` 

_This incantation allows the user to add all the magic spells to the repository_

In case you have added a spell by mistake and want to remove it,  you can use this command:

`git rm -r` 

_This incantation allows the user to remove added magic spells to the repository_

To engrave these spells onto your magic book, you can use this command:

`git commit -m [“Message Text”]`

_This incantation allows the user to commit the magic spells added earlier to the repository_

You also need to add a text along with the commit incantation.
Written in that text, should be the reasoning behind adding that change or a new spell, so that you remember it when you open your magic book again. 
(there are too many spells to work on these days :P)

You should always write good commit messages.Don't know how? Try this [link][git-commit-link]

These are all the basic commands. The following command is a powerful one. 

`git clone ssh://git@github.com/username/repository-name.git`

_This incantation allows you to copy someone else’s magic book into your own magic book and make changes within your book_
(great incantation to have, right? XP)

This command is widely used by practicing wizards. Due to this, any terminal wizard can use the cloning spell and work upon the book without starting from scratch.

Now, onto the next part. . . 

## Branching Up
There can be multiple types of magic spells in a magic book. 
However, instead of creating a new magic book for specialized spells of each type, we can use the same one again by a skill called branching.
Branching is also used when you are experimenting on a spell improvement but don't want the current spell to break (think of it as the last page you use for rough work :P)

![alt text][branch-gif]

`git branch <branch-name>`

_This git incantation allows the user to create another branch of the current magic book_

```bash
:~/magic-book$ git branch 
  fire-spell
  ice-spell
* master
```
Want to delete a branch that you made? No problem,use this incantation: 

`git branch -d <branch-name>`

_This git incantation allows the user to create another branch of the current magic book_

```bash
:~/magic-book$ git branch -d ice-spell
```
To shift from one branch to another, when working on different spells,use this:
 
`git checkout <branch-name>`

_This incantation allows us to switch a branch within the repository._

```bash
:~/magic-book$ git checkout fire-spell
:~/magic-book$ git branch
* fire-spell
  master
```

`git checkout -b <branch-name>`
 
_This git incantation allows us to both create another branch within the repository and switch to it._ 

```bash
:~/magic-book$ git checkout -b ice-spell
:~/magic-book$ git branch
  fire-spell
* ice-spell
  master
```
Now, if you were using it for experimenting on your spell and the change works, then you can add the changes to the book by this incantation:

`git merge <source-branch> [target-branch]`

_Allows a wizard to merge a the source branch into the target branch.If the target branch is not mentioned, then the branch is merged into the active branch._

```bash
:~/magic-book$ git status
On branch master
nothing to commit, working tree clean

:~/magic-book$ git merge fire-spell
Updating 3515790..043b603
Fast-forward
 firespell.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

By this time, I am sure you would have done a lot of work on your spells.

Want to share your work? You'll need to create a remote copy of your magic book.
This remote copy can be made in any Git platform and allows other wizards to copy from this remote magic book using the git clone command we talked about earlier.

Next, we will learn more about sharing your magic book.

## Remote but Together

Remote magic books are very important part for terminal wizards. It allows us to copy other magic books as well as share ours.

Often, terminal wizards work together on powerful spells and creating new incantations.
They create projects within an organization, of which they are members.
So that they can combine their work, they clone a remote magic book created by them (the organization book) and work on their copy of that magic book, called origin.

To create this remote, the follwowing incantation must be invoked:

`git remote add <remote-name> <url>`

_Allow the user to create a remote (called origin by default) to the repository mentioned in the url_

After working on the spell, they add the updated work in their local magic book back to the remote one. This way others can now copy an updated remote book (amazing, isn't it?)

To update the organization book, you need to create another remote made by this incantation:

`git remote add upstream <url>`

_Allow the user to create a remote called upstream to the repository mentioned in the url_

![alt text][remote-img]

`git push origin master`

_This incantation pushes the spells present in the master branch(local copy) to origin (remote copy)_

`git push upstream master`

_This incantation pushes the spells present in master branch(local copy) to upstream (remote organization book in this case)_

Let's say your fellow wizards pushed the code before you and you want to see htier changes then you can use this invocation:
`git pull origin master`

_This incantation copies/pulls the spells present in the origin (remote copy) into the master branch(local copy)_

`git push upstream master`

_This incantation copies/pulls the spells present in upstream (remote organization book in this case) to master branch (local copy)_
 
There is another use of it. You can pull the copy of remote book in case you want to work on your spells and don't have your magic book around.

Ancient terminal wizards have always documented their research on spells in their magic books.
After using the git clone incantation, we can see the whole research process. 
This includes the wizards who contributed as well as the reasoning behind each and every change using this command: 

`git log [--flags]`

_Allows the user to see the changes made by in the magic book with the most recent changes at the top_

git log is a very powerful command and provides a lot of data.To make it easier for fellow wizards to look for the required data, 
there are many flags which can be added after the git log incantation :

`--summary`
Allows user to view changes in a detailed manner

`--author <author-name>`
Allows the user to see the changes made in the magic book by a specific wizard.

`--since`
Allows the user to see the changes made to the magic book since a given time or date-time

Now, so that the remote book doesn't get corrupted, each change is submitted as a request which must be accepted by the maker of that book. 
Sometimes the book is maintained by more than one wizard. 

Now let's say you are the one receiving the request, and you want to see what changes have been made.You can see that using this incantation: 

`git diff <source branch> <target branch>`

_Allows the user to preview changes before merging_

```bash
~/magic-book$ git diff fire-spell master
diff --git a/firespell.txt b/firespell.txt
index 46e039b..469f750 100644
--- a/firespell.txt
+++ b/firespell.txt
@@ -1 +1 @@
-Flames of Heaven!
+Flame!
```
That's it for the overview! (you forgot it was an overview, didn't you? XD)

Git Magic is much more vast and has lots of features for very specialized uses. 
Keep learning and aim to be a better terminal wizard.

[what-is-version-control]: https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
[git-commit-link]: https://chris.beams.io/posts/git-commit/
[branch-gif]: https://github.com/AbhayKaushik/AbhayKaushik.github.io/tree/master/images/git-branching.gif
[remote-img]: https://github.com/AbhayKaushik/AbhayKaushik.github.io/tree/master/images/git-remote.png


