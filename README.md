# The n00b's guide to bspwm (with XFCE)...

If you are interested in tiling WM's but you're also an id10t (like me) the following guide below will walk you through setting up the best (imho) tiling WM ( **bspwm** ) to run alongside XFCE. This setup is nice for n00b id10ts because it grants you all of the great features of a tiling WM without having to sacrifice the conveniences of a DE (in this case, XFCE).

I've written this guide from the perspective of a user running Arch Linux (because that's the distro that I run and it's the best Linux distro around ;] ). However, these instructions should be applicable to any system running XFCE, regardless of the distribution.

I **heavily** referenced this [guide](http://feeblenerd.blogspot.com/2015/11/pretty-i3-with-xfce.html) as I was getting this setup to work, substituting bspwm with i3, of course. This guide is a great resource, I had to make a few variations (outlined below) but this is a nice template to work off of when trying out different WM's under XFCE.

**Table of Contents**
- [[OPTIONAL] Create new user: xfcebspwm](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#optional-create-new-user-xfcebspwm)
- [Install bspwm, sxhkd, compton, and [OPTIONAL] rofi | Make directories | Copy Dots](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#install-bspwm-sxhkd-compton-and-optional-rofi--make-directories--copy-dots)
- [Deactivate xfwm4](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#deactivate-xfwm4)
- [Remove XFCE hotkeys](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#remove-xfce-hotkeys)
- [Autostart required applications in XFCE](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#autostart-required-applications-in-xfce)
- [Dotfile notes](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#dotfile-notes)
- [Additional notes](https://github.com/bgdawes/bspwm-xfce-dotfiles/wiki#additional-notes)


## [OPTIONAL] Create new user: xfcebspwm


You may or may not want to do this step. If you've got a good setup already, I highly recommend doing this because any tweaks/changes/modifications you make won't fuck up your existing setup; then, once you're happy with your configurations, apply the same settings to any user you like. Creating another user is a nice way to make your own sandbox.


- Create a new user

`useradd -m -G wheel -s /bin/bash xfcebspwm`

- Add a password 

`passwd xfcebspwm`



### Set XFCE to forget user settings

If you do decide to create a new user (and you're running Arch), this step may also be necessary. There is a 'quirk' with Arch / XFCE respective to user settings described [here](https://forum.xfce.org/viewtopic.php?id=11509); following the steps below solved the problem for me.

- Edit file: /etc/systemd/logind.conf
- Uncomment line `#KillUserProcesses=no and change to ‘yes’`


## Install bspwm, sxhkd, compton, and [OPTIONAL] rofi | Make directories | Copy Dots
bspwm relies on sxhkd to manipulate windows via assigned key bindings. sxhkd is a 'simple X hotkey daemon' or, in n00b terms, a program that assigns key bindings (i.e. hotkeys) to control windows in bspwm. sxhkd is coded incredibly well and could not be easier to configure once you understand how it works. compton is a 'standalone composite manager' or, in n00b terms, a program that makes your windows look cool. You need to install compton if you want fancy shadows, fading effects, transparency, etc. Lastly, rofi is a 'window switcher, run dialog, ssh-launcher and dmenu replacement'. Installing bspwm on top of XFCE really eliminates the need for a program to launch applications, however, I really like rofi to switch windows and use rofi primarily for this purpose.
- If you're running Arch Linux, run the command below, otherwise install these packages however you have to source them according to your distribution:

`pacman -S bspwm sxhkd compton rofi`

- Create the following directories

`mkdir ~/.config/bspwm/`

`mkdir ~/.config/sxhkd/`

`mkdir ~/.config/compton/`

`mkdir ~/.config/rofi/`

- Copy dotfiles to the directories you just created

**IMPORTANT: MAKE SURE YOUR bspwmrc FILE IS EXECUTABLE - THIS IS THE BIGGEST ROOKIE MISTAKE**

`chmod +x ~/.config/bspwm/bspwmrc`   

## Deactivate xfwm4
- Open 'Session and Startup' in XFCE settings manager and go to the 'Session' tab
- Select xfwm4, click 'Immediately' and change it to the 'Never' option
- Click the button: 'Save Session'

## Remove XFCE hotkeys
- Open 'Keyboard', and click the 'Application Shortcuts' tab
- Remove **ALL** keyboard shortcuts - if you don't do this, sxhkd won't work

## Autostart required applications in XFCE
I'm pretty sure there is a more efficient / elegant way to initiate these applications by editing xprofile or some such but since I'm a n00b and lazy, leveraging XFCE to autostart these applications is the easiest / most convenient option.
- Open 'Session and Startup' in XFCE settings manager
- Navigate to 'Application Autostart'
### Add bspwm
- Name: bspwm
- Description: tiling-window-manager
- Command: bspwm
### Add sxhkd
- Name: sxhkd
- Description: x-hotkey-daemon
- Command: sxhkd
### Add compton
- Name: compton
- Description: composite-manager
- Command: compton --config /home/xfcebspwm/.config/compton/compton.conf -b

The --config flag directs compton to start using the config file located in the user's home directory. You need to spell out the full user directory path. XFCE will not accept '~' as a user's home directory. The -b flag sets compton to run in the background.

## Dotfile notes
### bspwm | bspwmrc
There are a lot of resources out there to understand how this file works. For me, the most helpful guidance was understanding how this file controls mouse actions. The lines below allow the mouse to manipulate windows when the 'alt' key is drpressed: floating windows can be resized with the 'left click' button; floating windows can be moved with the 'right click' button; tiling windows can be resized with the 'left click' button.
- bspc config pointer_modifier mod1
- bspc config pointer_action1 resize_side
- bspc config pointer_action1 resize_corner
- bspc config pointer_action3 move

The other settings I have in this file set the number of workspaces, window padding, etc.
Lastly, I also like having a dock. I use [Docky](http://wiki.go-docky.com/index.php?title=Welcome_to_the_Docky_wiki). In order to set Docky to appear above all other windows, I set this rule:

`bspc rule -a Docky layer=above manage=on border=off focus=off locked=on`

I also have Docky locked with focus turned off, this helps me to prevent accidentally closing Docky. 

### sxhkd | sxhkdrc
sxhkd is great and it's also really easy to use. You assign a keybinding on one line and then in the line below, you indent, and then list the action you want to execute after pressing that keybinding. After reloading the config file (assigned to alt + Escape in my config file) the command will work or it won't. If it doesn't, something is wrong with the action you want to execute or there is a keybinding conflict.

I like to leverage the function keys to execute the main features of bspwm and these are the settings I have defined in my sxhkdrc file:
- F1: rotate windows
- F2: circulate windows
- F3: flip windows horizontal
- F4: flip windows vertical
- F5: alternate between the tiled and monocle layout
- F6: balance windows
- F7: increase window gap
- F8: decrease window gap
- F9: set the window state - floating
- F10: set the window state - tiled
- F11: set the window state - pseudo_tiled
- F12: set the window state - fullscreen

I've also set up some hotkeys to move through workspaces:
- alt + left or right arrow

And some hotkeys to cycle through windows on a workspace:
- alt + up or down arrow

**Note:** I haven't even scratched the surface of bspwm by using the small number of commands listed above. bspwm is such an incredibly versatile WM I'm almost ashamed to only be using these features. Explore the man page, search google, and look at other dots to fully leverage bspwm. Do better than me. You're worth it.

### compton | compton.conf
I honestly don't know what 90% of the shit in this config file even does, the most important part of this file (for me) was to set inactive window transparency. I wanted to set all 'unfocused' windows to be transparent. To do this, I had to adjust the opacity settings:

`#################################`  
`#`  
`# Opacity`  
`#`  
`#################################`  
`menu-opacity = 1;`  
`inactive-window-opacity = 1;`  
`inactive-opacity = 0.60;`  
`active-opacity = 1;`  
`frame-opacity = 1;`  

I also had to make sure these settings equaled 'false':  

`mark-wmwin-focused = false;`  
`mark-ovredir-focused = false;`  

### rofi | config
I really only use rofi to switch windows. 
**Note to anyone reading - please let me know if you have a cool way to switch windows other than rofi!!!**
I've enabled rofi to run by hitting 'alt-tab' [to switch windows] and 'alt-return' [to run applications] both defined in sxhkdrc. Rofi was also always transparent, even when focused. To fix this, I had to add the following settings to **compton.conf**:

`# Specify a list of conditions of windows that should always be considered focused.`

`focus-exclude = ["name = 'rofi'"];`

The [rofi website](https://davedavenport.github.io/rofi/p11-Generator.html) has a really cool page to generate a custom theme. I like black and green. I selected these colors then copypasta into the rofi dot.

### termite | config
The only elements I really adjusted here were 'font' and '[colors]'. For font, set this to whatever you've got installed on your system that you like, for me, that is ['Hack'](https://www.archlinux.org/packages/extra/any/ttf-hack/). For colors, I really dig the website [terminal.sexy](http://terminal.sexy/). The color scheme I'm using is a very slight variation of '/collection/x-dotshare' with foreground et al changed to #00FF00.

## Additional notes
bspwm uses roman numerals to name workspaces. I like this naming convention. To adjust this setting, open XFCE's settings manager, select workspaces, adjust the number of workspaces to match the number of workspaces you have defined in your bspwmrc file and rename them with roman numerals by simply clicking the 'workspace' name.

I was a little confused about CaSe sensitivity respective to bspwmrc and sxhkdrc when launching applications. [I asked about this on the bspwm subreddit](https://www.reddit.com/r/bspwm/comments/6sqw66/case_sensitivity_bspwmrc_and_sxhkdrc/) and received a very helpful response:

`From what i know, in the sxhkdrc file you use the same command that you use when starting the application. In my case for`
`example, that could be firefox or firefox-esr. But, in the bspwmrc I use the the output of xprop second "WM_CLASS(STRING)". In my`
`case, that's Firefox-esr.`

`Or, with libreoffice, I would put libreoffice or loffice in the sxhkd file but i have`

`bspc rule -a libreoffice-startcenter desktop=^3`

`in my bspwmrc since that's the output from xprop.`

`If you don't know about xprop, type xprop in the terminal and select the a window. The last string after "WM_CLASS(STRING)" is`
`what I put in bspwmrc. On firefox, xprop says this for eaxmple:`

`WM_CLASS(STRING) = "Navigator", "Firefox-esr"`

`(It's the same when excluding shadows or changing opacity for specifik aplications with compton btw. You have to use the output`
`from xprop. "urxvt" or "firefox-esr" won't work. It has to be Firefox-esr or URxvt.`

`Hope that helps :)`

`(Btw, if you want to start a GUI app from the terminal without terminal output and so on (and don't use rofi), put something like`

`alias gimp='((gimp > /dev/null 2>&1)&)'`

`in your .bash_aliases file.)`
