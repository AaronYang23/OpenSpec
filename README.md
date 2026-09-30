# OpenSpec

本仓库用于记录 OpenSpec 的使用方法，不是需要执行 `openspec init` 的代码项目。OpenSpec 可以在代码项目中初始化，也可以将规格放在独立的 store 中；首次体验先试项目内的标准方式。

## 开始使用

确认 CLI 已安装：

```bash
openspec --version
openspec --help
```

进入实际代码项目（建议先切到用于尝试的分支），再为 Codex 初始化 OpenSpec：

```bash
cd /path/to/your-project
openspec init --tools codex
git status --short
```

初始化会在代码项目中生成 OpenSpec 和 Codex 相关文件。先查看新增文件，再决定是否将这套方式留在项目中；本笔记仓库不需要初始化。

## 一次变更的流程

以下命令均在已经初始化的代码项目根目录执行，`add-user-search` 只是变更名称示例：

```bash
openspec new change add-user-search
openspec status --change add-user-search
```

向 Codex 描述需求，请它围绕该变更编写提案、规格、设计和任务；确认内容后再按任务实施。默认 `spec-driven` 流程的产物顺序为 `proposal → specs → design → tasks`，可用 `openspec status --change add-user-search` 查看进度。

在实施前校验变更内容，实施并验证完成后归档：

```bash
openspec validate add-user-search --strict
openspec archive add-user-search
```

归档会将完成的变更合并进主规格。具体选项以当前安装版本的 `openspec <command> --help` 为准。

## 独立存放规格

如果以后不希望 OpenSpec 文件进入代码仓库，可以创建独立 store，并在命令中用 `--store` 指定它：

```bash
openspec store setup my-project --path /path/to/spec-store
openspec new change add-user-search --store my-project
```

这种方式不会自动将代码项目与 store 关联；让 Codex 处理变更时，需要同时提供代码和规格的上下文。可先体验项目内初始化，再决定是否切换。