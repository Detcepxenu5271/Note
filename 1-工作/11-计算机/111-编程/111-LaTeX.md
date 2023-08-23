# LaTeX

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
