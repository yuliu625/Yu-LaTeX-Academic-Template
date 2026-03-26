# Latex Academic Template
这是一个遵循“约定优于配置”思想的 **LaTeX 工程化模板**。其核心目标是通过**层级隔离**，实现学术资产（图表、算法、文字）在不同出版社模板间的无缝迁移与快速复用。


## 🌟 核心设计哲学
### 约定优于配置
通过预设的文件夹命名结构，无需在 `main.tex` 中编写复杂的路径查找逻辑。只要将文件放入对应的 `modules` 或 `components`，即可通过标准化的 `\input` 命令进行调用，极大降低了环境迁移时的配置成本。

### 模块化隔离
`contents/modules` 这个中性命名指的是 `sections` 或 `chapters`，即:
- **短文/会议**: Module 对应 `\section`。
- **长文/学位论文**: Module 对应 `\chapter`。

### 过渡层设计
这是本模板的精髓。`components` 作为 `assets` 与 `contents` 之间的桥梁：
- **修改友好**: 如果图片需要从 `.pdf` 换成 `.png`，只需修改 `components` 里的封装代码，无需触碰正文 `contents`。
- **多处调用**: 同一个图表组件可以同时被论文 `main.tex` 和演示文稿 `beamer.tex` 引用。

### 协作兼容性
考虑到学术合作中并非所有成员都熟练使用 Git，`backups` 文件夹提供了一个物理存储空间，用于存放合作者修改后的旧稿或草堆，确保在版本回溯时的人工容错。


## 📂 项目结构
本项目将论文构建视为一条自动化流水线，每一层处理特定的任务，确保内容与表现形式解耦。
```bash
# 1. 原始资源层 (Raw Assets)
├── assets/                 # 存放原始实验数据 (SVG, AI, Python Plot, Excel)
│
# 2. LaTeX 适配层 (Component Bridge)
├── components/             # 过渡层：将 Assets 包装为 LaTeX 可调用的对象
│   ├── figures/            # 包含 \includegraphics, \caption, \label 的独立 .tex 片段
│   ├── tables/             # 封装好的表格逻辑
│   └── algorithms/         # 封装好的伪代码块
│
# 3. 语义内容层 (Semantic Contents)
├── contents/               # 纯文字内容，不涉及具体的排版样式
│   ├── modules/            # 论文主体 (Chapter 或 Section )
│   ├── appendix/           # 附录内容
│   ├── references/         # 参考文献库 (.bib)
│   └── structure.tex       # 逻辑组织层，编排 Modules 
│
# 4. 环境配置层 (Global Configs)
├── configs/                # 全局宏包依赖与自定义宏命令 
│
# 5. 表现/输出层 (Presentation Layer)
├── main.tex                # 出版社提供的标准模板入口（如 IEEEtran.cls / nature.cls）
│
# 6. 辅助工具层 (Support & Ops)
├── scripts/                # 自动化处理脚本（数据转表格、清理冗余等）
└── backups/                # 容错层：为不熟悉 Git 的合作者保留的旧版内容备份
```


## 💡 使用指南
1.  **准备素材**: 将实验原始图表放入 `assets`。
2.  **编写组件**: 在 `components` 中创建对应的 `.tex` 文件，引用 `assets` 中的导出图。
3.  **撰写内容**: 在 `contents/modules` 中完成文字叙述，并在需要处引用 `components` 中的组件。
4.  **注入容器**: 在 `main.tex` 中通过 `\input{contents/structure.tex}` 完成整篇论文的组装。


## 🚀 快速切换投稿流
当需要更换投稿期刊时，你的工作流仅需两步：
1. **替换 `main.tex`**: 使用出版社提供的 `.cls` 和 `.tex` 样例。
2. **重定向引用**: 在新 `main.tex` 中通过 `\input{configs/...}` 和 `\input{contents/structure.tex}` 重新挂载你的内容资产。


## 🔗 关联项目
除了 LaTeX 模板，我还构建了一个基于**Typst**的学术模板[Typst-Academic-Template](https://github.com/yuliu625/Yu-Typst-Academic-Template)。尽管Typst是一种更现代、高效的排版工具，但目前LaTeX仍然是学术界的主流规范。你可以:
- 使用 Typst 日常使用和快速构建内容。
- 使用相关工具将 Typst 项目转换为 LaTeX 格式。(对于个人论文如此，合作论文可能需要共同使用LaTeX在线编辑工具。)

这个模板系列的目的，是为了能够轻松地在不同排版工具间转换和复用内容，以适应不同的合作和投稿需求。

