git-publish-pages
=================

About
-----

Script to generate and deploy (publish) Jekyll site to Github Pages.

Usage
-----

First create remote branch 'gh-pages' manually and then use in
place you have a Jekyll site in your repository:

    git publish
    
This invocation is equal to:
    
    git publish --site-dir _site --gh-branch gh-pages --message "Built from branch:latest_revision"
    
See *Motivation* and *Under the hood* sections for more details.
    
Motivation
----------

Jekyll on Github Pages have the following problems:

* no support for plugins
* no support for categories and tags
* it's not possible to setup Github flavored markdown with pygments
* old version of packages and markup engines

Fortunately user is not limited in using Jekyll and building page
on server, page can be built locally and sent to the github. This
is not an easy process, you need to have two separate branches, one
with source and one with static page, called gh-pages.

This script makes things easy. See *Under the hood* section to
find out what/how.

Under the hood
--------------
    
This script tries to:

* clone existing single branch from origin, by default gh-pages
** just once, already existing repo is reused
** it's a fake submodule, where subrepository is just
a different branch
* build jekyll site
** in a temporary directory, so it can not delete .git
** result is copied to site directory, by default _site
* add all changes to one commit
* push commit to origin gh-pages

Installation
------------

Download stuff to bin folder, in this case /usr/local/bin:

    sudo wget https://raw.github.com/prost87/git-publish-pages/master/git-publish-pages --output-document /usr/local/bin/git-publish-pages
    
Change execute permission:
    
    sudo chmod ugo+x /usr/local/bin/git-publish-pages
    
Make git alias, so you can use completition: ```git pub<tab>```.
Note that completition of options and ```--help``` command with alias are not supported.
Instead of ```--help``` use ```-h```.

    git config --global alias.publish '!sh -c "/usr/local/bin/git-publish-pages $*"'
    
Creation of branch gh-pages
---------------------------

First create local branch without any parent.

    git checkout --orphan gh-pages
    
Then delete local content (it's the stuff from previous branch).
    
    git rm -rf .
    
Create an empty commit.
    
    git commit --allow-empty -m 'Initialized empty gh-pages branch'
    
Push it to remote server.
    
    git push origin gh-pages

Now back to the branch master.
    
    git checkout master