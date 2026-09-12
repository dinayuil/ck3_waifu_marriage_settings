# 纸片人婚姻设置 / Waifu Marriage Settings

CK3 mod，为纸片人角色定制婚姻行为，并兼容婚舰通用库的誓约系统。

## 前置模组

| 模组 | 必需 |
|------|------|
| 二向箔核心库 / Anime Core Lib | ✅ 必须 |
| 婚舰通用库 / Hunjian Common Lib | ✅ 必须 |
| 幻萌入侵 mod（战舰少女相关扩展包） | ⬜ 可选 |

## 功能

### 1. 纸片人婚姻设置（游戏规则，默认开启）
满足 `waifu_portrait_trigger` 的纸片人角色**只能**与同为纸片人的角色结婚或订婚，非纸片人角色无法与其结婚。可在游戏规则中关闭。

### 2. 纸片人同性婚姻（游戏规则，默认开启）
纸片人**无视宗教教义和性别限制**，可与同性角色结婚；若同时开启“纸片人只能与纸片人结婚”，则仅限纸片人之间。AI 不会因为信仰不认可同性婚姻而对已婚同性纸片人夫妻发起离婚。可在游戏规则中关闭。

### 3. 誓约关系继承（需要婚舰通用库）
玩家角色死亡、继承人接管后，**原有的所有誓约关系（hunjian/shiyuezhe）自动转移**给继承人。若同时使用 WSG 扩展包，继承人还会获得对应数量的**誓约纪念章（tidu_ring）**特质 XP。

### 4. 拒绝纸片人参战召唤豁免（游戏规则，默认开启）
当纸片人盟友**通过原版召唤交互**（同盟召唤 `call_ally_interaction`、家族召唤、王朝召唤）发起战争并召唤玩家参与时，**玩家拒绝不会受到任何惩罚**（无名声损失、无负面好感修正）。可在游戏规则中关闭。

> 注：本机制**只作用于原版召唤交互**（通过覆盖 `call_ally.0101` 事件撤销惩罚）。功能 8 的「召唤婚舰参战」是**独立交互**，不经过本机制，它自身就不施加任何拒绝惩罚（两个方向都是）。

### 5. 婚舰姊妹好感（游戏规则，默认开启）
同一玩家的所有「婚舰」（hunjian）角色之间获得**大量好感加成（+100）**，显著降低婚舰互相谋害、结仇或决斗的概率。可在游戏规则中关闭。

### 6. 婚舰主人好感（游戏规则，默认开启）
婚舰与其主人之间获得**大量互惠好感加成（+100）**，方向对称；玩家死亡、继承人接管后也会自动补上，避免继承后好感丢失。可在游戏规则中关闭。

### 7. 拓宽可誓约条件
- **可誓约条件已拓展**：世界上任何地方、符合好感/舰种条件、且**还没被誓约**的纸片人（不管是不是封臣、自己是不是也有婚舰）都**仍然可以手动单个誓约**。
- **批量功能限定领地内**：「统计可誓约数量」的面板/列表、集体誓约决策、以及顶部“誓约一位新的{}”圆圈提醒，只扫描玩家**领地内**（廷臣/宾客+封臣）符合条件的纸片人，避免全图遍历卡顿。
- **顶部圆圈种类已拓展**：顶部“誓约一位新的战舰少女”圆圈提醒的可誓约纸片人种类**不再限于舰娘**，而是覆盖玩家领地内所有符合条件的纸片人。
- **集体誓约新增「其他/杂项」分类**：集体誓约决策除了原有的 6 个舰种外，新增第 7 个「其他」选项，用于收录满足 `waifu_portrait_trigger`、但不属于那 6 类舰种的纸片人（例如绫地宁宁等彩蛋/杂项角色），避免它们出现在顶部圆圈却无法在金框中集体誓约。

### 8. 召唤婚舰参战（游戏规则，默认开启）
新增一个**独立交互**：在战争中直接召唤誓约的婚舰/纸片人参战。**不覆盖任何原版规则**。

- **无视信仰与血缘**：不同于原版的「召唤家族成员」，本交互只认誓约关系（`hunjian`/`shiyuezhe`），异教、异族、非亲非故的婚舰都能召唤。
- **无需结盟**：不依赖同盟关系，直接把参战选项加入战争。
- **零成本**：不消耗威望/虔诚/金币。
- **拒绝无惩罚**：本交互自身的 `on_decline` **不施加任何惩罚**，因此**两个方向**被拒绝都不会有负面好感或名声损失。这与功能 4 的「拒绝纸片人参战召唤豁免」是**两套互相独立的机制**——那个只撤销**原版**召唤交互的惩罚，本交互不读取它，即使把该规则关闭，本交互依然无惩罚。
- **反向可选**：可让婚舰（AI）也召唤你参战。
- **可召唤封臣**：即使是你的**封臣**也能被召唤（这是与原版「召唤家族成员」的一个重要差异——原版会排除自己的封臣）。
- **顶部提醒**：打仗时，顶部「当前局势」列表会出现与「召唤盟友 / 家族成员 / 宗族成员」并列的**「召唤婚舰」**提示，点击即可打开召唤窗口。
- 被召唤者必须是**统治者（有兵）**；你自己必须是**战争领袖**（正在打仗）；不能召唤自己的**领主或更高者**。

游戏规则「召唤婚舰参战」共四档：

| 选项 | 效果 |
|------|------|
| 双向（默认） | 玩家可召唤婚舰，婚舰也可召唤玩家 |
| 仅玩家召唤婚舰 | 只有你能召唤婚舰，婚舰不会召唤你 |
| 仅婚舰召唤玩家 | 只有婚舰能召唤你，你不能召唤婚舰 |
| 关闭 | 关闭该交互 |


## 文件结构

```
common/
  game_rules/              游戏规则定义
  character_interactions/  “召唤婚舰参战”交互（新增，不覆盖任何原版交互）
  scripted_triggers/       覆盖婚姻相关触发器（同性婚姻判定、可誓约范围）+ 召唤方向判定
  scripted_effects/        婚舰互惠好感相关脚本效果
  opinion_modifiers/       婚舰姊妹好感修正
  script_values/           覆盖可誓约数量统计（含封臣、自为主人的纸片人）
  decisions/               覆盖集体誓约决策（遍历玩家领地内的纸片人）
  important_actions/       覆盖“誓约一位新的{}”顶部提醒；新增“召唤婚舰”顶部提醒
  on_action/               玩家死亡时的誓约继承钩子，以及婚舰好感维护钩子
events/
  waifu_call_to_arms_events.txt   覆盖 call_ally.0101，实现拒绝参战豁免
localization/
  english/                 英文本地化
  simp_chinese/            简体中文本地化
```

## 技术说明

- 覆盖 `marriage_interaction_valid_target_trigger`：添加纸片人婚姻设置检查
- 覆盖 `allowed_to_marry_same_sex_trigger`：为纸片人豁免信仰同性婚姻限制，阻止 AI 发起离婚
- 新增 `waifu_same_sex_can_marry_trigger` / `waifu_same_sex_could_marry_trigger`：专供同性纸片人婚姻使用的触发器
- 新增 `on_death` 钩子：转移誓约关系及纪念章特质
- 覆盖 `call_ally.0101` 事件：拒绝纸片人参战召唤后，撤销名声损失和好感修正
- 覆盖 `can_be_oath_by_ACTOR_shown`：拓宽可誓约范围（含封臣、自为主人的纸片人）
- 覆盖 `action_send_shiyue`（Important Action）与 `hm_set_second_oath_interaction`：顶部“誓约一位新的{}”圆圈提醒改为覆盖所有纸片人（含封臣、自为主人的），点击后列表也列出全部可誓约纸片人（需你的 mod 在 HM/WSG 之后加载；不依赖 HM 也能用）
- 覆盖 `to_*_shiyue_interaction_number` 与 `group_wedding_decision`：统计和集体誓约都改为遍历玩家领地内（廷臣/宾客+封臣）的纸片人
- 新增 `waifu_misc_pledgeable_trigger` 与 `to_other_shiyue_interaction_number`：为集体誓约决策增加「其他/杂项」分类，收录不属于 6 类舰种的纸片人（如绫地宁宁等彩蛋角色）
- 新增 `waifu_hunjian_sibling_opinion` 规则 + `on_set_relation_hunjian` 钩子：婚舰之间互加好感修正
- 新增 `waifu_hunjian_master_opinion` 规则：主人与婚舰互加好感，并在继承时自动补上，避免好感丢失
- 新增 `waifu_call_to_war_interaction`：**全新交互**，通过 `interface = call_ally` + `special_interaction = call_ally_interaction` 复用原版「选择参战战争」界面；在 `on_accept` 里内联执行 `add_attacker` / `add_defender` 参战，**不触发任何 `call_ally.01xx` 事件**，故零覆盖、零冲突
- 新增 `waifu_call_to_war` 游戏规则（双向 / 仅玩家召唤婚舰 / 仅婚舰召唤玩家 / 关闭）+ `waifu_call_to_war_player_direction_trigger` / `waifu_call_to_war_reverse_direction_trigger` 方向判定触发器
- 反向（AI 婚舰召唤玩家）：通过 `ai_targets = { ai_recipients = scripted_relations }` 精确命中誓约对象（`hunjian` / `shiyuezhe` 是 scripted relation），并用 `ai_will_do` 按规则开关及「只召唤玩家」过滤
- 新增 `waifu_action_can_call_waifu`（Important Action）：在顶部「当前局势」列表新增与「召唤盟友 / 家族成员 / 宗族成员」并列的「召唤婚舰」提醒，遍历玩家的 `hunjian` / `shiyuezhe` 关系，并用 `is_character_interaction_valid` + `can_join_war_liege_vassal_check_trigger` 过滤；仅当规则允许「玩家方向」时创建
- **刻意允许召唤自己的封臣**：原版 `call_house_member_to_war_interaction` 把 `NOT = { target_is_liege_or_above = scope:actor }` 写在 `scope:recipient` 上，等价于「对方不能是我的封臣」，因此排除自己的封臣；本 mod 把它改写到 `scope:actor` 上（`NOT = { target_is_liege_or_above = scope:recipient }`），只排除自己的**领主或更高者**，所以封臣婚舰同样可以召唤

## 兼容性

- 不修改原版婚姻互动本体，兼容性较好
- **「召唤婚舰参战」是全新交互（`waifu_call_to_war_interaction`），不覆盖 `call_ally_interaction` / `call_house_member_to_war_interaction` / `call_dynasty_member_to_war_interaction` 中的任何一个，也复用了原版 UI，与其他 mod 冲突风险极低**
- 若其他 mod 也覆盖 `marriage_interaction_valid_target_trigger` 或 `allowed_to_marry_same_sex_trigger`，需手动合并
- 本 mod 文件名以 `w` 开头，字母序靠后，会覆盖同名触发器的其他定义（如 `free_marriage`）
- 若启用「幻萌入侵」mod，请将本 mod 置于其**下方加载**，否则本 mod 对顶部圆圈/交互的覆盖无效（本 mod 不依赖幻萌入侵，未加载时其余功能照常）
