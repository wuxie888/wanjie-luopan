# 上手指南

这份指南只覆盖万界罗盘当前真实存在的形态：一个安装在本机的 Codex Skill。

## 前置条件

- 已安装支持本地 Skills 的 Codex
- 已安装 Git
- macOS 或 Linux 可使用 `rsync`
- 能访问 GitHub 或其他待核验的公开来源

万界罗盘不自带 GitHub 搜索服务。它会使用当前 Codex 环境里可用的 GitHub、浏览器、网络和本地工具。

## 第一次安装

在你希望保存源码的位置执行：

```bash
git clone https://github.com/wuxie888/wanjie-luopan.git
mkdir -p "$HOME/.codex/skills/wanjie-luopan"
rsync -a --delete wanjie-luopan/wanjie-luopan/ "$HOME/.codex/skills/wanjie-luopan/"
```

安装后的关键结构应为：

```text
~/.codex/skills/wanjie-luopan/
  SKILL.md
  agents/openai.yaml
  references/
  scripts/
```

不要出现下面这种多嵌套一层的结构：

```text
~/.codex/skills/wanjie-luopan/wanjie-luopan/SKILL.md
```

## 让 Skill 生效

本地 Skill 列表通常不会在已经打开的任务中热刷新。安装或更新后：

1. 保留当前工作
2. 新建一个 Codex 任务
3. 在新任务中调用 `$wanjie-luopan`

## 第一次成功

复制下面的请求：

```text
使用 $wanjie-luopan 帮我寻找适合 macOS 本地运行、用于研究语音转文字的开源项目。
只做快速发现，不安装运行。
```

成功不是“Skill 被识别”就结束。你应该拿到：

- 3–8 个真实候选
- 每个候选的原始链接和真实形态
- 推荐理由、证据等级和主要风险
- 已验证、未验证和本次未执行的事项
- 一个继续深查或比较的自然下一步

默认路引不应克隆、安装、下载模型或运行候选代码。

## 更新

在最初 clone 的源码目录中执行：

```bash
git pull --ff-only
rsync -a --delete wanjie-luopan/ "$HOME/.codex/skills/wanjie-luopan/"
```

然后开启一个新的 Codex 任务。

如果你不确定当前目录是源码根目录，先确认其中同时存在 `README.md` 和 `wanjie-luopan/SKILL.md`。

## 检查源码与安装副本

在仓库根目录执行：

```bash
diff -qr wanjie-luopan "$HOME/.codex/skills/wanjie-luopan"
python3 -m unittest discover -s wanjie-luopan/scripts -p 'test_*.py' -v
```

`diff -qr` 没有输出表示两个目录一致。

## 卸载

关闭正在使用该 Skill 的任务，然后删除：

```text
~/.codex/skills/wanjie-luopan
```

卸载本地 Skill 不会自动删除你另外保存的源码 clone。

## 权限与安全

- 普通发现请求默认只读公开来源
- 克隆、安装和执行代码只在你明确要求最小运行验证时发生
- 登录、付费、密钥、发送、发布、部署和生产数据操作需要单独确认
- 运行陌生仓库前应使用临时或用户指定目录，并记录准确命令和恢复方法
