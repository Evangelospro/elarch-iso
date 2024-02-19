## Dependencies<a name="dependencies"></a>

### Packages (ALL come ready to use in the iso)

#### [Arch packages](iso/archiso/all_packages.x86_64)

```
paru -S --needed - < iso/archiso/all_packages.x86_64
```

##### [Hacking packages](iso/archiso/all_packages.x86_64#L418) Only in the Hacking ISO

#### [Python pip packages](pip-requirements.txt)

```
pip install -r pip-requirements.txt
```

#### [Python pipx packages](pipx-requirements.txt)

```
pipx install -r pipx-requirements.txt
```

## Linux Setup

### OS: [Arch Linux](https://archlinux.org/)

### Kernel: [Linux-zen](https://archlinux.org/packages/?name=linux-zen)

### Display Server: [Wayland](https://wiki.archlinux.org/title/Wayland)

### Window Manager: [Hyprland](https://wiki.hyprland.org)

### Terminal: [Wezterm](https://github.com/wez/wezterm/)

### Shell [ZSH](https://wiki.archlinux.org/title/Zsh)

#### Bindings: [binds.zsh](dot_config/zsh/executable_binds.zsh)

#### Aliases: [aliases.zsh](dot_config/zsh/executable_aliases.zsh)

#### Functions: [functions.zsh](dot_config/zsh/executable_functions.zsh)

#### Plugin Manager: [Zinit](https://github.com/zdharma-continuum/zinit)

#### [Plugins config](dot_config/zsh/executable_plugins.zsh)

#### Theme: [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

#### Font: [FiraCode Nerd Font](https://www.nerdfonts.com/font-downloads)

#### Color Scheme: [Dracula](https://draculatheme.com/zsh)

## Development Setup

### [Docker-rootless](https://docs.docker.com/engine/security/rootless)

### [Visual Studio Code Insiders](https://code.visualstudio.com/insiders/) [configuration](dot_config/private_Code - Insiders/User/settings.json)

## Hacking Setup

### Shell functions

| Function              | Action                                                                  |
| --------------------- | ----------------------------------------------------------------------- |
| update-burp           | Update burp to the latest version                                       |
| angr                  | Run angr in a docker container                                          |
| extract-base64-string | Extract base64 encoded strings from a file                              |
| extract-urls          | Extract urls from a file                                                |
| frida-init            | Initialize frida server on android device                               |
| frida-kill            | Kill frida server on android device                                     |
| pwnenv                | Create a pwn environment in a docker container                          |
| pwnsetup              | Setup a pwn template in the current directory                           |
| scan                  | Use rustscan to scan a host                                             |
| curl                  | Normal curl but uses the burp proxy if it's running                     |
| ferox-\*              | Feroxbust a host with a specific wordlist                               |
| ffuf-\*               | Fuzz a host with a specific wordlist                                    |
| getWordlist           | Return a wordlist of either dns or dir according to the argument passed |

### Burp

#### Installation and updates

Burp is setup to auto update with the update zsh function above. As I like to use the jar file with my own loaders for obvious reasons, the latest jar file is fetched and placed in $HOME/.config/Burp/Burp-Loader and symlinked to burpsuite_pro.jar

#### Config

-   [project-options.json](dot_config/Burp/project-options.json)
-   [user-options.json](dot_config/Burp/user-options.json)

### IDA [DockerWineIDA](https://github.com/NyaMisty/docker-wine-ida)

IDA essentially runs in docker(running xfce and wine) and rdesktop auto connects
It can be started via the IDA [desktop file](dot_local/private_share/private_applications/burp.desktop) it can be launched from the launcher

### Android Emulator

A setup android emulator can be started from the launcher using the [android_emulator](dot_local/private_share/private_applications/android-emulator.desktop) desktop file

## Custom Arch Linux ISO with AUR packages batteries included

### Ways to get the ISO

#### From the releases tab (automated builds)

##### Two self-explainatory isos (full and light)

[![full version](https://github.com/Evangelospro/dotfiles/actions/workflows/buildISO-full.yml/badge.svg)](https://github.com/Evangelospro/dotfiles/actions/workflows/buildISO-full.yml)
[![light version](https://github.com/Evangelospro/dotfiles/actions/workflows/buildISO-light.yml/badge.svg)](https://github.com/Evangelospro/dotfiles/actions/workflows/buildISO-light.yml)

##### Oneliner that gets you a ready-to-use iso with my dotfiles and packages

```
curl --silent https://raw.githubusercontent.com/Evangelospro/dotfiles/main/iso/get-iso.sh|bash
```

#### Manual download and verification

##### 1) Download all the files from the latest release

##### 2) Verify each part's sha256sum(all should return OK)

```
sha256sum --check *.part*.sha256
```

##### 3) Merge the parts together to get the iso

```
iso_name=$(\ls | grep -E '^ELARCH-*.iso.sha256$' | sed 's/.sha256//')
cat $(\ls | grep -E '^ELARCH-.*\.part[^.]*$') > $iso_name
```

##### 4) Verify the combined sha256sum

```
sha256sum --check $iso_name.sha256
```

### Manual Build

```
cd iso
./build.sh
```

## Installation and Usage

### WARNING: The dotfiles are applied differently on the iso based on the hostanme `ELARCH-ISO`, so **whatever you do dont' change or set the hostname to** `ELARCH-ISO` or `ELARCH-F15`(as this applies some extra configs that are very specific to me and my own hardware etc...), during or after the installation! But again **I really, really recommend that you fork this repo and edit the files** to your liking before applying them!!!

### 1) [Download](#ways-to-get-the-iso) the iso and flash it to a usb drive

### 2) Default user is `liveuser` and password is `liveuser` sign in with these and wait for the iso to finish the initial downloads

### 3) A nice calamares installer is also included to guide you through the installation process, in case it didn't start automatically using the launcher shortcut from [above](#launch--reload-applications), you can start it manually by searching `install system` in the launcher or by running `sudo calamares -d` in a terminal, which will also give you some debug info that you should include in an issue if you encounter any problems.
