# Base16 Shell
See the [Base16 repository](https://github.com/chriskempson/base16) for more information.
These scripts were built with [Base16 Builder PHP](https://github.com/chriskempson/base16-builder-php).

A shell script to change your shell's default ANSI colors but most importantly, colors 17 to 21 of your shell's 256 colorspace (if supported by your terminal). This script makes it possible to honor the original bright colors of your shell (e.g. bright green is still green and so on) while providing additional base16 colors to applications such as Vim.

![Base16 Shell](base16-shell.png)

## Use Cases

* You want to use a `*.256.*` variant of a Terminal theme designed to honor the original bright colors.
* You prefer to use a script instead of a terminal emulator theme to color your shell.
* You use this script to have different colorschemes appear on different SSH sessions.

## Installation

```shell
git clone https://github.com/chriskempson/base16-shell.git ~/.config/base16-shell
```

## Configuration

### Bash/ZSH

Add following lines to `~/.bashrc` or `~/.zshrc`:

```bash
# Base16 Shell
BASE16_SHELL="$HOME/.config/base16-shell/"
[ -n "$PS1" ] && \
    [ -s "$BASE16_SHELL/profile_helper.sh" ] && \
        source "$BASE16_SHELL/profile_helper.sh"
```

#### If you're using ZSH + plug

You won't need to do the `git clone` in the Installation section.
Add the following commands to your `~/.zshrc` instead:

```
# before `zplug load`
zplug chriskempson/base16-shell, from:github
```

### Fish

Add following lines to `~/.config/fish/config.fish`:

```fish
# Base16 Shell
if status --is-interactive
    set BASE16_SHELL "$HOME/.config/base16-shell/"
    source "$BASE16_SHELL/profile_helper.fish"
end
```

### Base16-Vim Users

the BASE16_THEME environment variable will set to your current colorscheme, you just need to add the following to your vimrc: i.e. (remove the base16colorspace line if not needed)

    if exists('$BASE16_THEME')
          \ && (!exists('g:colors_name') || g:colors_name != 'base16-$BASE16_THEME')
        let base16colorspace=256
        colorscheme base16-$BASE16_THEME
    endif

### tmux users

Add the following line to `~/.tmux.config` to passthrough color escape sequences.
(As of version 3.3 the passthrough of escape sequences is turned off by default)

```tmux
set -g allow-passthrough 1
```

## Usage

If you have just installed and configured base16_shell for the first time, open a new shell or reload the configurations for your current shell (e.g. `source ~/.bashrc`).

Apply themes in your shell by typing `base16_`, using your shell's autocomplete function show you the options, then executing the theme you want to try. The current theme will be saved at the symlink `~/.base16_theme`, and the profile_helper script (see Configuration section) will load the theme (e.g. when you next log in or manually `source` your shell config).

## Troubleshooting

Run the included **colortest** script and check that your colour assignments appear correct. If your teminal does not support the setting of colours in within the 256 colorspace (e.g. Apple Terminal), colours 17 to 21 will appear blue.

![setting 256 colourspace not supported](setting-256-colourspace-not-supported.png)

If **colortest** is run without any arguments e.g. `./colortest` the hex values shown will correspond to the default scheme. If you'd like to see the hex values for a particular scheme pass the file name of the theme as the arguement e.g. `./colortest base16-ocean.sh`.

### Inverted blacks and whites

This is the expected behaviour when using a light theme:
https://github.com/chriskempson/base16-shell/issues/150
