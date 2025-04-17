# LaTeX


## 环境配置
[Visual Studio Code (vscode)配置LaTeX](https://zhuanlan.zhihu.com/p/166523064)

关于 VSCode 使用外部 pdf 查看器 SumatraPDF 反向搜索的问题
* 在 VSCode 的设置中, 配置以下内容:
	```json
	"latex-workshop.view.pdf.external.synctex.args": [
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "-reuse-instance",
        "-inverse-search",
        "\".../Microsoft VS Code/Code.exe\" --ms-enable-electron-run-as-node \".../Microsoft VS Code/resources/app/out/cli.js\" -r -g \"%f:%l\"", // 注意修改...为你的路径
        "%PDF%"
    ]
	```
* 在 SumatraPDF 的 `SumatraPDF-settings.txt` 文件中, 配置 (同样记得修改为你的路径):
	```txt
	InverseSearchCmdLine = ".../Microsoft VS Code/Code.exe" --ms-enable-electron-run-as-node ".../Microsoft VS Code/resources/app/out/cli.js" -r -g "%f:%l"
	EnableTeXEnhancements = true
	```
* 然后在 SumatraPDF 中就可以双击反向搜索了, 且不会弹小黑框

## 一份其实很短的 LaTeX 入门文档
### 第一篇文档
`\documentclass[UTF8]{article}`调用 article 文档类，增加文档选项 UTF8；影响文档输出的效果

注释符号：`%`

环境
```TeX
\begin{document}
\end{document}
```
* 只有环境中的内容才被输出到文档，或作为控制序列对文档产生影响
* `\documentclass{article}`和`\begin{document}`之间的内容被称为导言区，通常在导言区设置页面大小、页眉页脚样式、章节标题样式等等

`\usepackage{xeCJK}`使用宏包

### 组织你的文章
