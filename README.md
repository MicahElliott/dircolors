# Dircolors

Color your `ls` and `tree` output based on file and directory
names/extensions.

Should support most any 256-color capable terminal.

## Usage

Clone this repo. In my case this is:

```shell
cd ~/proj
git clone https://github.com/MicahElliott/dircolors
```

Then put into your `~/.zshrc` or equivalent:

```shell
export DIR_COLORS="$HOME/proj/dircolors/dir_colors"
eval "$(TERM=xterm dircolors -b $DIR_COLORS)"
```

## Customization

This is something of a starter kit that you can use to create your preferred
colors.

There is a script here that lets you iterate quickly on trying new colors. Use
it as such:

```shell
% test-dircolors
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
into a gist. Then I figured it'd be better as a first-class repo project, so
here it is. Since then, other similar things have surfaced. AFAIK, the most
well-known is [LS_COLORS](https://github.com/trapd00r/LS_COLORS).
