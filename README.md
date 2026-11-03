# Mafia Ops SOP · 欧美女频 Mafia 有声书 YouTube 全自动运营迭代库

三个人、N 个频道、一套 SOP、每天迭代。

## 这是什么

一个给 YouTube 欧美女频 Mafia 有声书频道用的**运营操作系统**：

- `sop/` —— 沉淀下来的标准操作规范（本地化、标题、成稿、封面、发布、数据迭代）
- `skills/` —— 每个自动化任务一个 Skill，Agent 照着干，不发挥
- `channels/` —— 每个频道一个目录，每支视频一个目录：标题、封面、选题、成稿、公开数据
- `data/daily/` —— 每天的公开数据投喂（标题、封面、播放、点赞、评论）
- `reports/` —— AI 每天的迭代报告：发现了什么、改了什么、为什么
- `rules.json` —— 事件 → 处理规则（谁触发、谁来干、要不要人拍板）
- `DECISIONS.md` / `REJECTED.md` —— 定了的事 / 定了不做的事（只记人亲口拍板的）

## 架构（学 @Khazix0918）

```
事件（每天定时 / 有人提交数据 / 新视频发布）
  → rules.json 查规则
  → skills/ 里对应的 Skill 干活
  → 结果进 reports/，数据沉淀
  → 只有这几类找人"批奏折"：选题方向大改、SOP 规则变更、对外发布
```

人的注意力是最贵的资产。Agent 自己能处理的，自己处理完上线；
拿不准的，才推到人面前，一次点完。

## 数据原则

**只用公开数据**：视频标题、封面、播放量、点赞、评论数。
不碰 YT Studio 后台，不收集收入等隐私数据。
没人提交数据时，Agent 自己去频道主页看最新一天的作品数据。

## 频道

| 频道 | 地址 | 运营 |
|---|---|---|
| Moonveil Stories | https://youtube.com/@moonveilstories-h1 | 用户本人 |
| Kimi Audiobooks | https://youtube.com/@kimiaudiobooks | 哈基小咪 |
| （待定） | | |
| （待定） | | |

## 快速开始

1. 在 `channels/_template/` 照抄一个新频道目录
2. 每发一支视频，在频道下建 `videos/YYYY-MM-DD-<slug>/`，填 `meta.md`
3. 每天把公开数据填进 `data/daily/YYYY-MM-DD.md`（或等 Agent 自己去抓）
4. 看 `reports/` 里当天的迭代报告；需要拍板的会单独推给你

## 每天的循环

- **08:00（美东）** 定时事件 → `daily-optimizer` Skill 跑全量迭代
- 有人提 PR（新标题/新选题/新数据）→ 按 rules.json 路由到对应 Skill
- 新视频发布 → 自动归档 + 首日数据追踪
