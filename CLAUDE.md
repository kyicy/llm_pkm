# CLAUDE.md

## 笔记生成规范

- wiki 目录生成的笔记**必须使用英文**书写
- raw 和 wiki 目录中生成的笔记，其中的数学公式**必须使用 KaTeX 格式**（即 `$...$` 或 `$$...$$`）

## Python 脚本运行

所有 Python 脚本均使用 `mise` 搭配 `uv` 运行，而非系统自带的 `python` 或 `python3`。

- 执行脚本：`mise exec -- uv run <script.py>`
- 安装依赖：`mise exec -- uv add <package>`
- 安装项目：`mise exec -- uv sync`

## Rust 项目运行

所有 Rust 项目均使用 `mise` 搭配 `cargo` 运行。

- 构建项目：`mise exec -- cargo build`
- 运行项目：`mise exec -- cargo run`
- 运行测试：`mise exec -- cargo test`
- 检查代码：`mise exec -- cargo check`
- 添加依赖：`mise exec -- cargo add <package>`
- 安装项目：`mise exec -- cargo build --release`
