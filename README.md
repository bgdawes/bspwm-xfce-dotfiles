## The n00b's guide to bspwm...

If you are interested in tiling WM's but you're also an id10t (like me) the following guide below will walk you through setting up the best (imho) tiling WM ( **bspwm** ) to run alongside XFCE. This setup is nice for n00b id10ts because it grants you all of the great features of a tiling WM without having to sacrifice the conveniences of a DE (in this case, XFCE).

### === Create new user: xfcebspwm ===
> You may or may not want to do this step. If you've got a good setup already, I highly recommed doing this because any tweaks/changes/modifications you make won't f' up your existing setup.

Execute the follwing commands as root:

Create a new user
- useradd -m -G wheel -s /bin/bash xfcebspwm

Add a password 
- (root) passwd xfcebspwm

### === Set XFCE to forget user settings ===
1. Edit file: /etc/systemd/logind.conf
2. Uncomment line #KillUserProcesses=no and change to ‘yes’
3. Turn off all selections in the ‘Actions Button’ item on the XFCE top panel except for ‘Log Out...’ and then be sure to uncheck ‘Save session for future log in’ otherwise XFCE will try and restart all applications you had running before log-off / reboot 

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/bgdawes/dotfiles/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
