# 科研工具笔记

## Obsidian

- 使用稳定目录管理课程作业、每日记录和长期知识。
- 通过 Markdown 链接连接相关笔记，例如 `[推荐系统笔记](recsys.md)`。
- 每天复制 `daily_logs/TEMPLATE.md`，避免遗漏关键记录项。
- `.obsidian/workspace.json` 属于本机界面状态，不需要同步。

## Git

第一次初始化：

```powershell
git init
git add .
git commit -m "init research training notes"
git branch -M main
```

日常更新：

```powershell
git status
git add .
git commit -m "update learning notes"
git push
```

查看历史：

```powershell
git log --oneline --decorate --graph
```

## GitHub

创建公开仓库时：

- 仓库名使用 `recsys-research-training-liming`。
- 可见性选择 `Public`。
- 本地已经有 `README.md` 和 `.gitignore`，远程创建时不要再初始化这些文件。

连接远程仓库：

```powershell
git remote add origin https://github.com/llemmm/recsys-research-training-liming.git
git push -u origin main
```

推送后在未登录状态打开仓库链接，确认公开访问和文件完整性。

## VS Code 与 PowerShell

- 使用 VS Code 阅读项目结构、搜索函数和查看 Git 修改。
- 在运行命令前用 `pwd` 确认当前位置。
- 报错记录至少包含命令、完整错误、环境版本和已经尝试的方法。

## Zotero

- 建立与研究主题对应的分类目录。
- 保存题目、作者、年份、会议/期刊、链接和标签。
- 将文献卡片与 `paper_reading.md` 中的精读记录对应起来。
