<p align="center">
  <img src="assets/logo-lockup.svg" alt="万界罗盘" width="600">
</p>

<p align="center">为每个想法找到方向，在开源万界中留下自己的星图</p>

万界罗盘是个人开源项目发现与研究系统。它把一个模糊方向转成有真实来源、证据分层和明确风险的项目短名单，并允许用户按需继续比较、深查和运行验证。

当前仓库首先交付可全局调用的 Codex Skill。持续发现、更新追踪和个人项目库属于后续产品路线，尚未伪装成已实现功能。

## 它解决什么

普通搜索可以返回关键词相似的仓库，却很难稳定回答：

- 哪些是真正存在且有实质代码的项目
- 哪些值得现在打开
- README、源码、社区和本地运行分别证明了什么
- 哪些项目只是热度高，哪些真的适合继续研究
- 下一步应该比较、深查还是运行哪一个

万界罗盘先过许可证、相关性、代码实质和依赖等硬门槛，再对候选进行证据化排序。Star 只作为热度信号，不作为质量证明。

## 当前 Skill

机器标识：`wanjie-luopan`

```text
路引（快速发现）
  → 星图（候选对比）
    → 开卷（仓库深查）
      → 最小运行验证
```

- **路引**：从一个方向建立候选池，返回 3–8 个值得看的项目
- **星图**：统一证据口径，比较候选和相邻项目关系
- **开卷**：检查真实文件、入口、依赖、维护、Issues、Release 和许可证
- **最小运行验证**：只对最终 1–2 个项目执行隔离的核心工作流

用户只说“找项目”时，默认停在路引，不自动克隆、安装或运行代码。

## 产品语言

| 名称 | 含义 | 状态 |
| --- | --- | --- |
| 路引 | 主动寻找并生成项目短名单 | 已实现 |
| 星图 | 候选对比与项目生态关系 | 部分实现 |
| 开卷 | 单项目完整研究 | 已实现 |
| 巡天 | 持续发现新项目与重要变化 | 规划中 |
| 星历 | 项目更新与维护轨迹 | 规划中 |
| 藏卷 | 个人收藏与研究库 | 规划中 |
| 舆图 | 跨任务项目知识底座 | 规划中 |

## 使用

安装为全局 Skill 后，可以直接提出：

```text
使用 $wanjie-luopan 帮我寻找适合 macOS 本地运行的开源录屏项目
```

也可以自然表达：

```text
帮我找一批值得看的本地 AI 项目
比较这几个 GitHub 仓库
完整看下这个项目值不值得用
把最终两个候选跑一下最小工作流
```

## 安装

将 `wanjie-luopan` 目录复制到 Codex Skills 目录：

```text
~/.codex/skills/wanjie-luopan
```

Skill 不绑定某个浏览器或 GitHub 连接器，会根据当前环境选择可验证的官方页面、API、项目文档和本地工具。

## 验证

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py wanjie-luopan
python3 -m unittest discover -s wanjie-luopan/scripts -p 'test_*.py' -v
```

评分脚本仅使用 Python 标准库：

```bash
python3 wanjie-luopan/scripts/score_candidates.py candidates.json --pretty
```

## 仓库结构

```text
wanjie-luopan/
  SKILL.md
  agents/openai.yaml
  references/
  scripts/
product-docs/
test-results/
assets/
LICENSE
```

## 当前边界

- 已完成 Skill 内核、评分脚本、4 项回归测试和一次独立前向测试
- 当前证据证明工作流可用，不代表所有搜索主题都已达到同样质量
- 巡天、星历、藏卷、舆图尚未实现

## 许可证

本项目采用 [MIT License](LICENSE)。

更完整的产品定义和品牌语言见 [产品文档](product-docs/00_项目总览.md) 与 [品牌语言系统](product-docs/05_品牌语言系统.md)。
