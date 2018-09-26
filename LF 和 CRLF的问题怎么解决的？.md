##   LF 和 CRLF的问题怎么解决的？

解决步骤：
```
1.首先，git进行如何设置
git config --global core.autocrlf false
git config --global core.safecrlf true

2.然后再vscode编辑中，选择文件》首选项》设置

```
```js
{
     "workbench.iconTheme": "vscode-icons",
    "editor.fontSize": 20,
    "javascript.implicitProjectConfig.experimentalDecorators": true,
    "files.associations": {
        "*.js": "javascriptreact"
    },
    "workbench.colorTheme": "Monokai",
    "window.zoomLevel": 0,
    "sublimeTextKeymap.promptV3Features": true,
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.snippetSuggestions": "top",
    // "editor.formatOnPaste": true,
    "emmet.triggerExpansionOnTab": true,
    "editor.tabSize": 2,
    "editor.quickSuggestions": {
        "other": true,
        "comments": true,
        "strings": true
    },
    "editor.formatOnSave": true,
    "editor.renderControlCharacters": true,
    "editor.renderWhitespace": "all",
    "eslint.autoFixOnSave": true,
    "workbench.startupEditor": "newUntitledFile",
    "explorer.confirmDragAndDrop": false,
    "files.autoSave": "onFocusChange",
    "git.autofetch": true
}
```
```
3.将这个设置补充到你的用户设置内容中


4.如果你本地在全局环境中也生成有eslint的配置文件，就将咱们项目中的 eslintrc.js 这份配置文件，将你全局下的配置文件覆盖掉
```

工作注意：

你在写文件时，可以看下vscode 编辑器的右下角是不是LF，这里会显示换行符类型，如果不是LF的，你就点击这里进行切换，然后保存文件就行了


find . -type f -exec dos2unix {} \;



