# ReqCheck

AI 写代码前的需求检查器。

ReqCheck 是一个 Codex / Claude skill，用来在 AI 写代码前，把模糊的产品想法整理成可以开发的需求说明。

它主要给不懂代码、但需要用 AI 做产品和功能的人使用。用户可以只说一句很粗的需求，比如“帮我做一个客户导入功能”“把这个页面做得像竞品一样”，ReqCheck 会先帮用户想清楚那些很容易在后面变成 bug 的产品问题。

## 为什么需要它

很多 AI 写代码失败，不是代码阶段才失败。

问题经常出现在更早的需求阶段：

- 这条数据什么时候才算真正生效？
- 用户点取消之后，要不要留下记录？
- 新入口和旧入口是真的一样，还是只是看起来一样？
- 一个慢一点返回的旧请求，会不会覆盖用户刚刚做的新操作？
- 这个改动到底怎么让真实用户用到？

ReqCheck 的作用，就是让 AI 在写代码前先停一下，把这些隐藏判断用普通话问清楚。

## 快速示例

用户：

```md
帮我做一个客户导入功能。
```

不用 ReqCheck 时：

```md
AI 可能直接开始写上传按钮。
```

使用 ReqCheck 时：

```md
ReqCheck 会先帮你想清楚：

1. 用户上传后，是直接加入客户列表，还是先看到一页确认名单？
2. 文件里有重复客户时，是自动跳过，还是提醒用户决定？
3. 只导入成功一部分时，用户要不要看到成功和失败的明细？
```

区别在这里：第二种会提前避免误导入、重复客户、部分失败说不清楚、用户不知道怎么恢复这些真实问题。

## ReqCheck 会检查什么

ReqCheck 内置了一组从真实 AI 辅助开发 bug 里抽出来的模式。

| 模式 | 避免的问题 |
| --- | --- |
| 临时结果和正式结果 | 用户只是预览或编辑一半，数据却已经生效 |
| 新入口复用旧入口 | 新入口错误复用旧入口的校验、超时、错误处理 |
| 同一数据多处展示 | 首页、详情页、导出、通知、AI 总结里的数据不一致 |
| 页面上下文继承 | 新记录保存到了错误的日期、项目、门店、客户或角色 |
| 业务时间和创建时间 | 报表用录入时间代替真实发生时间 |
| 完成、过期、补确认 | 系统不知道一件事算完成、过期，还是仍在等待 |
| 非默认环境 | 长文案、小屏、拒绝权限、深色模式、多语言路径出问题 |
| 旧请求覆盖新操作 | 慢一步返回的旧数据覆盖用户刚刚做的新修改 |
| 失败重试和加载状态 | 无限 loading、重复重试、页面闪烁、重复提交 |
| 权限拒绝和局部可用 | 用户拒绝一个权限后，整个产品被卡住 |
| 发布方式和版本 | 用户、审核人员、前端、后端看到的不是同一个版本 |
| 页面承诺和真实行为 | UI 或协议写了某个承诺，但后端并没有真的做到 |

## 安装

### Codex

把 skill 目录复制到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/reqcheck ~/.codex/skills/reqcheck
```

如果 skill 列表没有立刻刷新，重启 Codex 或打开一个新会话。

### Claude Code

把 skill 目录复制到 Claude skills 目录：

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude/reqcheck ~/.claude/skills/reqcheck
```

也可以导入打包文件：

```text
packages/reqcheck.skill
```

## 使用方法

```md
用 reqcheck 先帮我澄清需求，不要直接写代码。

我的需求是：帮我做一个客户导入功能。
```

ReqCheck 会输出：

- 可能的目标
- 最小可用版本
- 完整版本
- 风险
- 这次不做什么
- 不做的话可能出什么问题
- 最多 3 个关键问题
- 用户确认后，整理成开发需求说明

## 示例

可以看这些文件：

- [客户导入](examples/customer-import.md)
- [订阅付费墙](examples/subscription-paywall.md)
- [日历事件](examples/calendar-event.md)
- [管理后台看板](examples/admin-dashboard.md)
- [AI 总结功能](examples/ai-summary-feature.md)

每个示例都包含：

1. 原始模糊需求
2. ReqCheck 会问的问题
3. 开发需求说明大纲

## 评估方式

ReqCheck 不是用来评估代码写得好不好，而是评估 AI 在写代码前有没有帮用户想清楚关键产品问题。

一个好的 ReqCheck 输出应该：

- 每次最多问 3 个问题
- 在产品规则没清楚前，不直接问数据库、API、字段这些问题
- 如果缩小范围，要写清楚这次不做什么
- 解释现在不做可能带来什么问题
- 至少抓住一个隐藏的状态、数据、上下文、失败、权限或发布问题
- 用户确认后，能输出一份可以交给 coding agent 执行的开发说明

评估样例见：[evals/prompts.json](evals/prompts.json)

## 项目结构

```text
reqcheck/
  README.md
  README.zh-CN.md
  skills/
    codex/reqcheck/SKILL.md
    claude/reqcheck/SKILL.md
  packages/
    reqcheck.skill
  docs/
    patterns.md
  examples/
  evals/
```

## License

MIT
