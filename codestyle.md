# JS/HTML/CSS 代码规范

## 代码格式化

- 编辑器(vscode)
- 扩展(vetur + eslint + Prettier - Code formatter)
- 配置(file>preferences>settings>workspace)

```
{
    "vetur.format.defaultFormatter.js": "vscode-typescript",
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
    "eslint.autoFixOnSave": true,
    "eslint.validate": [
        {
          "language": "vue",
          "autoFix": true
        },
        {
          "language": "html",
          "autoFix": true
        },
        {
          "language": "javascript",
          "autoFix": true
        }
    ],
    "editor.tabSize": 2,
    "prettier.eslintIntegration": true,
    "prettier.singleQuote": true,
}
```
- Linux   快捷键(CTRL SHIFT + I)
- Windows 快捷键(SHIFT Alt + F)

## 编码规范

参照[eslint](https://github.com/standard/standard/blob/master/docs/RULES-zhcn.md)规范文件
