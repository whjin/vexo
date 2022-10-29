---
title: vscode配置
date: 2019-09-05 04:41:29
category: ["工具"]
tags: ["前端工具"]
comments: true
---

# 插件 #

1. `Beautify`
2. `chinese Language`
3. `open in browser`
4. `Vetur`
5. `minapp`

<!--more-->

# `settings.json` #

```json
{
    "window.zoomLevel": 1,
    "markdown.preview.fontSize": 16,
    "[html]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[javascript]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[json]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "editor.wordWrap": "on",
    "files.associations": {
        "*.tpl": "html",
        ".easymockrc": "json"
    },
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            "wrap_attributes": "force-aligned"
        }
    }
}
```


```json
{
    "window.zoomLevel": 1,
    "markdown.preview.fontSize": 16,
    "[html]": {
        "editor.defaultFormatter": "vscode.html-language-features"
    },
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[json]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "editor.wordWrap": "on",
    "files.associations": {
        "*.tpl": "html",
        ".easymockrc": "json",
        "*.vue": "vue",
        "*.cjson": "jsonc",
        "*.wxss": "css",
        "*.wxs": "javascript"
    },
    "editor.hideCursorInOverviewRuler": true,
    "editor.hover.enabled": false,
    "editor.autoClosingBrackets": "always",
    "workbench.sideBar.location": "left",
    "[jsonc]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "prettier.singleQuote": true,
    "prettier.semi": false,
    "emmet.includeLanguages": {
        "wxml": "html",
        "javascript": "html",
        "velocity": "html"
    },
    "minapp-vscode.disableAutoConfig": true,
    "eslint.enable": false,
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        {
            "language": "html",
            "autoFix": true
        },
        {
            "language": "vue",
            "autoFix": true
        }
    ],
    "explorer.confirmDragAndDrop": false,
    "explorer.confirmDelete": false,
    "liveServer.settings.donotShowInfoMsg": true,
    "[typescript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "workbench.iconTheme": "vscode-icons"
}
```