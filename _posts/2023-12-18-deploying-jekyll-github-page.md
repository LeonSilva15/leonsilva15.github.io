---
layout: post
title: Deploying Jekyll Github Page
date: 2023-12-18
---
This is my first time deploying a Github Page, so I decided to use Jekyll. Here's a list of points to remember.

## Installation
First, I had to download a more recent Ruby version, since I'm using MacOS I did it through Homebrew.
I wanted to be able to switch the Ruby version as needed so decided to use [RVM], which allows you to have multiple Ruby versions on your machine.

Here's how to download [RVM]
```sh
\curl -sSL https://get.rvm.io | bash
```

After downloading, we verify it using
```sh
rvm -v
```

We can see the full list of Ruby versions using
```sh
rvm list known
```

In order to install some Ruby verions we require to use openssl. We can install it using brew if not installed yet
```sh
brew install openssl@3.0
which openssl
```

This command will show us the location of openssl so we can use it the next command
```sh
rvm install ruby-3.2.1 -C --with-openssl-dir=/opt/homebrew/bin/openssl
```

Now we can see the version of Ruby that we requested
```sh
ruby -v
```

now using Gem (installed with Ruby) install Jekyll bundler
```sh
gem install jekyll bundler
```

We use the project scaffold with
```sh
jekyll new <my-project-name>
```

To build the project we use
```sh
bundle
```

And then deploy it using
```sh
jekyll serve
```

## Using external themes
I wanted to use an external theme because none of the [supported themes] by Github were what I was looking for, so I decided to use [jekyll-gitbook]

To make Github support external themes we need to use [jekyll-remote-theme]
1. Add the following to your Gemfile

  ```ruby
  gem "jekyll-remote-theme"
  ```

2. Add the following to your site's `_config.yml` to activate the plugin

  ```yml
  plugins:
    - jekyll-remote-theme
  ```

3. Add the following to your site's `_config.yml` to choose your theme

  ```yml
  remote_theme: sighingnow/jekyll-gitbook
  ```

## Deploying in Github Pages
Lastly to deploy in my Github Page I just had to follow the official [Github Page guide]

Some important points:
- The repo must be public if we want the free deployment
- The repo must be named as _\<your-user\>_.github.io

#### Some useful resources:
- [Install RVM in macOS (step by step)
](https://nrogap.medium.com/install-rvm-in-macos-step-by-step-d3b3c236953b)
- [Homebrew openssl@3.0](https://formulae.brew.sh/formula/openssl@3.0)
- [Ruby Version Manager (RVM)
](https://rvm.io/)
- [Creating a GitHub Pages site
](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [Adding a theme to your GitHub Pages site using Jekyll
](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)
- [Github Pages supported themes](https://pages.github.com/themes/)
- [Gitbook theme home page](http://jekyllthemes.org/themes/gitbook/)


[RVM]: https://rvm.io/
[supported themes]: https://pages.github.com/themes/
[jekyll-gitbook]: https://github.com/sighingnow/jekyll-gitbook
[jekyll-remote-theme]: https://github.com/benbalter/jekyll-remote-theme
[Github Page guide]: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site