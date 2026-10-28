# OS Lab Tutor

**简体中文** · [English](README-en.md)

## 用途

面向操作系统实验的 AI 导师，内置 ChCore Lab1 指引。作为一个 skill（一组供 AI 工具读取的指导文件），它帮助你理解实验、独立完成代码和报告，培养分析与调试能力。

## 特性

- **逐步推进**：按实验讲义与任务依赖安排进度，每次聚焦一个任务。
- **按需讲解**：解释具体概念与命令，提供由你执行的 GDB 调试指引。
- **自主完成**：你编写代码和报告、运行测试并修复问题；导师不代写答案。
- **只读辅助**：读取材料与已提交的尝试，报告反馈关注核心理解；不修改文件或代跑命令。

## 安装

先安装 [Node.js](https://nodejs.org/) 22.20 或更高版本，再运行：

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g
```

该命令通过 [Skills CLI](https://github.com/vercel-labs/skills) 安装本仓库的 `tutor`，按提示选择 AI 工具。`-g` 表示所有项目可用；去掉它则只安装到当前项目。

安装后新建对话，选择 `tutor` 技能开始。在 Codex 中需主动选择技能或输入 `$tutor`，例如：

```text
$tutor 带我学习 ChCore Lab1，从当前进度开始。
```

基于 [TuTor](https://github.com/kevinnio/tutor) · [MIT 许可证](LICENSE)
