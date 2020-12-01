---
title: "How to Hugo"
date: 2020-11-22T22:26:06+01:00
draft: false
tags:
  - hugo
---

Choosing the right blogging software can be quite tricky. After a first search tens of different options show up. Being a Python programmer I first tried some python based frameworks, namely pelican and nikolas. Although their was nothing wrong with them in the end I settled on hugo, which is also running the blog you are currently looking at. From a first glance hugo is fast, easy to set up and easy to tweak.

In this blog I will describe my learnings in using the platform in the hope that future users (myself included) might find it usefull. I'm sure to add many updates as I go along.

# Installation & setup
The easiest way to get started with Hugo is by just following the quickstart guide which you can find here: https://gohugo.io/getting-started/quick-start/. This will set you up with a small explanation on how to initialize your project, create a first post, pick a theme and how to check the resultant page locally.

## Making the basic layout
Hugo uses themes to change the layout of you webpage. You can easily tweak these to you liking, but for now I will just go with a premade one.
For my blog I want a basic landing page that shows the first few blogposts, want to be able to view an about me section and finally an archive showcasing all the old blogs. Sind this is pretty standard I can choose from tens of different layouts that achieve this goal. 

After trying a couple I went with a fairly minimalistic design: https://github.com/gizak/nofancy.

# Tweaking hugo to your liking 
Next step is to change the overall design to your liking. To do this we have to dive deeper into the themes and configuration.

A basic overview of how hugo is structured
https://www.sitepoint.com/premium/books/a-beginner-s-guide-to-creating-a-static-website-with-hugo/read/1

Summary of hugo templates: https://terrty.net/2018/15-hugo-framework-blog-themes/

# Hosting
https://github.com/ncruces/appengine-hosting

# Conclusion
In the end I don't think it really matters which platform you choose for building your blog. They are all really similar in structure and functionality. With Hugo you have a platform that is really flexible in function, fast and easy to use.