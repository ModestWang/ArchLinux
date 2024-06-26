# ArchLinux
## oh-my-posh
```shell
export PATH="${PATH}:~/bin"
export POSHTHEME="~/.cache/oh-my-posh/themes"

eval "$(oh-my-posh --init --shell bash --config ${POSHTHEME}/my.omp.json)"
```
```json
my.omp.json
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
