---
layout: post
title:  "How I built my personal website"
date:   2017-07-22
author: Jared Johnson
---

Last weekend, I decided to build my own personal website and I thought it would be a helpful resource to document the steps that I took to get [jared-johnson.com](http://jared-johnson.com/) up and running.

### Hosting on Github Pages

I decided to set my website up using [GitHub Pages](https://pages.github.com/). For those who aren't familiar with GitHub, it's a [version control repository](https://en.wikipedia.org/wiki/GitHub) for code. What this means is that developers use it to preserve iterations of their projects and applications. It's a great tool and for those new to programming, I highly recommend checking it out.

Ok so what is GitHub Pages? GitHub offers a relatively easy way for users to host projects and personal websites to the web for free. And you're able to manage your website using the same workflow that you'll be familiar with from working with code projects on GitHub.

To start using GitHub Pages for your website, the first think you will need to do is [create a repository](https://github.com/new) with your GitHub username and the extension _'.github.io'_ -- it should look something like this:
> your-username.github.io

Once you have this repository set up, the only file you need to create your website something called _index.html_. I cloned my repository down locally and set my website up with it's own directory but if these words mean nothing to you, I would recommend downloading the [GitHub app](https://central.github.com/mac/latest) to interface with your website repo.

Using a text editor like [Atom](https://atom.io/), try typing _'it's my website'_ in your _index.html_ file and sending those changes up to GitHub using the code below if you're using the terminal, or by syncing your changes if you are using the GitHub app.

````
git add .
git commit -m "my first commit"
git push
````
Now go to your-username.github.io in your browser and you should see something like this!

![your very own website!](/assets/images/website1.png)

Your website is now live and you have the freedom to make it anything you want. Once I got to this point, I only partly felt satisfied. I have a functioning website but I have to type in the full _.github.io_ URL to access my site. Wouldn't it be cooler if I could pull my website up with a snappy _'.com'_ address? Well, you can be the judge of that but I knew my next step was to buy a domain.

### Buying and setting up my domain

First thing I did? High-tailed it to [GoDaddy.com](https://www.godaddy.com/). Dot com domain names can get pricey and I was lucky to find [jared-johnson.com](/) at an affordable price (Although I did opt to pay a premium to insert a dash between my name rather than purchasing [jaredjohnson.net](http://www.jaredjohnson.net) or [jaredjohnson.us](http://www.jaredjohnson.us)).

To get my GitHub site to be served to my fancy new domain name, I had to complete a few more steps. First, I had to let GitHub know that I was using a custom domain. In the 'settings' tab of your repository, you should find a box to enter a different URL (see below).

![ custom domain box](/assets/images/website2.png)

After letting GitHub know to serve your custom domain, you will need to let your DNS provider (GoDaddy in my case) know where to route your URL. I found a really helpful [blog post](https://medium.com/@kswanie21/how-to-set-up-godaddy-domain-with-github-pages-a9300366c7b) by Kristen Swanson that details the steps needed to set this up if you are also using GoDaddy.

### Building the site

As awesome as it is to own a URL on the internet that just says "it's my website," I knew that I wanted to use my site for blogging. By now, I know enough programming to build something from scratch that looks good but my experience has also taught me just how much work can go into maintaining something as simple as a blog. Drawing routes for all my posts, formatting my plain text and designing my site in plain HTML/CSS was starting to look like a part-time job. That was until I discovered [Jekyll](https://jekyllrb.com/).

Jekyll is a static-site generator built by one of the [co-founders](https://en.wikipedia.org/wiki/Tom_Preston-Werner) of GitHub. Ok but what is a static-site generator? This just means that Jekyll is an application that can render all of the pages of your website from plain text and a template. Jekyll uses [Markdown Syntax](https://daringfireball.net/projects/markdown/syntax), which is mostly plain text that renders to HTML, to tell your site what the contents of each page or post should be. It makes managing your site so much easier. With all of this said, understanding a little bit of HTML and CSS is extremely useful when using Jekyll, which I will demonstrate later.

Allow me to show you an example to better hammer home why this is so useful and then I'll discuss setting up Jekyll.

This is what the Markdown syntax looks like for my last blog post.

![markdown syntax for my post](/assets/images/website3.png)

And this where my blog post content is pulled into my HMTL file.

![html template](/assets/images/website4.png)

All of this is rendered to my site to display like this.

![blog post output](/assets/images/website5.png)

I didn't have to set up a database or write logic that tells my site how to deal with each individual post. Following the convention of Jekyll projects, I was able to get my post content rendered to my site in minutes. Pretty cool, right? Now let's discuss setting up Jekyll.

**Setup/Configuration**

Jekyll is a RubyGem. This means that, assuming you have a version of the [Ruby](http://www.ruby-lang.org/en/) programming language installed on your machine, Jekyll can be installed using the following commands.
````
gem install jekyll
jekyll new my-website
````
You should now have a new Jekyll project at 'my-website' on your computer. Since I already have a working site via my GitHub pages repository, I moved all of the files that Jekyll gave me into the same folder. Now is a good time to discuss what these files are.

**File Structure**

````
# from the Jekyll official documentation
.
├── _config.yml
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2017-07-02-quit-being-difficult.md
|   └── 2017-06-13-4-things-i-learned-toying-around-with-nested-resources-in-rails.md
├── _sass
|   └── _layout.scss
├── _site
└── index.html
````
For simplicity, I've pared down the file tree example from the official Jekyll documentation. The first file that you should edit is *_config.yml*, which is the configuration file that contains settings and variables that become available for use throughout your site.

In the *_layouts* folder is where your page templates are stored. I am currently only using two different templates for my site, one for blog posts -- _post.html_ -- and another for my home page called _default.html_. As I mentioned earlier, these templates are just HTML files that are populated with content from associated Markdown files (where you write your plain text). Content from your posts and variables defined in your *_config.yml* file will be available to these templates using double brackets.

New posts must follow a certain naming convention (see below) to be recognized by the Jekyll logic.
````
# post example in _posts folder
YYYY-MM-DD-title.md
````
The _'.md'_ here denotes Markdown syntax. Anything I write in these files is sent through my _post.html_ template and a ready-to-serve HTML file is generated in my *_site* folder. In the *_site* folder lies the magic of Jekyll. All of the HTML files, images and CSS/styling elements used in my website are copied over or generated in this folder. As you make changes to your '.md' files in your *_posts* folder, the accompanying HMTL file in the *_site* folder gets re-generated. With GitHub pages, the only thing I need to do after creating or editing a post is pushing my commits up to my repository. It's that easy -- No part-time job necessary.  

**Design/Layouts**

The last that I want to touch on is using themes in Jekyll. Pre-made themes make it really easy to spin up a site that looks great in minutes. If you initialize your Jekyll project using the 'jekyll new' command, your site will come with a default theme named [minima](https://github.com/jekyll/minima). While this theme looks great, I wanted something even more pared down and swapped the theme for one called [minimal](https://github.com/pages-themes/minimal).

Jekyll makes changing your theme extremely easy. In your _config.yml_ file, you can swap out your theme for a number of options available in the [RubyGems library](https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme). I narrowed my search by reviewing the list of themes [supported by GitHub Pages](https://pages.github.com/themes/). Each theme comes with it's own default template for pages, so I would recommend copying this over from the GitHub repository for your chosen theme.

I genuinely hope that this post has been helpful and that I've inspired you to create your own website. Don't hesitate to reach out to me [@yungpanko](https://twitter.com/yungpanko) if you have any questions about my experience.


## Additional resources:

1. [How to Set up GoDaddy Domain with GitHub Pages](https://medium.com/@kswanie21/how-to-set-up-godaddy-domain-with-github-pages-a9300366c7b)
2. [Jekyll Documentation](https://jekyllrb.com/docs/home/)
3. [YesWeJekyl Startup Guide](http://yeswejekyll.com/)
