# OS Lab Tutor

**简体中文** · [English](README-en.md)

## 用途

面向操作系统实验的 AI 导师，内置 ChCore Lab1、Lab2 和 Lab3 指引。作为一个 skill（一组供 AI 工具读取的指导文件），它帮助你理解实验、独立完成代码和报告，培养分析与调试能力。

## 特性

- **逐步推进**：按实验讲义与任务依赖安排进度，每次聚焦一个任务。
- **按需讲解**：解释具体概念与命令，提供由你执行的 GDB 调试指引。
- **自主完成**：你编写代码、报告并修复问题，导师按需解释和引导。
- **Lab1 辅助**：读取材料与已提交的尝试，由你运行命令和调试。
- **Lab2 实现思路辅导**：可以询问 TODO 函数的实现思路、需要哪些步骤，以及每一步做什么、为什么需要。导师可结合现有接口和数据结构讲解，但不提供代码、伪代码或逐行照抄的文字实现，也不直接定位和修复你的代码错误。
- **Lab2 操作支持**：导师可运行已有编译和测试、解释输出、导出真实日志并打包提交材料。你负责核心 TODO 和代码修改，GDB 仍由你操作。修订后的 Lab2 保留练习1的 `split_chunk`、`merge_chunk`，练习4的 `query_in_pgtbl`，以及练习10中 `handle_trans_fault` 的三处填空，共4个函数、6处填空。练习9的 `find_vmr_for_va` 已由教师补全。思考题5、6和挑战题7、11无需完成，其余相关代码已提供。以现有基础评分项合计100分为完成标准，提交代码和真实对话，不要求实验报告。环境安装和修复按课程现有要求处理。
- **Lab3 操作支持**：导师可讲解实现思路、运行已有编译和测试、解释输出、导出真实日志并打包提交材料。你负责核心 TODO 和代码修改，GDB 由你操作。练习 1 在 `sys_create_cap_group` 中初始化权利组并处理失败情况。练习 2 在 `create_root_thread` 中设置 ELF 段的映射权限。练习 3 在 `init_thread_ctx` 中初始化线程上下文。练习 5 填写异常向量表 `el1_vector`，练习 6 在 `exception_enter` 和 `exception_exit` 中保存和恢复通用寄存器。共 3 个 C 函数、1 张异常向量表和 2 个汇编宏，每处一个填空。五项评分各 20 分，合计 100 分为完成标准。提交修改后的代码和真实 AI 对话记录，无需实验报告。环境安装和修复按课程现有要求处理。

当前开发版本为 **0.7.19-dev**，尚未发布版本标签。

## 安装

先安装 [Node.js](https://nodejs.org/) 22.20 或更高版本，再运行：

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g
```

该命令通过 [Skills CLI](https://github.com/vercel-labs/skills) 安装本仓库的 `tutor`，按提示选择 AI 工具。`-g` 表示所有项目可用；去掉它则只安装到当前项目。

安装后新建对话，选择 `tutor` 技能开始。在 Codex 中需主动选择技能或输入 `$tutor`，例如：

```text
$tutor 带我学习 ChCore Lab2，从当前进度开始。
```

基于 [TuTor](https://github.com/kevinnio/tutor) · [MIT 许可证](LICENSE)

## 课程项目接入

Lab1 使用 `templates/AGENTS.lab1.md` 和 `templates/CLAUDE.lab1.md`，Lab2 使用对应的 `templates/AGENTS.lab2.md` 和 `templates/CLAUDE.lab2.md`。课程维护者将它们分别放到实验目录的 `AGENTS.md` 和 `CLAUDE.md` 中。这些入口会要求 AI 工具读取完整技能和当前实验指引。

Lab2 需要包含 `references/lab2-guide.md` 的技能副本。使用课程提供的本地新版时，入口支持直接读取同级 `DyingCoderLin_OS-Lab-Tutor` 仓库。远端安装命令获取的是远端内容，本地改动需要同步到远端后才会随该命令安装。

Lab3 使用 `templates/AGENTS.lab3.md` 和 `templates/CLAUDE.lab3.md`，搭配[实验三教学指南](references/lab3-guide.md)。
