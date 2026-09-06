# 纸片人婚姻设置 / Waifu Marriage Settings

CK3 mod，为纸片人角色定制婚姻行为，并兼容婚舰通用库的誓约系统。

## 前置模组

| 模组 | 必需 |
|------|------|
| 二向箔核心库 / Anime Core Lib | ✅ 必须 |
| 婚舰通用库 / Hunjian Common Lib | ✅ 必须 |
| WSG mod（战舰少女相关扩展包） | ⬜ 可选 |

## 功能

### 1. 纸片人婚姻设置（游戏规则，默认开启）
满足 `waifu_portrait_trigger` 的纸片人角色**只能**与同为纸片人的角色结婚或订婚，非纸片人角色无法与其结婚。可在游戏规则中关闭。

### 2. 纸片人同性婚姻（游戏规则，默认开启）
纸片人**无视宗教教义和性别限制**，可与同性角色结婚；若同时开启“纸片人只能与纸片人结婚”，则仅限纸片人之间。AI 不会因为信仰不认可同性婚姻而对已婚同性纸片人夫妻发起离婚。可在游戏规则中关闭。

### 3. 誓约关系继承（需要婚舰通用库）
玩家角色死亡、继承人接管后，**原有的所有誓约关系（hunjian/shiyuezhe）自动转移**给继承人。若同时使用 WSG 扩展包，继承人还会获得对应数量的**誓约纪念章（tidu_ring）**特质 XP。

### 4. 拒绝纸片人参战召唤豁免（游戏规则，默认开启）
当纸片人盟友发起战争并召唤玩家参与时，**玩家拒绝不会受到任何惩罚**（无名声损失、无负面好感修正）。可在游戏规则中关闭。

### 5. 婚舰姊妹好感（游戏规则，默认开启）
同一玩家的所有「婚舰」（hunjian）角色之间获得**大量好感加成（+100）**，显著降低婚舰互相谋害、结仇或决斗的概率。可在游戏规则中关闭。

### 6. 婚舰主人好感（游戏规则，默认开启）
婚舰与其主人之间获得**大量互惠好感加成（+100）**，方向对称；玩家死亡、继承人接管后也会自动补上，避免继承后好感丢失。可在游戏规则中关闭。

### 7. 拓宽集体誓约范围
集体誓约不再只限玩家的**廷臣/宾客**，而是覆盖全世界**所有符合条件的在世纸片人**（好感达标/特定舰种、未被他人誓约），包括玩家的**封臣**以及**自己也是主人（有自己的婚舰）**的纸片人。「统计可誓约数量」的面板/列表和集体誓约决策都一并拓展。

## 文件结构

```
common/
  game_rules/              游戏规则定义
  scripted_triggers/       覆盖婚姻相关触发器（同性婚姻判定、可誓约范围）
  scripted_effects/        婚舰互惠好感相关脚本效果
  opinion_modifiers/       婚舰姊妹好感修正
  script_values/           覆盖可誓约数量统计（含封臣、自为主人的纸片人）
  decisions/               覆盖集体誓约决策（遍历全世界在世纸片人）
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
- 覆盖 `to_*_shiyue_interaction_number` 与 `group_wedding_decision`：统计和集体誓约都改为遍历全世界在世纸片人
- 新增 `waifu_hunjian_sibling_opinion` 规则 + `on_set_relation_hunjian` 钩子：婚舰之间互加好感修正
- 新增 `waifu_hunjian_master_opinion` 规则：主人与婚舰互加好感，并在继承时自动补上，避免好感丢失

## 兼容性

- 不修改原版婚姻互动本体，兼容性较好
- 若其他 mod 也覆盖 `marriage_interaction_valid_target_trigger` 或 `allowed_to_marry_same_sex_trigger`，需手动合并
- 本 mod 文件名以 `w` 开头，字母序靠后，会覆盖同名触发器的其他定义（如 `free_marriage`）
