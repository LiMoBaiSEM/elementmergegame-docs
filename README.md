# Element Merge

**五元素 · 一个灵体。**  
A browser puzzle game about feeding, clearing and forging spirits.

> **Proprietary — All rights reserved.**  
> This repository and its contents are **not open source**. No license is granted. You may not copy, modify, redistribute, sublicense or use the code, artwork or game design without prior written permission from the owner.

---

## 1. 项目简介

Element Merge 是一个无需下载、打开即玩的 5×5 五元素合成解谜游戏。玩家在同一行或同一列中，把“相生”的同级元素合并升级，或用“相克”的元素清除障碍，最终合成 Spirit。

游戏把五行生克做成一套可读的棋盘规则，并在其上叠加了关卡、每日挑战、周排行榜、灵体图鉴、融合实验室和互动灵宠。

- **线上游戏**：https://elementmergegame.com/play/
- **完整规则**：https://elementmergegame.com/how-to-play/
- **每日挑战**：https://elementmergegame.com/daily-challenge/
- **灵体图鉴**：https://elementmergegame.com/spirit-codex/
- **互动灵宠**：https://elementmergegame.com/pet/
- **Spirit Garden**：https://elementmergegame.com/spirit-garden/

---

## 2. 核心玩法

棋盘是 5×5。每个元素有颜色、等级和两个职责：

1. **相生**：Wood → Fire → Earth → Metal → Water → Wood  
   两个同级元素如果存在相生关系，且在同一行/列，可以合并；被喂养的一方升 1 级。
2. **相克**：Wood → Earth → Water → Fire → Metal → Wood  
   一个元素可以清除同行/列或相邻的相克目标。

合成两个 Lv5 元素可以锻造一个 **Spirit**，也就是关卡目标。每一关都有步数限制，剩余步数、时间和合并等级共同决定分数与星级。

- **30 个手工关卡**
- **3 档每日挑战**：Casual 60 步 / Standard 45 步 / Expert 35 步
- **Swap**：部分关卡可用交换步数调整棋盘
- **后期法则**：Fire Day / Long Night / Flood / Pure Five / The Crucible

---

## 3. 灵体图鉴：38 个形态

灵体按照元素数量和稀有度分层：

| 稀有度 | 形态 | 数量 |
|---|---|---|
| Common | 单元素 | 5 |
| Uncommon | 双元素 | 10 |
| Rare | 三元素 | 10 |
| Epic | 四元素 | 5 |
| Legendary | 普通五元素 Fivefold | 1 |
| Special | Wind / Thunder / Ice / Light / Dark / Void | 6 |
| Mythic | Omni（全 11 元素） | 1 |

**共 38 个形态。**

### 合成与拆解

- **相生合成**：两个没有共同元素、且存在相生关系的灵体可以融合；元素取并集，生成更高阶灵体。需要 **1 个 Synthesis Agent（特殊合成剂）**，并消耗双方各 1 个副本。
- **相克拆解**：选择一个多元素灵体，再选择一个能“克”其中某个元素的基础灵体作为工具。需要 **1 个 Disassembly Agent（特殊拆解剂）**。拆解消耗目标灵体 1 个副本，得到去掉该元素后的结果；工具灵体作为催化剂不被消耗。
- **特殊元素**：3 个 **Special Shard** 可以合成 1 个指定特殊灵体（Wind / Thunder / Ice / Light / Dark / Void）。

### 材料从哪里来

关键材料不能只靠普通推关获得：

- **任意 26–30 关通关**：+1 Synthesis Agent、+1 Disassembly Agent、+1 Special Shard
- **每周排行榜前 10**：额外获得材料
  - 第 1 名：各 +3
  - 第 2–3 名：各 +2
  - 第 4–10 名：各 +1
  - 每个难度每周只领取一次

这让“挑战难关 + 排行榜”成为高阶合成与特殊元素的真实入口。

---

## 4. 全球 100 个 Omni Spirit

**Omni Spirit** 是全部 11 个元素的集合体。

- 集齐 11 个单元素灵体各 1 个副本后，才可锻造。
- 服务端通过 Supabase `ultimate_claims` 表分配 **1–100** 的永久槽位。
- 第 101 个会被拒绝；锻造失败或售罄不会消耗本地灵体。
- 当前是匿名安装 ID 机制，全球硬上限为 100；要做严格“一人一个”，还需要登录或 Turnstile/风控。

---

## 5. 互动灵宠

Spirit Pet 是一个网页小精灵：

- **拖动**：在 Spirit Garden 舞台内任意拖动，位置保存在本地。
- **跟随鼠标**：输入 `follow` 或点 Follow，它会跟随光标。
- **动作指令**：`dance / jump / spin / sleep / eat / glow / follow / come / wave / hug`，支持中英文关键词。
- **喂养成长**：通关掉落 Spirit Moss；喂食获得 XP，成长阶段为  
  **Wisp → Sprout → Bloom → Doll → Guardian**。
- **小窗口**：支持 380×620 的 compact 模式，可放在桌面角落。

当前动作是本地关键词解析，不是大模型对话；自由自然语言与真正 always-on-top 桌面宠物属于后续桌面应用版本。

---

## 6. 技术栈

- **前端**：单文件 HTML5 + CSS + JavaScript，无框架、无构建依赖
- **游戏页**：`/play/` 是内容页，`/game/` 是实际 iframe（noindex）
- **站点**：静态 SEO 页面、sitemap、robots、Open Graph、JSON-LD
- **托管**：Cloudflare Pages
- **数据**：Supabase
  - 每周排行榜：`weekly_scores` / `weekly_leaderboard` / `submit_weekly_score`
  - 全球终极灵体：`ultimate_claims` / `claim_ultimate` / `ultimate_status`
- **分析**：Google Tag Manager
- **广告**：AdSense 槽位已预留，默认关闭，可在后台开关

本项目不使用服务端渲染，所有关卡和棋盘逻辑都在浏览器内运行。

---

## 7. 隐私

- 无需账号即可游玩。
- 关卡进度、灵体、灵宠成长保存在浏览器 `localStorage`。
- 周排行榜只保存匿名玩家 ID、显示名、分数、难度和周。
- 全球 Omni 槽位保存匿名安装 ID 和槽位号。
- 不收集邮箱、密码或真实姓名。

---

## 8. 路线图

- [x] 30 关 + 后期法则 + Swap
- [x] 三档每日挑战 + 周排行榜
- [x] 灵体收集 + 皮肤 + Spirit Garden
- [x] 全屏 + 五行生克动画
- [x] 38 形态灵体图鉴 + 相生合成 / 相克拆解
- [x] 互动灵宠：拖动 / 指令 / 喂养成长
- [x] 全球 100 个 Omni Spirit
- [ ] Tauri/Electron 桌面灵宠（透明置顶、开机启动）
- [ ] 灵宠自然语言 AI
- [ ] 登录 / Turnstile 严格限量
- [ ] 更多挑战关卡与赛季

---

## 9. 版权与许可

Copyright © 2026 MHK Color / LiMoBai. All rights reserved.

This project is proprietary. **It is not open source.** No permission is granted to use, copy, modify, distribute, sublicense or create derivative works from the code, visual assets, game design or documentation without prior written permission.

For licensing, partnership or press enquiries, please contact the owner through the website: https://elementmergegame.com/about/
