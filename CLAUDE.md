# CLAUDE.md

## Python 脚本运行

所有 Python 脚本均使用 `mise` 搭配 `uv` 运行，而非系统自带的 `python` 或 `python3`。

- 执行脚本：`mise exec -- uv run <script.py>`
- 安装依赖：`mise exec -- uv add <package>`
- 安装项目：`mise exec -- uv sync`
