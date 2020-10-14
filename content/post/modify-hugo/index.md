+++
author = "humanist"
title = "Modify Hugo Theme"
date = "2020-10-14"
description = "Making changes to a sample Hugo Theme - creating a blog"
tags = [
    "hugo",
    "themes",
]
categories = [
    "themes",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

This writeup gives insights on setting up a blog and modifying the sample Hugo theme - [Theme stack by Cai Jimmy]().
<!--more-->

whether it is creating a blog, portfolio website, company website etc, so many options exist. one 

You know how you have the pure delight of working on that feature, fixing the bug, writing that article. You are finally delighted to get it done. You quickly estimate, by 20minutes i should be done with this. 
An hour or two into the entire process you just know oh crap this will be a wishful game...lol.

So I'll share my experience with a bug setting up my blog with hugo.

i love hugo as static site generator. It can be simple to set up(compared to other options like a full blown dynamic site with db, backend)
It is highly performant, secure and flexible. The challenge is it can be a hassle setting for non-techies.

There are other [static site](https://jamstack.org/generators/) alternatives [here](https://jamstack.org/generators/).

Some facts worthwhile. When setting up a blog that is styled with sass/scss, hugo extended version is ideal over the basic hugo version. 
It provides support for sass/scss and postCSS. it also gives all the added functionality of the hugo basic version which includes but not limited to:
* Minification
* Image processing
* Fingerprinting integrity, etc 

Hugo is an open source static site generator created with Golang. To set up a website.

### Setting up project

1. [Install Hugo](https://gohugo.io/getting-started/installing/) 
```
snap install hugo --channel=extended
```

switch to the hugo extended version

```
snap refresh hugo --channel=extended
```
2. Using the Hugo CLI generate a directory (in this context, we'll call the site blog) and initialize git.
```
hugo new site blog

cd blog

git init
```



3. Fork this theme to your personal repository: https://github.com/CaiJimmy/hugo-theme-stack
eg. this is the URL to the theme after i forked it: https://github.com/jakazzy/hugo-theme-stack.git

4. Add the theme you forked to the site blog as a git submodule.
```
git submodule add https://github.com/jakazzy/hugo-theme-stack.git themes/stack
```
hugo generates a directory called blog and adds as theme, stack as a submodule.
The blog directory has the structure below
```
▸ archetypes /
▸ content /
▸ plugins /
▸ resources /
▸ themes /
▸ .gitmodules
 config.toml
```
5. In the blog site, open the stack folder located here blog/themes/stack. 
Copy the content folder and the config.toml file in the stack folder into the root of the project(blog folder).

6. Add the theme name to the site configuration file, config.toml.
```
echo 'theme = "stack"' >> config.toml
```
7. Run the hugo server with the command below and navigate to navigate to http://localhost:1313/  to view the site in the browser.
```
hugo server -D 
```

8. Open the .gitmodules file in the root of the project and ensure that both the path for the theme an the URL are correct
[submodule "themes/stack"]
	path = themes/stack
	url = https://github.com/jakazzy/hugo-theme-stack.git

ps. the URL should not use this 'git@github.com:jakazzy/human.git'


### Modifying the theme
9. Open the file with the styles, the variables.scss. It is located themes/stack/assets/scss
 and change the following color values of the variables: body-background, accent-color.
 ps. you can change any variable of your choice to any preferred color
 ```
 --body-background:#042c34;
 --accent-color: #a0750d;
 ```
10. Move to the stack folder
```
cd ../..
```
since there's a git submodule(the stack folder) in another git project(the blog/root folder). Always stage, commit and push any changes made in the git submodule before doing same again in the root of the project.
What do I mean?
```
cd into blog/themes/stack folder
git add .
git commit -m"Made changes to the blog background color"
git push
```

11. Move into the root of the project(blog) and stage, commit changes. If you have a remote repository, you can push your changes
```
cd ../..
git add .
git commit -m"Add initial changes to the project"
git remote add origin <Name of repository for the blog>
git push origin master
```

12. You are set up with your blog and can deploy to your preferred hosting platform such as netlify, vercel, etc.

If this article was helpful, do like it or leave a comment below with suggestions or feedback.
Thanks
