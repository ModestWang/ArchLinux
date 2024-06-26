# ArchLinux

## archlinuxcn
```
使用方法：在 /etc/pacman.conf 文件末尾添加以下两行：

[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch

# 安装 haveged
pacman -Syu haveged
systemctl start haveged
systemctl enable haveged

# 初始化 keyring
rm -fr /etc/pacman.d/gnupg
pacman-key --init
pacman-key --populate archlinux

# 之后通过以下命令安装 archlinuxcn-keyring 包导入 GPG key。
pacman -Sy archlinuxcn-keyring
# 新系统中安装 archlinuxcn-keyring 包前的额外步骤
# 2023 年 12 月后，在新系统下安装 archlinuxcn-keyring 时可能会出现错误：
# error: archlinuxcn-keyring: Signature from "Jiachen YANG (Arch Linux Packager Signing Key) " is marginal trust
# 需要在本地信任 farseerfc 的 GPG key：
pacman-key --lsign-key "farseerfc@archlinux.org"

# 执行完毕后再次安装archlinuxcn-keyring
pacman -S archlinuxcn-keyring

#然后执行下一条命令
pacman-key --populate archlinuxcn
```

## environment
```
#
# This file is parsed by pam_env module
# etc/environment
# Syntax: simple "KEY=VAL" pairs on separate lines
#

GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```

## fcitx
```shell
sudo pacman -S fcitx5-im fcitx5-chinese-addons fcitx5-material-color fcitx5-configtool
sudo pacman -S fcitx5-pinyin-zhwiki fcitx5-pinyin-moegirl
```


## flatpak
```
sudo apt install flatpak

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo # 官方源

flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub # 上海交大源
```

## locale.gen
/etc/locale.conf
```

LC_ALL=zh_CN.UTF-8
```

/etc/locale.gen
```
zh_CN.UTF-8 UTF-8  
en_US.UTF-8 UTF-8
```

```shell
locale-gen
```

## oh-my-posh
```shell
export PATH="${PATH}:~/bin"
export POSHTHEME="~/.cache/oh-my-posh/themes"

eval "$(oh-my-posh --init --shell bash --config ${POSHTHEME}/my.omp.json)"
```

my.omp.json

```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "blocks": [
    {
      "alignment": "left",
      "segments": [
        {
          "type": "python",
          "style": "plain",
          "foreground": "#b4eb8d",
          "properties": {
            "display_virtual_env": true,
            "display_default": true,
            "display_version": false,
            "home_enabled": true,
            "prefix": "\uE235 ",
            "postfix": " ",
            "display_mode": "always"
          }
        },
        {
          "background": "#33c4e5",
          "foreground": "#f8f8f2",
          "leading_diamond": "\ue0b6",
          "style": "diamond",
          "template": "{{ .Icon }} {{ .HostName }} ",
          "type": "os"
        },
        {
          "background": "#bd93f9",
          "foreground": "#f8f8f2",
          "powerline_symbol": "\ue0b0",
          "properties": {
            "style": "folder"
          },
          "style": "powerline",
          "template": " {{ .Path }} ",
          "type": "path"
        },
        {
          "background": "#ffb86c",
          "foreground": "#f8f8f2",
          "powerline_symbol": "\ue0b0",
          "properties": {
            "branch_icon": "",
            "fetch_stash_count": true,
            "fetch_status": false,
            "fetch_upstream_icon": true
          },
          "style": "powerline",
          "template": " \ue725 ({{ .UpstreamIcon }}{{ .HEAD }}{{ if gt .StashCount 0 }} \ueb4b {{ .StashCount }}{{ end }}) ",
          "type": "git"
        },
        {
          "background": "#00c983",
          "foreground": "#f8f8f2",
          "powerline_symbol": "\ue0b0",
          "style": "powerline",
          "template": " \ue718 {{ if .PackageManagerIcon }}{{ .PackageManagerIcon }} {{ end }}{{ .Full }} ",
          "type": "node"
        },
        {
          "background": "#ff79c6",
          "foreground": "#f8f8f2",
          "powerline_symbol": "\ue0b0",
          "properties": {
            "time_format": "15:04"
          },
          "style": "powerline",
          "template": " \u2665 {{ .CurrentDate | date .Format }} ",
          "type": "time"
        },
        {
          "background": "#83769c",
          "foreground": "#f8f8f8",
          "powerline_symbol": "\ue0b0",
          "properties": {
            "always_enabled": true
          },
          "style": "powerline",
          "template": " \ueba2 {{ .FormattedMs }} ",
          "type": "executiontime"
        }
      ],
      "type": "prompt"
    },
    {
      "alignment": "left",
      "segments": [
        {
          "background": "#f1fa8c",
          "foreground": "#282a36",
          "invert_powerline": true,
          "leading_diamond": "\ue0b2",
          "style": "diamond",
          "template": " \ue7ad {{.Profile}}{{if .Region}}@{{.Region}}{{end}}",
          "trailing_diamond": "\ue0b4",
          "type": "aws"
        }
      ],
      "type": "rprompt"
    },
    {
      "alignment": "left",
      "newline": true,
      "segments": [
        {
          "foreground": "#cd5e42",
          "style": "plain",
          "template": "\ue3bf ",
          "type": "root"
        },
        {
          "foreground": "#9ef8fa",
          "style": "plain",
          "template": " <#45F1C2><b>\u26a1</b></><b>{{ .UserName }}</b> <#26C6DA>\u276f</><#45F1C2>\u276f</>",
          "type": "text"
        }
      ],
      "type": "prompt"
    }
  ],
  "final_space": true,
  "version": 2
}
```

## pacman.conf
```
#
# /etc/pacman.conf
#
# See the pacman.conf(5) manpage for option and repository directives

#
# GENERAL OPTIONS
#
[options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
#RootDir     = /
#DBPath      = /var/lib/pacman/
#CacheDir    = /var/cache/pacman/pkg/
#LogFile     = /var/log/pacman.log
#GPGDir      = /etc/pacman.d/gnupg/
#HookDir     = /etc/pacman.d/hooks/
HoldPkg     = pacman glibc
#XferCommand = /usr/bin/curl -L -C - -f -o %o %u
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
#CleanMethod = KeepInstalled
Architecture = auto

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
#IgnorePkg   =
#IgnoreGroup =

#NoUpgrade   =
#NoExtract   =

# Misc options
#UseSyslog
#Color
#NoProgressBar
CheckSpace
#VerbosePkgLists
#ParallelDownloads = 5

# By default, pacman accepts packages signed by keys that its local keyring
# trusts (see pacman-key and its man page), as well as unsigned packages.
SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional
#RemoteFileSigLevel = Required

# NOTE: You must run `pacman-key --init` before first using pacman; the local
# keyring can then be populated with the keys of all official Arch Linux
# packagers with `pacman-key --populate archlinux`.

#
# REPOSITORIES
#   - can be defined here or included from another file
#   - pacman will search repositories in the order defined here
#   - local/custom mirrors can be added here or in separate files
#   - repositories listed first will take precedence when packages
#     have identical names, regardless of version number
#   - URLs will have $repo replaced by the name of the current repo
#   - URLs will have $arch replaced by the name of the architecture
#
# Repository entries are of the format:
#       [repo-name]
#       Server = ServerName
#       Include = IncludePath
#
# The header [repo-name] is crucial - it must be present and
# uncommented to enable the repo.
#

# The testing repositories are disabled by default. To enable, uncomment the
# repo name header and Include lines. You can add preferred servers immediately
# after the header, and they will be used before the default mirrors.

#[core-testing]
#Include = /etc/pacman.d/mirrorlist

[core]
Include = /etc/pacman.d/mirrorlist

#[extra-testing]
#Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#Include = /etc/pacman.d/mirrorlist

[multilib]
Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs

[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

## End
Thanks!🙏
