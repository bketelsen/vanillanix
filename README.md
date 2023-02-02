# Install Nix on VanillaOS

## WARNING
This is *experimental* use at your own risk!

## Instructions

Step 1:
Make a directory in your $HOME to hold the nix store:
`mkdir $HOME/.nix`

Step 2:
clone this repository to /tmp 
`cd /tmp && git clone https://github.com/bketelsen/vanillanix`

Step 3:
Open an ABRoot shell and move into the tmp dir:
`sudo abroot shell`
`cd /tmp/vanillanix`

Step 4:
edit the two service files to replace my username with yours
`ensure-nix-dir.service` & `ensure-nix-own.service`

Step 5:
edit the mount file to replace my username with yours
`nix.mount`

Step 6:
Copy the service and mount files into /etc/systemd/system:
`cp *.service /etc/systemd/system/`
`cp *.mount /etc/systemd/system/`

Step 7:
Enable the `nix.mount` unit.
`systemctl enable /etc/systemd/system/nix.mount`

You don't need to enable the others, they're dependencies of the mount file.

Step 8:
Exit abroot shell & reboot

Step 9:
Install nix as in single-user mode.
Open a regular (non apx) shell:
`sh <(curl -L https://nixos.org/nix/install) --no-daemon`

This installs nix to `/nix` where it wants to be, but `/nix` is actually a symlink to inside your home directory.
The installation will modify your `.bashrc`, `.zshrc` as appropriate, adding nix to your paths.

Step 10: Optional, but highly recommended!
Add a nix configuration file enabling flakes and the new nix command:
`mkdir -p ~/.config/nix/`
`echo "experimental-features = nix-command flakes" > ~/.config/nix/nix.conf`

