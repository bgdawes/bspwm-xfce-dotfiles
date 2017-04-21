## The n00b's guide to bspwm (with XFCE)...

If you are interested in tiling WM's but you're also an id10t (like me) the following guide below will walk you through setting up the best (imho) tiling WM ( **bspwm** ) to run alongside XFCE. This setup is nice for n00b id10ts because it grants you all of the great features of a tiling WM without having to sacrifice the conveniences of a DE (in this case, XFCE).

### === Create new user: xfcebspwm ===
> You may or may not want to do this step. If you've got a good setup already, I highly recommed doing this because any tweaks/changes/modifications you make won't f' up your existing setup.

Execute the follwing commands as root:

Create a new user
- useradd -m -G wheel -s /bin/bash xfcebspwm

Add a password 
- passwd xfcebspwm

### === Set XFCE to forget user settings ===
- Edit file: /etc/systemd/logind.conf
- Uncomment line #KillUserProcesses=no and change to ‘yes’
- If you have a XFCE panel and have 'Actions Button' as a panel item,  turn off all selections in the ‘Actions Button’ item on the XFCE top panel except for ‘Log Out...’ and then be sure to uncheck ‘Save session for future log in’ otherwise XFCE will try and restart all applications you had running before log-off / reboot 

### === Install bspwm, sxhkd, compton, and rofi | Make directories | Copy Dots ===
If you're running Arch Linux, run the command below, otherwise get these packages however you have to source them according to your distribution:
- pacman -S bspwm sxhkd compton rofi

Create the following directories
- mkdir ~/.config/bspwm/
- mkdir ~/.config/sxhkd/
- mkdir ~/.config/compton/
- mkdir ~/.config/rofi/

Copy my dots to the directories you just created


