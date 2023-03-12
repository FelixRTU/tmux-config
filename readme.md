Tmux Configuration
=====================
Tmux configuration, that supercharges your [tmux](https://tmux.github.io/) and builds cozy and cool terminal environment.

![intro](https://user-images.githubusercontent.com/768858/33152741-ec5f1270-cfe6-11e7-9570-6d17330a83aa.gif)

Table of contents
-----------------

1. [Features](#features)
1. [Installation](#installation)
1. [General settings](#general-settings)
1. [Key bindings](#key-bindings)
1. [Status line](#status-line)
1. [Nested tmux sessions](#nested-tmux-sessions)
1. [Copy mode](#copy-mode)
1. [Clipboard integration](#clipboard-integration)
1. [Themes and customization](#themes-and-customization)
1. [iTerm2 and tmux integration](#iterm2-and-tmux-integration)

Features
---------

- "C-a" prefix instead of "C-b" (screen like)
- support for nested tmux sessions
- local vs remote specific session configuration
- scroll and copy mode improvements
- supercharged status line
- prompt to rename window/session right after it's created
- newly created windows and panes retain current working directory
- monitor windows for activity/silence
- highlight focused pane
- merge current session with existing one (move all windows)
- configurable visual theme/colors, with some elements borrowed from [Powerline](https://github.com/powerline/powerline)

**Status line widgets**:

- username and hostname, current date time
- visual indicator when you press `prefix`
- visual indicator when you're in `Copy` mode
- visual indicator when pane is zoomed
- toggle visibility of status line


Installation
-------------
Prerequisites:
- tmux >= "v2.4"


To install tmux-config:
```
$ git clone https://github.com/samoshkin/tmux-config.git
$ ./tmux-config/install.sh
```

`install.sh` script does following:
- copies files to `~/.tmux` directory
- symlink tmux config file at `~/.tmux.conf`, existing `~/.tmux.conf` will be backed up
- [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm) will be installed at default location `~/.tmux/plugins/tpm`, unless already presemt
- required tmux plugins will be installed

Finally, you can jump into a new tmux session:

```
$ tmux new
```


General settings
----------------
Windows and pane indexing starts from `1` rather than `0`. Scrollback history limit is set to `20000`. Automatic window renameing is turned off. Aggresive resizing is on. Message line display timeout is `1.5s`. 

256 color palette support is turned on, make sure that your parent terminal is configured propertly. See [here](https://unix.stackexchange.com/questions/1045/getting-256-colors-to-work-in-tmux) and [there](https://github.com/tmux/tmux/wiki/FAQ)

```
# parent terminal
$ echo $TERM
xterm-256color

# jump into a tmux session
$ tmux new
$ echo $TERM
screen-256color
```

Key bindings
-----------
So `~/.tmux.conf` overrides default key bindings for many action, to make them more reasonable, easy to recall and comforable to type.

Let's go through them. 

<table>
    <tr>
        <td nowrap><b>tmux key</b></td>
        <td><b>Description</b></td>
    </tr>
    <tr>
        <td nowrap><code>C-a</code></td>
        <td>Default prefix, used instead of "C-b". Same prefix is used in screen program, and it's easy to type. The only drawback of "C-a" is that underlying shell does not receive the keystroke to move to the beginning of the line.
        </td>
    </tr>
    <tr>
        <td nowrap><code>&lt;prefix&gt; C-e</code></td>
        <td>Open ~/.tmux.conf file in your $EDITOR</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-r</code></td>
        <td>Reload tmux configuration from ~/.tmux.conf file</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; r</code></td>
        <td>Rename current window</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; R</code></td>
        <td>Rename current session</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; "</code></td>
        <td>Split new pane horizontally</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; %</code></td>
        <td>Split new pane vertically</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; ←</code></td>
        <td>Select pane on the left</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; →</code></td>
        <td>Select pane on the right</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; ↑</code></td>
        <td>Select pane on the top</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; ↓</code></td>
        <td>Select pane on the bottom</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-←</code></td>
        <td>Resize pane to the left</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-→</code></td>
        <td>Resize pane to the right</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-↑</code></td>
        <td>Resize pane to the top</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-↓</code></td>
        <td>Resize pane to the bottom</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; n</code></td>
        <td>Move to next window</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; N</code></td>
        <td>Move to previous window</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; Tab</code></td>
        <td>Switch to most recently used window</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; L</code></td>
        <td>Link window from another session by entering target session and window reference</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; \</code></td>
        <td>Swap panes back and forth with 1st pane. When in main-horizontal or main-vertical layout, the main panel is always at index 1. This keybinding let you swap secondary pane with main one, and do the opposite.</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-o</code></td>
        <td>Swap current active pane with next one</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; z</code></td>
        <td>Toggle zoom for current pane</td>
    </td>
    <tr>
        <td><code>&lt;prefix&gt; x</code></td>
        <td>Kill current pane</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; X</code></td>
        <td>Kill current window</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-x</code></td>
        <td>Kill other windows but current one (with confirmation)</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; Q</code></td>
        <td>Kill current session (with confirmation)</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-u</code></td>
        <td>Move current window to another session by given name</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; d</code></td>
        <td>Detach from session</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; D</code></td>
        <td>Detach other clients except current one from session</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-s</code></td>
        <td>Toggle status bar visibility</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; m</code></td>
        <td>Monitor current window for activity</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; M</code></td>
        <td>Monitor current window for silence by entering silence period</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; F12</code></td>
        <td>Switch off all key binding and prefix hanling in current window. See "Nested sessions" paragraph for more info</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; S</code></td>
        <td>Create new session and ask for name</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; s</code></td>
        <td>List all sessions</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; c</code></td>
        <td>Create new window and ask for name</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; +</code></td>
        <td>Sync Panes</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; y</code></td>
        <td>Sync Panes</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; [</code></td>
        <td>Copy Mode</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; w</code></td>
        <td>copy</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; ]</code></td>
        <td>paste</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; p</code></td>
        <td>paste</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; C-p</code></td>
        <td>show all buffers (paste with p, delete with d)</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; y</code></td>
        <td>(requires xsel) yank commandline / selection (copy mode) to clipboard</td>
        <td>-</td>
    </tr>
    <tr>
        <td><code>&lt;prefix&gt; Y</code></td>
        <td>copy current pane current working directory to the clipboard / copy+paste selction to commandline (copy mode)</td>
        <td>-</td>
    </tr>
</table>



Status line
-----------

I've started with Powerline as a status line, but then realized it's too fat for my Macbook 15'' display, it hardly can fit all those fancy arrows, widgets and separators, so that I can only see one window "tab".

So I decide to make my feet wet, with the idea to keep it dense, and include essential widgets. Sometimes it tries to replicate OSX topbar (battery, date time).

Left part:
![status line left](https://user-images.githubusercontent.com/768858/33151594-59db6a8e-cfe1-11e7-8a36-476fe0b416b3.png)

Right part:
![status line right](https://user-images.githubusercontent.com/768858/33151608-6978de72-cfe1-11e7-829a-e303e31e8c16.png)

The left part contains only current session name.

Window tabs use Powerline arrows glyphs, so you need to install Powerline enabled font to make this work. See [Powerline docs](https://powerline.readthedocs.io/en/latest/installation.html#fonts-installation) for instructions and here is the [collection of patched fonts for powerline users](https://github.com/powerline/fonts)

The right part of status line consists of following components:

- username and hostname (invaluable when you SSH onto remote host)
- current date time
- visual indicator when you press prefix key: `[^A]`.
- visual indicator when pane is zoomed: `[Z]`

You might want to hide status bar using `<prefix> C-s` keybinding.


Nested tmux sessions
--------------------
When in outer session, simply press `F12` to toggle off all keybindings handling in outer session. Now work with inner session using the same keybinding scheme and same keyprefix. Press `F12` to turn on outer session back.

![nested sessions](https://user-images.githubusercontent.com/768858/33151636-84a0bab2-cfe1-11e7-9d5d-412525689c9b.gif)

You might notice that when key bindings are "OFF", special `[OFF]` visual indicator is shown in the status line, and status line changes its style (colored to gray).

###  Local and remote sessions

Remote session is detected by existence of `$SSH_CLIENT` variable. When session is remote, following changes are applied:
- status line is docked to bottom; so it does not stack with status line of local session

You can apply remote-specific settings by extending `~/.tmux/.tmux.remote.conf` file.

Themes and customization
------------------------

All colors related to theme are declared as variables. You can change them in `~/.tmux.conf`.

```
# This is a theme CONTRACT, you are required to define variables below
# Change values, but not remove/rename variables itself
color_dark="$color_black"
color_light="$color_white"
color_session_text="$color_blue"
color_status_text="colour245"
color_main="$color_orange"
color_secondary="$color_purple"
color_level_ok="$color_green"
color_level_warn="$color_yellow"
color_level_stress="$color_red"
color_window_off_indicator="colour088"
color_window_off_status_bg="colour238"
color_window_off_status_current_bg="colour254"
```

Note, that variables are not extracted to dedicated file, as it should be, because for some reasons, tmux does not see variable values after sourcing `theme.conf` file. Don't know why.
