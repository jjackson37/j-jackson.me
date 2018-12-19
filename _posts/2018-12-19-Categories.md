---
layout: post
title: "Categories"
categories: Jekyll-Site
permalink: "/category/jekyll-site/categories/"
---
Hi, welcome to my first actual post about a project! This is the first post of a series about the development of this website, this post will be about the implmentation of categories into the site. I wanted categories in my site to make it easier to keep track of posts related to certain projects.

### Not using the Jekyll built-in?

Now, if you've looked at [the code](https://github.com/jjackson37/j-jackson.me) for my site you may have noticed that I'm not actually using the [categories built-in implementation](https://jekyllrb.com/docs/posts/#displaying-post-categories-or-tags) that Jekyll comes with.
The reason for this: it pretty much didn't do everything that I wanted without the use of plug-ins. A key feature I wanted was a page for each category that could list all the posts for it. I did at first attempt using this way but I won't get into that.

### Custom collections

So to implement a way I could show a page per category I resorted to creating a custom collection, main reasoning is that using a custom collection you can tell Jekyll to create a page per entry of said collection. You can do this in the config like so :
```yml
collections:
  category:
    output: true
defaults:
  -
    scope:
      path: ""
      type: category
    values:
      layout: "category"
```
To run through what this says, basically the 'collections' section defines my collection and says to output each one as a page. The 'defaults' section sets the default page layout for each page that's created for it.

### Creating the pages

Now that the custom collection has been created we need to create the layout it's referencing in the config. In my layout I call the `site.categories` (Yeah I kinda used the Jekyll built-in and lied a bit earlier) and pass in a Front Matter in order to get all posts of the current category. <br> Something like this : `for post in site.categories[page.tag]`. I also create another page which displays all the category pages for selection, this is done virtually the same as the individual category pages but just going through `site.categories` instead.

### Creating a category

To create a category I need to create a _category folder, this is just the standard way of storing any category entries. I then create a category in it like 'Jekyll-Site.md', in this Markdown file I'm going to put all the Front Matter that I need :
```
---
tag: Jekyll-Site
permalink: "/category/jekyll-site/"
name: "Jekyll Site"
description: "Creation of blog site to track project progress. Created using Jekyll and AWS."
---
```
tag is used for category page to retrieve all the posts for that category (you can see that in the previous section), permalink is used for the links to the page, name is used on the category page and on links to it, description is used the same as the name.

### To close

I think I've covered all of what I've done for the categories, next time I'm going to take notes whilst I go... Admittedly this, like most code, was mostly stolen patches of code that I gathered and twisted for my needs. Below I'm going to list the sources I used during this, see ya!
- [Jekyll official post on categories and tags](https://jekyllrb.com/docs/posts/#displaying-post-categories-or-tags)
- [Jekyll official post on collections](https://jekyllrb.com/docs/collections/)
- [Nice beginner friendly guide to collections](https://alligator.io/jekyll/collections/)
- [Creating category pages without plugins (The original implemntation)](https://kylewbanks.com/blog/creating-category-pages-in-jekyll-without-plugins)