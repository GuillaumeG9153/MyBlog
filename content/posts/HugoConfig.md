+++
title = "Hugo and Unity Set-Up"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

# Hugo Set-Up

## Hugo
I've chosen Hugo to create my blog since it was the proposed tool on our firt lab, I also took Hugo for its simplicity to deploy and configure and I wanted something more technical than a "wordpress" like web editor in order to train myself.

## Deployment

I deployed my blog thanks to Github since it's a powerfull and a widely used tool. 

## What I did ?

Then I chose a minimalist template as you can see because I wanted to keep my blog simple.

However I had several issues particularly with images. As you will see in the following posts, I I did not succeed center and resize my images.

Moreover, in my md files I had to change the path of my images from /image_path to /MyBlog/image_path

The advantage of my template is that it was easy to configure since on the Github I found it, the config.toml was given. 

```js
baseurl = "https://guillaumeg9153.github.io/MyBlog"
languageCode = "en-us"
theme = "terminal"
paginate = 5
publishDir = "docs"

[params]
  # dir name of your main content (default is `content/posts`).
  # the list of set content will show up on your index page (baseurl).
  #posts
  contentTypeName = "posts"

  # ["orange", "blue", "red", "green", "pink"]
  themeColor = "red"

  # if you set this to 0, only submenu trigger will be visible
  showMenuItems = 2

  # show selector to switch language
  showLanguageSelector = false

  # set theme to full screen width
  fullWidthTheme = false

  # center theme with default width
  centerTheme = true

  # set a custom favicon (default is a `themeColor` square)
  # favicon = "favicon.ico"

  # set post to show the last updated
  # If you use git, you can set `enableGitInfo` to `true` and then post will automatically get the last updated
  showLastUpdated = false
  # Provide a string as a prefix for the last update date. By default, it looks like this: 2020-xx-xx [Updated: 2020-xx-xx] :: Author
  # updatedDatePrefix = "Updated"

  # set all headings to their default size (depending on browser settings)
  # it's set to `true` by default
  # oneHeadingSize = false

[params.twitter]
  # set Twitter handles for Twitter cards
  # see https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started#card-and-content-attribution
  # do not include @
  creator = ""
  site = ""

[languages]
  [languages.en]
    languageName = "English"
    title = "Guillaume Grandineau Blog"
    subtitle = "A simple, retro theme for Hugo"
    owner = ""
    keywords = ""
    copyright = ""
    menuMore = "Show more"
    readMore = "Read more"
    readOtherPosts = "Read other posts"
    missingContentMessage = "Page not found..."
    missingBackButtonLabel = "Back to home page"

    [languages.en.params.logo]
      logoText = "Guillaume Grandineau blog"
      logoHomeLink = "https://guillaumeg9153.github.io/MyBlog"

    [languages.en.menu]
      #[[languages.en.menu.main]]
      # identifier = "about"
      # name = "About"
      # url = "/about"
      # [[languages.en.menu.main]]
      #  identifier = "showcase"
      # name = "Showcase"
      # url = "/showcase"
	  

```

# Unity Set-Up

When we did the first lab I already knew how to start a Unity project so I didn't have issues.

I encourage you parcouring the next labs to know more about my Unity journey, I also added a post concerning my Unity game.


**So I hope you will appreciate my blog and its content, see you !**