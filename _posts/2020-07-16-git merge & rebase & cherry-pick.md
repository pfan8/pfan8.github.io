---
layout:     post   				    # 使用的布局（不需要改）
title:      Git merge/rebase/cherry-pick 	# 标题 
subtitle:   How to fix conflict correctly			#副标题
date:       2020-07-16  			# 时间
author:     pfan8 						# 作者
header-img: img/post-bg-github-cup.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - git
---
# Preface

Since I come to a place where I need to speak English everyday, I wanna have a try to post this blog with this Language, it seems intersting and challenging, even for the future, maybe we can see a Janpanese blog too!!! =w= this idea came into my mind just now, but few seconds later I realize that's gonna be a long way to go, however, nobody knows future except god. Ok, talk a load of garbage, let's dig into Git flow!

# Team workflow

In order to be clear to process of Git (or other version control tools), we need to take a landscape for team workflow, which will lift you up from concrete git command whenever you get confused with them.

There are several workflows desgined by company managers who wants to make their team collaborate better, and the main ideas of different workflows will cause different solutions under conflict situation, I will talk this later. Actually, GitFlow is the most popular and worldwidely used workflow for team work, which works in my team.

Gitflow Workflow is a Git workflow design that was first published and made popular by Vincent Driessen at nvie. The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects.

What I understand this workflow is that we make three type branches which will make managering different parts of code from different team members, they can take own's work finished seperately and merged them togather easily. The main idea is to check carefully and log commit history made by every member, thus problem can be positioned and fixed faster. 

The next part is to introduce these 3 branches (`master`, `develop`, `feature`), once you fully understand the reason for seperating 3 branches and even high level design thought, it's impossible for you to make mistake on git command. in fact, only a few patience you need to take to study this, then you will find the git world is open for you.

# Git flow

## Master and Develop branches

once you constructing your product, you must make every version work well and there should be few bugs for users who will use your product, your released product need to be stable, useful, and even friendly to user, which means if you build a web site or app, you may use the most powerful server to run application and thus make it faster. This will make some diffs between your release production and develop production, the former is used to serve your customer, the latter is used to develop new things (which is called `feature`, we will use this term later).Actually, we call the former branch in Gitflow `master` branch, which must be reviewed and tested before we make a new function (called `push a new commit`) into it, thus we can get a cleaner and safer branch to build and take them to user. For example, you can test many test cases which usually won't happen, one of them is called `corner case`, such as a user sign up and cancel the account repeatly, this must be a rare case, but user can be upset if we cannot response to them correctly, even more, what if such action mess up our system and break other users? Yes, you may never see the actual situation, but I tend to think of it as a possibility model, you can imagine it like your interview, the more cases you coverd, the more possible for you to achieve it. I thinks this metaphor is quite accurate.

So, if you absord my words above, you will get what the picture here says: as for your `master` branch, there will be less but more stable commit, and on your `develop` branch, you can test more cases you wanna to check, it maybe a bug fix, or new feature, or backend/architecture's optimazation. **Make sure to sync develop branch with master branch once master branch push a new commit, only this way will make sence for Gitflow design.**

![](https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=1131)

one more thing to say, you can use version number to signature each commit, or some other way which you can track your commit action or history by this tag (such as date info in my company, this is decided by your company rules), in industry they usually use there parts of number, and make them to version number, for example

```
V 1.2.0
```
`V` means version, the first part `1` should be a baseline for your current production, if this part number changed, your must take a makeover to your product, which user can obviously feel. The second part `2` maybe several different develop flow, may be leaded by different team in big company, or just different aspect for your production, but it should also be quite a big change, and stable to use. The last part usually shows your new feature, you can let it to small part of your customer and get some feedback on these new features, therefore it may lead to bugs somehow, but worth. I believe the nightly version of some famous works such as VS-Code, Tensorflow, may work like this way. and you can also see them as that the first part of `1` means `master` branch, the second part of `2` means `develop` branch, the last `0` means `feature` branch. Of course, there are still some subtle difference between them, but you can get most part of it.

I don't want to say much to practice command and teach you step by step, because I believe the design idea/concept is a shorcut to mastering a skill/tool, once you get the idea, you can learn the related commands by yourself, it gonna be faster than the way I tell you them straightly, as long as the question is a consumption of the brain, this rule will always work, until now I don't miss it.

However, I will give several main commands for two reason:
1. log here for me if I forget them in the future
2. make this blog complete

So, back to the topic of branch, if you want to create `master` branch and `develop` branch, you may use the following commands: 

```sh
git branch # see all branches and HEAD info
git checkout master
git pull
git checkout -b develop
git push -u origin develop
```

When using the git-flow extension library, executing git flow init on an existing repo will create the develop branch:

```sh
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []

$ git branch
* develop
 master
```

## Feature branch

In Gitflow, what makes team work really work is `feature` branch, as I mentioned above, every unit task should be fullfilled in `feature` branch, which can be seperately coded by different member. Besides, one main advantage for `feature` branch is that we can easily backup specific commit which is completed by members who finished their test, other members can continue their work and wait for next commit on `develop` branch, thus to improve effciency of whole team work.

![](https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=1131)

In pracetice, team members usually code on their own feature branch and test on their local machine first, after first check, they can push feature branch to remote github repo and create a `pr`(pull request) which may need a reviewer in your team (usually your mentor or TM), after they approve code on your feature branch, the feature branch come to merge into develop branch, then test engineers or QA will test your function to check if these functions work well on test server, that's the second check. After this double-check, it should be safe enough to merge new code to master. To avoid some accidents, you can leave new develop branch a few days before merge into master branch, during the period your team member may use the test server and find some bugs which have not been found before, thus to make changes safer.



Then we can dig into git command `merge`,`rebase` and `cherry-pick`, they are all used to resolve conflict situation, although small difference here, you need to identify scenario 

# Command to resolve conflict

## merge

## rebase

## cherry-pick