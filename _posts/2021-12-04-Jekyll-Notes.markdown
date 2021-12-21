---
layout: post
title:  Jekyll Notes
categories: jekyll
background: '/img/posts/numpy/cheetSheet1.png'
---

### Installation and launching the server
1. Install ruby   dev version and run 1,3 when ruby command prompt appear

2. open cmd and run command
> gem install jekyll bundler

3. run command in CMD to check version
> ruby -v
> jekyll -v

4. To create a new project  , go to the designated directory and run command
> jekyll new projectname

5. cd projectname

5. To run the server , ever first time
> bundle exec jekyll serve  
> from next time jekyll serve can work
> jekyll serve --livereload

6. To stop the server
> Cntrl + C

7. To clear terminal screen
> clear 


### how to host site in github
1. create a new repository, with out read me file. 
2. edit config.yml file and add your repository name in base URL.
3. keep the url filed empty
4. run git init , git add . , git commit -m "message", git add origin .
5. create a new branch called git checkout -b gh-pages
6. git push origin gh-pages
7. take the url from setting page.


### How to create post
1. when ever you want to include draft pages to your runnig site 
> jekyll serve --draft

7. Naming Convention for drafts
> Do not include date as prefix of file name  
> include date only when moving post to _post directory

8. Frontmatter
> front matter tell the jeykll server that it needs to do something
> it becomes part of url  
> title, date, cateogry comes as a part of url

### how to create structure of page
##### _layout 

##### _include

##### _SASS