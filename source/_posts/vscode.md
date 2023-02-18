---
title: vscode
date: 2021-16-21 20:49:44
categories: vscode
excerpt: vscode插件备忘，用户代码片段，setting配置文件。
---

### 插件
- 正则: any-rule
- 中文: Chinese (Simplified) Language
- Git记录: Git History
- GitLens: 可history，file、branch、commit对比，合并     
- 文件引入: Path Intellisense
- 文件图标: vscode-icons
- 预览md文件 Markdown Preview Enhanced
- html 重复(覆盖)注释工具 Nested Comments

- 代码校验: ESLint
- vue代码提示: Vetur
- vue3 代码提示: Vue 3 Snippets
- vue3语法高亮 Vue Language Features (Volar)  把插件Vuter禁用

- vue快速代码格式: vue-helper
- 代码块快速识别标记: Bracket Pair Colorizer
- html标签开始标签与结尾标签 高亮 Highlight Matching Tag 很不错
- 保存格式化: Prettier - Code formatter
- 自动匹配html/xml标签  Auto rename tag

- Tailwind CSS IntelliSense
- Tailwind CSS Autocomplete

### setting
```json
{
  "editor.fontSize": 15.4,
  "editor.tabSize": 2,
  "editor.formatOnSave": false, // 保存格式化
  "editor.tabCompletion": "on", // 启用 Tab 补全
  "editor.formatOnType": true, // 控制编辑器在键入一行后是否自动格式化该行。
  "editor.autoIndent": "keep", // 控制编辑器是否应在用户键入、粘贴、移动或缩进行时自动调整缩进。
  "editor.guides.bracketPairs": true, // 控制是否启用括号对指南。
  "editor.fastScrollSensitivity": 10, // 按下"Alt"时滚动速度倍增。
  "editor.mouseWheelScrollSensitivity": 3, // 对鼠标滚轮滚动事件的 deltaX 和 deltaY 乘上的系数
  "editor.bracketPairColorization.enabled": true, // 重写括号突出显示颜色
  "editor.suggest.snippetsPreventQuickSuggestions": false, // 控制活动代码段是否阻止快速建议。
  "editor.accessibilitySupport": "off", // 控制编辑器是否应在对屏幕阅读器进行了优化的模式下运行。设置为“开”将禁用自动换行。
  "editor.wordWrap": "on", // on: 将在视区宽度处换行，off: 永不换行, on: 将在视区宽度处换行。
  "editor.wordWrapColumn": 80, // 在 #editor.wordWrap# 为 wordWrapColumn 或 bounded 时，控制编辑器的折行列。
  "editor.detectIndentation": false, // 控制是否在打开文件时，基于文件内容自动检测 #editor.tabSize# 和 #editor.insertSpaces#。
  "editor.codeActionsOnSave": {
    // "source.fixAll.tslint": true,
    // "eslint.autoFixOnSave": true,
  },
  // 自定义代码片段显示的位置
  "editor.snippetSuggestions": "top",
  // 控制当超出可用空间时，选项卡是否应在多行之间换行，或者是否应显示滚动条。
  // 当 "#workbench.editor.showTabs#" 处于禁用状态时，将忽略此值。
  "workbench.editor.wrapTabs": true,
  "debug.console.fontSize": 15, // 控制调试控制台中的字体大小(以像素为单位)。
  // 控制如何处理在受信任的工作区中打开不受信任的文件。此设置也适用于通过 `#security.workspace.trust.emptyWindow#" 打开的空窗口中的文件。
  // open: 始终允许不受信任的文件引入受信任的工作区，而不显示提示
  "security.workspace.trust.untrustedFiles": "open",
  "html.format.enable": true, // 对 {{#foo}} 和 {{/foo}} 进行格式化与缩进。
  "html.format.indentHandlebars": true, // 对 {{#foo}} 和 {{/foo}} 进行格式化与缩进(针对html代码可读性)
  "html.format.preserveNewLines": false, // 控制是否保留元素前已有的换行符。仅适用于元素前，不适用于标记内或文本。
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true, //让函数(名)和后面的括号之间加个空格
  /** vetur配置 */
  "vetur.validation.script": true,
  "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
  "vetur.format.defaultFormatter.html": "js-beautify-html", //格式化.vue中html
  "vetur.format.defaultFormatter.js": "vscode-typescript", //让vue中的js按编辑器自带的ts格式进行格式化
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      // "wrap_attributes": "force-expand-multiline" //属性强制折行对齐
    },
    "prettier": {
      "eslintIntegration": true, // 让prettier使用eslint的代码格式进行校验
      "semi": false, // 禁止结尾分号
      "trailingComma": "none", // 禁止末尾加逗号
      "singleQuote": false, // 禁止单引号
      // "tabWidth": 2, // 缩进
    }
  },
  /** prettier配置 */
  // 添加⾃定义规则
  // "prettier.semi": false, // 句末加分号
  // "prettier.useTabs": true,
  // "prettier.singleQuote": true, // 用单引号
  // "prettier.trailingComma": "none", // 禁止末尾添加逗号
  // "prettier.tabWidth": 2,
  // "prettier.embeddedLanguageFormatting": "off",
  /** End */
  "files.associations": {
    "tslint.json": "jsonc",
    "*.md": "mdx",
    "*.cjson": "jsonc",
    "*.wxss": "css",
    "*.wxs": "javascript"
  },
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[javascript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    // "editor.defaultFormatter": "rvest.vs-code-prettier-eslint",
  },
  "[typescript]": {
    "editor.defaultFormatter": "vscode.typescript-language-features",
    // "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "[vue]": {
    "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
  },
  // "[vue]": {
  //   // "editor.defaultFormatter": "octref.vetur", // vetur插件vue2标准格式化
  //   // "editor.defaultFormatter": "Vue.volar" // Vue.volar能识别vue3的语法，（但不应该用作格式化，有问题）
  //   // "editor.defaultFormatter": "rvest.vs-code-prettier-eslint", // prettier根据eslint格式化
  //   // "editor.defaultFormatter": "esbenp.prettier-vscode", // 千万注意!!! 用于vue3可能因为一些非标准代码写法,导致误删已有代码
  // },
  /**插件-自动补全标签配置*/
  // "auto-rename-tag.activationOnLanguage": ["html","xml","php","javascript"],
  /** End */
  /** 配置主体icon文件图标 */
  // "workbench.iconTheme": "vscode-icons",
  /** End */
  /** 插件-编辑区背景 Start */
  "background.enabled": true,
  "background.useFront": true,
  "background.loop": true,
  "background.style": {
    "content": "''",
    "pointer-events": "none",
    "position": "absolute",
    "z-index": "999",
    "width": "100%",
    "height": "100%",
    "background-position": "100% 100%",
    // "background-repeat": "no-repeat",
    "opacity": 0.6
    // "opacity": 0.2,
  },
  "background.useDefault": true,
  // "background.customImages": [
  // "/D:/vscode-background/011321OZPMH.jpg"
  // ],
  /** End*/
  /** gitlens Start*/
  "gitlens.views.branches.files.layout": "tree",
  "git.autofetch": true, // 自动从当前 Git 仓库的默认远程仓库提取提交。若设置为“全部”，则从所有远程仓库进行提取
  "git.suggestSmartCommit": false,
  "emmet.includeLanguages": {
    "wxml": "html"
  },
  "minapp-vscode.disableAutoConfig": true,
  // "markdown-preview-enhanced.automaticallyShowPreviewOfMarkdownBeingEdited": true,
  "git.allowForcePush": false, // 控制是否启用强制推送 (不论 force 还是 force-with-lease)。
  /** End*/
}
```