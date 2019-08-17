---
layout: post
title:  "Creating a Pull Request"
date:   2019-08-17 13:47:30 +0530
categories: jekyll update
---

Pull requests are an essential part of contributing to Open Source.
Any change that you wish to add to the public repo (not owned by you) can only be done by sending a pull request to the owner of the repository.

Generally, changes are done to branches other than the master branch. Master branch is the one which has all the final stable work. 
If there is a topic branch relevant to your changes, then you should make a pull request on that branch. 

In case there isn't any such branch, you can create a new one for the topic you want to address. 
However, you must be the owner of the repository to make branches. Or, if the the repo belongs to an organization, you must be a member.In essence, a person with write permissions

If you are none of them, do not worry as then you can fork their repo instead of branching and then make changes to your fork.

After forking, you can clone your repository in your local computer and make the changes that you wish to add.
Make sure you read the contributing guidelines to understand how to submit the proposed changes.

```bash
$ git clone forked-repo-url
$ git add files-you-added-changes-to
$ git commit -m "Reason why you made these changes"
$ git push
```

Now that you have made the required changes to your fork, you are ready to make a pull request.

To make the pull request, just specify which branch you want to merge your changes and click the pull request option. 
![Pull Request][pr-img]

Add a message in the manner described in the contributing guidelines. If there is a pull request template, write the message accordingly. 

Write the message and then send the pull request. Your pull request will now show up on the pull requests section of the repo you forked.

Congratulations! You have sucessfully created your pull request.


[pr-img]: https://raw.githubusercontent.com/AbhayKaushik/AbhayKaushik.github.io/master/images/pull-request.png
