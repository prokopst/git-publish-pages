git-publish-pages
=================

About
-----

Makes easier to generate and publish (deploy) Github Pages.

Just use:

    git publish
    
This invocation is equal to:
    
    git publish --site-dir _site --gh-branch gh-pages --message "Built from branch:latest_revision"

Under the hood
--------------
    
This script tries to:

* clone single branch from origin, by default gh-pages
** just once, already existing repo is reused
* build jekyll site
* add all changes to one commit
* push commit to origin gh-pages

Installation
------------

Download stuff to bin folder, in this case /usr/local/bin:

    sudo wget https://raw.github.com/prost87/git-publish-pages/master/git-publish-pages --output-document /usr/local/bin/git-publish-pages
    
Change execute permission:
    
    sudo chmod ugo+x /usr/local/bin/git-publish-pages
    
Make git alias, so you can use completition: ```git pub<tab>```.
Note that completition of options and --help command with alias are not supported.
Instead of ```--help``` use ```-h```.

    git config --global alias.publish '!sh -c "/usr/local/bin/git-publish-pages $*"'