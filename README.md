# dotfiles

Heavily inspired by https://github.com/andrew8088/dotfiles

## how it works 
At a high level, this dotfiles repo has one folder for each application that I want to configure:
```bash
❯ tree -L 1
.
├── README.md
├── alacritty
├── brew
├── git
├── mutt
├── nvim
├── scripts
├── tmux
└── zsh
```

And there is `scripts`, home to the install scripts.

Within each of these application directories live three types of files:

the actual config files
a install script
a `links.prop` file

## The Configuration (as seen in andrew8088/dotfiles)
The config files aren't much different from any other dotfiles repo you'll see out there (and honestly, there are better ones to look at). 
What I'm most pleased with in my current iteration, though, is the file naming pattern. 
In the past, I'd use file names like vimrc and zshrc ... which is pretty common, right?
My gripe though: most editors don't give you syntax highlighting by default, when your file has no extension. 
So now I'm using file names like rc.vim and rc.zsh, and get the syntax highlighting. 
Small change, big difference.

## The Links
we have the links.prop files, one per app dir. Looks something like this:

$DOTFILES/vim/rc.vim=$HOME/.vimrc
$DOTFILES/vim=$HOME/.vim
On the left, we have the source. On the right, we have the destination. This is just a simple way to codify the symlinks that need to be created to "install" these configs.
The `bootstrap.sh` script file will replace any environment variables in these lines, and then create the symlinks.

## The Local Stuff
The `bootstrap.sh` script also creates a file called `~/.env.sh`. By default, it includes a single line:

`export DOTFILES=/path/to/dotfiles`

This file is for any machine-specific configuration. Need to include API keys or other secrets as env vars, but don't want to commit them? Have extra paths or tools that you need to configure for a work machine? Yes and yes, as a matter of fact.

Then, we source `~/.env.sh` in the "root" `~/.zshrc`.

