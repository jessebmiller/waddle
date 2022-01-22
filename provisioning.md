# Provisioning a new linux install

## Applications

* Brave
* Steam
* Discord
* Docker
* qemu
* virt-manager

## services

* backups?!?
* sleep after a while (power management)
powerkit — Desktop independent power manager.
https://github.com/rodlie/powerkit || powerkit (AUR)

## apps to play with

* neofetch
* alacritty
* informant https://aur.archlinux.org/packages/informant/

# nvidia

* nvidia-installer-dkms
* yay -S optimus-manager optimus-manager-qt

systemctl status optimus-manager

To start and enable it run (if it is not running):

sudo systemctl enable --now optimus-manager

`optimus-manager --switch nvidia`
to switch to the Nvidia GPU
`optimus-manager --switch integrated`
to switch to the integrated GPU and power the Nvidia GPU off
`optimus-manager --switch hybrid`
to switch to the iGPU but leave the Nvidia GPU available for on-demand offloading, similar to how Optimus works on Windows.

## Configuration

* Some aliases please
  * abstract to the level of human decisions. pacman's options are opaque and dumb
    * Things I want to do with packages
      * install `pacman -S`
      * remove `pacman -R`
      * search `pacman -Ss`
      * info `pacman -Si`
      * update `echo "lol actually don't do this in arch..."
      * upgrade my system `pacman -Syu && yay`
      * snapshot what I've got (btrfs? before every install/upgrade?)
* Remap caps-lock to ctrl
  * move Xmodmap to `~/.Xmodmap`
    LightDM will load that at startup or you can load it with `xmodmap ~/.Xmodmap`
      kinda looks like lightdm doesn't load this...
* Connect bluetooth mouse
  https://discovery.endeavouros.com/bluetooth/bluetooth/2021/03/
  `sudo pacman -S --needed bluez bluez-utils blueman`
  add `blueman-applet` to ~/.config/qtile/autostart.sh`
* Fonts
  ~/.config/fontconfig/fonts.conf file to whitelist and blacklist fonts.
  * TODO take /etc/fonts/conf.d/* under WADDLE JURISDICTION?
    Maybe not. these are good defaults provided by EndevourOS they are
    probably pretty stable
  * Brave looks at GTK theme for menu/tab fonts...
    TODO take ~/.gtkrc-2.0 under WADDLE JURISDICTION
    TODO take ~/.config/gtk-3.0/ unde WADDKE JURISDICTION (this is the one brave looks at)
         changing `gtk-font-name` in `settings.ini` to `DefaVu Sans 12` fixed it
* Solarized terminal colors
  TODO take `~/.config/alacritty/alacritty.yml` undel WADDLE JURISDICTION
* `ssh-keygen` then add to github
* git global config
* put emacs.d in place
* Shell config
  * zsh? bash? fish?
  * functions
* Audio buttons
* Screen brightness
  `    Key([], "XF86MonBrightnessUp", lazy.spawn("xbacklight -inc 10")),`
  `    Key([], "XF86MonBrightnessDown", lazy.spawn("xbacklight -dec 10")),`
* TODO take qtile config under WADDLE JURISDICTION
* displays, screens, monitors etc.
  arandr to create .screenlayout/three.sh
  autorandr to detect and change layouts
    autorandr --save (to save current layout)
    autorandr --change (to load the detected profile)
  TODO take `~/.config/autorandr` uner WADDLE JURISDICTION

# Working environments

* Software project environments
  * nix-shell?
  * lxd containers?

* Windows VM
  * Need to set PCI passthrough
  * set grub boot options
  * Create virtual machine with qemu, virt-manager
  * https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF#Setting_up_IOMMU