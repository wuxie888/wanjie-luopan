# 排错指南

## Codex 没有识别 `$wanjie-luopan`

先检查入口文件：

```bash
test -f "$HOME/.codex/skills/wanjie-luopan/SKILL.md" && echo "Skill entry found"
```

如果没有输出，检查是否错误地嵌套成：

```text
~/.codex/skills/wanjie-luopan/wanjie-luopan/SKILL.md
```

修正目录后开启一个新的 Codex 任务。已经打开的任务通常不会热刷新 Skill 列表。

## 更新后仍然表现得像旧版本

对比源码和安装副本：

```bash
diff -qr wanjie-luopan "$HOME/.codex/skills/wanjie-luopan"
```

如果存在差异，重新同步：

```bash
rsync -a --delete wanjie-luopan/ "$HOME/.codex/skills/wanjie-luopan/"
```

然后开启新任务。不要把重复执行安装命令等同于已经加载新版本。

## 找到的项目不够新

万界罗盘不内置固定项目数据库。时效性取决于当前任务是否能访问 GitHub、项目官网或其他原始来源。

在请求中明确写：

```text
所有维护状态、Release、许可证和指标都使用本次现场核验结果，并标注检查日期。
```

如果来源不可访问，结果应该标记受阻或降级，而不是把旧信息写成当前事实。

## 候选很多，但结论不清楚

要求停在同一证据层级：

```text
先只使用 E1 仓库表面证据筛选，保留 3–8 个候选。
不要进入克隆和运行。
```

如果需要继续比较，再单独要求星图；只有最终 1–2 个项目才值得进入最小运行验证。

## 评分脚本报错

脚本接受 JSON 数组，或包含 `candidates` 数组的对象：

```json
{
  "candidates": [
    {
      "name": "Example",
      "url": "https://github.com/example/project",
      "repo_exists": true,
      "has_code": true,
      "license_status": "permissive",
      "core_dependency_available": true,
      "relevance": 4,
      "novelty": 3,
      "substance": 4,
      "activity": 3,
      "documentation": 4,
      "usage_evidence": 3,
      "legal_safety": 4
    }
  ]
}
```

所有评分字段必须是 0–5 的数字。硬门槛会覆盖总分：空壳、不相关、许可证冲突或核心依赖失效的项目仍会被排除。

## 没有运行证据却出现“已经可用”

要求重新按 E0–E3 整理：

- E0：线索
- E1：仓库表面
- E2：源码、测试和 Issue
- E3：本次环境运行

只有记录了明确环境、准确命令和结果，才能写成本次 E3。一个示例跑通也不等于生产可用。

## 仍然无法解决

提交问题时请包含：

- Codex 与操作系统版本
- Skill 安装路径和目录树
- 完整请求
- 已访问和受阻的来源
- 预期结果与实际结果
- 是否发生克隆、安装或运行

不要附带 API Key、Cookie、个人访问令牌或私有仓库内容。
