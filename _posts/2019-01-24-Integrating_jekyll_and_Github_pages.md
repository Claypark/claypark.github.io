---
title: "Integrating jekyll and Github pages."
date: 2019-01-24 00:05:28 +0900
categories: Jekyll
tags:
- Jekyll
- Github
---


  **Jekyll** is generator which convert text to static page. So, you can make site easily by using Jekyll. But you have some problem about server. It is difficult to operate server for 24 hours and config for connect to external network. So, there is a good solution to solve this problem. *github pages.*
  
  **Github pages** is feature that makes website in user's repository. you can easily make a website by typing some text such as *username.github.io* in the title when you create repository. It is no problem about keep operating your server because it is managed all by github. you don't worry about turning on your local server. now, let's make your page.
  
  # Create Repository
 
 First, connect to *github.com*. after sign in, you can find **New repository** button. you can see *Repository name* then you put *username.github.io*.
 ![New repository](/assets/images/post/2019-01-24-create_repository.PNG)
 
 # Initialize Repository
 
 Next, there is the repository main page. and you can see some commands for initializing repository. 
 ![Repo Home](/assets/images/post/2019-01-24-repository_home.PNG)
 
 In terminal, you just type those. then, you can see the readme file which has big title.
 ![After git init](/assets/images/post/2019-01-24-after_git_init.PNG)
 
 # Copy config.yml to your repository
 
 It has many open sources related to jekyll. We'll choose one of source. by searching Jekyll in github. In my case, I chose *minimal-mistakes* source. 
 ![minimal-mistake](/assets/images/post/2019-01-24-minimal-mistakes.PNG)
 
 In the repository, you can find *_config.yml* file. copy to your repository.
 ![config.yml](/assets/images/post/2019-01-24-config_yml.PNG)
 
 # Create index.html
 
 And you have to create *index.html* for showing your first page. In default, type this text.
 
```
---
layout: home
author_profile: true
---
```

 Good job! From now on, you can connect your site that url is ***username.github.io***.
 
 
 ## References
 
 * [minimal-mistakes repository](https://github.com/mmistakes/minimal-mistakes)
 * [configuration guide](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#)
 * [minimal-mistakes docs](https://github.com/mmistakes/minimal-mistakes/tree/master/docs/_docs)
 
