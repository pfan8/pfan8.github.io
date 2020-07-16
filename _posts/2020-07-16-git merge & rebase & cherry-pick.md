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

Since I come to a place where we need to speak English everyday, I wanna have a try to post this blog with this Language, it seems intersting and challenging, even for the future, maybe we can see a Janpanese blog too!!! =w= this idea came into my mind just now, but few seconds later I realize that's gonna be a long way to go, however, nobody knows future except god. Ok, talk a load of garbage, let's dig into Git flow!

# Team workflow

In order to be clear to process of Git (or other version control tools), we need to take a landscape for team workflow, which will lift you up from concrete git command whenever you get confused with them.

There are several workflows desgined by company managers who wants to make their team collaborate better, and the main ideas of different workflows will cause different solutions under conflict situation, I will talk this later. Actually, GitFlow is the most popular and worldwidely used workflow for team work, which works in my team.

Gitflow Workflow is a Git workflow design that was first published and made popular by Vincent Driessen at nvie. The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects.

What I understand this workflow is that we make three type branches which will make managering different parts of code from different team members, they can take own's work finished seperately and merged them togather easily. The main idea is to check carefully and log commit history made by every member, thus problem can be positioned and fixed faster. 

The next part is to introduce these 3 branches (`master`, `develop`, `feature`), once you fully understand the reason for seperating 3 branches and even high level design thought, it's impossible for you to make mistake on git command. in fact, only a few patience you need to take to study this, then you will find the git world is open for you.

# Git flow

//TODO

Then we can dig into git command `merge`,`rebase` and `cherry-pick`, they are all used to resolve conflict situation, although small difference here, you need to identify scenario 

# Command to resolve conflict

## merge

## rebase

## cherry-pick