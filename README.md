# Dircolors

Color your `ls`, `tree`, and tab-completion output based on file and directory
names/extensions. Sets `LS_COLORS` env var in your shell via GNU `dircolors`
command to accomplish it. Then any commands and completions that use the
standard will use your specified colors.

Should support most any 256-color capable terminal, and supports several
shells, like Zsh, Bash, Fish, and even Nushell.

Coloring files/dirs is useful for:

- seeing important files stand out
- differentiating certain source files
- semi-hiding some unimportant temp or binary files
- supporting new file types that you might invent (languages, specs, etc)
- conventionalizing files that indicate problems/processing (`bug`, `core`, etc)

## Usage

You should be able to simple copy the `dir_colors` file to `~/.dir_colors`.

If that doesn't work, clone this repo:

```shell
cd ~/proj # or wherever you like
git clone https://github.com/MicahElliott/dircolors
cd
ln -s ~/proj/dircolors/dir_colors .dir_colors
```

And possibly needed: then put into `~/.zshrc` (or your equivalent RC file) the
setup and some important aliases to see colors:

```shell
export DIR_COLORS="$HOME/proj/dircolors/dir_colors"
if   [[ -e $DIR_COLORS ]]
then eval "$(TERM=xterm dircolors -b $DIR_COLORS)"
else echo "Could not find dir_colors color-code file: $DIR_COLORS"
fi
```

To enable the colors for particular commands:

```shell
alias ls='ls -F --color=auto'
alias l='ls -hlkABFX' # optional
alias t='tree -C --charset utf8'
```

To enable colors for Zsh tab-completion:

```shell
zstyle ':completion:*:default' list-colors ${(s.:.)LS_COLORS}
```

Or, if using Nu:

```nushell
$env.LS_COLORS = (TERM=xterm dircolors -b ~/proj/dircolors/dir_colors )
```

## How it works

Running the command `dircolors` takes an input file of filename patterns.
These live in the provided `dir_colors` file, which you can edit to your
liking. The output of that `dircolors` run looks like this:

```shell
LS_COLORS='no=00:fi=00:di=01;34:ln=01;36:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.jpg=01;35:*.png=01;35:*.gif=01;35:*.bmp=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:...'
```

The default colors in your system likely come from `/etc/DIR_COLORS`, which
looks a lot like this project's `dir_colors` file — not a coincidence!

The color codes used to specify colors and effects are quirky/arcane.
Resources for understanding these ANSI color codes:

- [Wikipedia](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)
- [Stackoverflow](https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences)
- [Gist](https://gist.github.com/fnky/458719343aabd01cfb17a3a4f7296797#256-colors)
- `man 5 dir_colors`

## Customization

This is something of a starter kit that you can use to create your preferred
colors.

There is a script here that lets you iterate quickly on trying new colors. Use
it as such:

```shell
% ~/proj/dircolors/test-dircolors
I’m now creating a bunch of temp files for you to look at.

This test is mostly manual, but does create test files for you.
Here’s the test cycle:

 1. Edit your $DIR_COLORS file, or ~/.dircolors.
 2. Run this to update visible colors: eval $(TERM=xterm dircolors -b $DIR_COLORS)
 3. Do a colored ls on ~/tmp/test-dircolors
 4. Rinse and repeat until you’re happy with scheme.

Do this when you’re done: rm -rf /home/mde/tmp/test-dircolors.
```

## History

This started as something I loved and used in ~2002. I eventually turned it
into [a gist](https://gist.github.com/MicahElliott/719653). Then I figured
it'd be better as a first-class repo project, so here it is.

## Alternatives

Since my inception of this dircolors approach, other similar endeavors have
surfaced. AFAIK, the most well-known is
[LS_COLORS](https://github.com/trapd00r/LS_COLORS).

Other alternatives really reinvent the wheel when it comes to colors, so I
personally recommend sticking to the widely used/supported GNU `dircolors`
approach.

That said, there are other popular implementations of `ls` that have their own
handling of colors: [eza](https://github.com/eza-community/eza) and
[lsd](https://github.com/lsd-rs/lsd).

[colorls](https://github.com/athityakumar/colorls), a Ruby project, aims to add
colors (and icons) in a different way.

Emacs’ `dired` and family have their own way of coloring files/dirs.
