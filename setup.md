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
