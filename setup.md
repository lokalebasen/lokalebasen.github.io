---
layout: setup
---
Git
===

Installation
------------

    brew install git

Configuration
-------------

Setup name and email:

    git config --global user.name "Jacob Atzen"
    git config --global user.email "jacob@incremental.dk"

Configure some handy aliases:

    git config --global alias.ci "commit -v"
    git config --global alias.st "status -sb"
    git config --global alias.br "branch"
    git config --global alias.co "checkout"
    git config --global alias.ru "remote update"
    git config --global alias.ap "add -p"

Make it pretty:

    git config --global color.status auto
    git config --global color.diff auto
    git config --global color.branch auto

Only push current branch:

    git config --global push.default simple

Pulling from master
-------------------

You will need to add the main repository as a remote:

    git remote add upstream git@github.com:lokalebasen/lokalebasen.git

Then to pull from master (when on your master branch) either do:

    git pull upstream master

Or set the master branch to always use this remote:

    git config branch.master.remote upstream
    git config branch.master.merge refs/heads/master

You only need to do this once, afterwards you will be able to pull from master
by just using:

    git pull

Further reading
---------------

To dive further into git checkout the [Pro Git](http://git-scm.com/book/)
book.

ZSH
===

Installation
------------

    brew install zsh

Configuration
-------------

Get oh-my-zsh:

    curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

Peek in the plugins dir to see what is available:

    ls ~/.oh-my-zsh/plugins

Edit .zshrc:

    $EDITOR ~/.zshrc
