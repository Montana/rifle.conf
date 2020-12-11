# Montana's rifle.conf 

My customized/personal rifle.conf (customized for macOS) for ranger. Ranger is a console file manager with `VI` key bindings.

## Ranger installation on macOS 

You need some prerequisites before you can successfully install `ranger`. Grab `homebrew` via the following: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null
```

Then run: 

```bash
brew install ranger
ranger --copy-config=all
```

You can now open `ranger` by simply running `ranger` in the terminal like so: 

```bash
ranger
```

## Getting started 

To use my `rifle.conf` you can start by cloning it via: `git clone https://www.github.com/Montana/rifle.conf`. Once you've cloned it, open the `rifle.conf` with your editor of choice, in this markdown though I'll be using Vim. 

```bash
vim ~/.config/ranger/rifle.conf
```

The `rifle.conf` is structured as so, each line provides a set of conditions separated by commas (`,`) e.g. `ext mp3`, followed by an equals `=`, then a terminal command, e.g. vlc `$@`. When Ranger is asked to open a file, it cycles through every line from top to bottom until it finds a line where all the conditions are met, you can logically think of this like `grep`, Ranger then, runs the terminal command. This means that the top-most line where all the conditions are met will be run. Using this logic you can construct a `rifle.conf` that works on different systems, (e.g. Linux, macOS), that is, f you order potential applications from most to least preferred.

![Ranger](ranger.png)

## Using `commands`

Most if not all Linux applications can simply be opened by typing their name into the terminal, optionally followed by a file to open and various rules, flags, and conditionals, e.g. `zathura example.pdf`. In macOS however, typing the equivalent `preview example.pdf` just returns an error that preview has not been found. The same goes for `Preview`, `preview.app` and `Preview.app`.

Instead, on macOS, the best way I found to call an application from the command line (specifically as it pertains to ranger) is to use `open`.

The following lines all open `Preview.app`:

```bash
open -a preview
open -a preview.app
open -a Preview
open -a Preview.app
```

So let's say I had a `pdf` named `Montana.pdf`, just add it:

```bash
open -a Montana.pdf
```
This same syntax can be applied to `rifle.conf` to open specific apps for specific file types with Ranger. The simplest condition to use is the file extension (`ext`). So the following conditional would work: 

```bash
ext pdf = open -a preview "$@"
``` 

## Calling `finder` 

For my `rifle.conf` when adding this keybinding to `~/.config/ranger/rc.conf`, this will allow you to open Finder on the highlighted file with %:

```bash
map % shell open -R %f
```

## Structure hierarchy

Try and split up your `rifle.conf`. You'll see I did this, it will help for you not to get mixed up. Here's a quick example using `Text files`: 

```bash
#-------------------------------------------
# Text files
#-------------------------------------------
ext xml|json|tex|py|pl|rb|js|sh|php|m[ark]d[own]|txt = vim "$@"
mime ^text = vim "$@"
```
