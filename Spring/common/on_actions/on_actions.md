# On actions
On actions是游戏的自动触发入口，用于在游戏发生指定行为时执行效果。
## 文件夹结构格式
On actions文件位于`common/on_actions`中。
## 内容格式
以下是一个On actions文件的示例：
```paradox_script
on_actions = {
    # On action，此处为开始游戏时
    on_startup = {
        # 内容块
        effect = {
            # 作用域
            every_country = {
                if = {
                    limit = {
                        is_ai = no
                    }
                    country_event = Spring.1
                }
            }
        }
    }
}
```
### 内容块
一个 on action 内可使用多个内容块。常见内容块如下。
#### effect
`effect`用于直接执行效果。它适合设置 flag、变量、国家状态，或执行经过筛选后的事件触发。
#### events
`events`用于列出会被触发的事件。事件本身可以继续使用`trigger`控制是否实际执行。
#### random_events
`random_events`用于按权重随机选择事件。
### 作用域
On action被调用时会携带特定作用域。不同 on action 的`ROOT`、`FROM`、`PREV`、`THIS`含义并不相同。编写脚本前应先确认该On action的作用域说明。

TODO
### 可用 On actions
下列列表按原版文档分类整理。不同游戏版本和DLC可能会新增、移除或调整部分On action。实际项目应以当前游戏版本的原版`common/on_actions/_documentation.md`为准。
#### 通用
通用 on actions 主要用于游戏启动、固定周期、特殊军事行为等基础时机。

| On action                       | 说明                                                                       |
|---------------------------------|----------------------------------------------------------------------------|
| `on_startup`                    | 游戏启动或载入时调用。常用于初始化国家、设置全局 flag、建立初始状态。      |
| `on_daily`                      | 每日调用。适合必须每日更新的轻量逻辑。                                     |
| `on_daily_TAG`                  | 指定国家 TAG 的每日调用形式，例如`on_daily_GER`。                          |
| `on_weekly`                     | 每周调用。适合一般状态检查。                                               |
| `on_weekly_TAG`                 | 指定国家 TAG 的每周调用形式，例如`on_weekly_SOV`。                         |
| `on_monthly`                    | 每月调用。适合月度事件、结算和低频检查。                                   |
| `on_monthly_TAG`                | 指定国家 TAG 的每月调用形式，例如`on_monthly_ENG`。                        |
| `on_nuke_drop`                  | 核弹投放时调用。                                                           |
| `on_pride_of_the_fleet_sunk`    | 海军荣耀舰被击沉时调用。                                                   |
| `on_naval_invasion`             | 海军登陆发生时调用。                                                       |
| `on_paradrop`                   | 空降发生时调用。                                                           |
| `on_units_paradropped_in_state` | 单位空降至地区时调用；原版说明指出它按地区触发，而不是按每个空降单位触发。 |

#### 政治
政治类 on actions 用于政变、政府变动、执政党变化、选举任期和和会阶段。

| On action                          | 说明                                                                                       |
|------------------------------------|--------------------------------------------------------------------------------------------|
| `on_coup_succeeded`                | 政变成功时调用。可用于开启选举、调整执政党、设置新政权状态。                               |
| `on_government_change`             | 政府形态发生变化时调用。可用于处理意识形态、国家精神和外交限制。                           |
| `on_ruling_party_change`           | 执政党变化时调用。原版中可用临时变量`old_ideology_token`获取旧意识形态。                   |
| `on_ruling_party_change_immediate` | 执政党变化的旧式即时触发项。原版文档标注为不推荐使用，应优先使用`on_ruling_party_change`。 |
| `on_new_term_election`             | 新任期选举发生时调用。常用于选举事件池。                                                   |
| `on_before_peace_conference_start` | 和会开始前调用。`ROOT`为胜利方，`FROM`为失败方。                                           |
| `on_peaceconference_started`       | 和会开始时调用。`ROOT`为胜利方，`FROM`为失败方。                                           |
| `on_peaceconference_ended`         | 和会结束时调用。`ROOT`为胜利方，`FROM`为失败方；原版也用于战后殖民状态等检查。             |

#### 外交与战争
外交与战争类 on actions 覆盖志愿军、宣战、战争关系、和平、投降、吞并、附庸、释放国家等流程。

| On action                            | 说明                                                                                     |
|--------------------------------------|------------------------------------------------------------------------------------------|
| `on_send_volunteers`                 | 派遣志愿军时调用。                                                                       |
| `on_recall_volunteers`               | 召回志愿军时调用。                                                                       |
| `on_border_war_lost`                 | 边境战争失败时调用。                                                                     |
| `on_war_relation_added`              | 两国之间新增战争关系时调用。`ROOT`为进攻方，`FROM`为防御方。                             |
| `on_declare_war`                     | 宣战时调用。`FROM`为战争目标。                                                           |
| `on_war`                             | 国家从和平进入战争状态时调用。国家已处于战争中再加入另一场战争时通常不会再次调用。       |
| `on_peace`                           | 国家进入和平状态时调用。                                                                 |
| `on_capitulation`                    | 国家投降时调用。`ROOT`为投降国家，`FROM`为胜利方。                                       |
| `on_capitulation_immediate`          | 国家投降的即时处理项。`ROOT`为投降国家，`FROM`为胜利方。                                 |
| `on_uncapitulation`                  | 先前投降的国家恢复非投降状态时调用。                                                     |
| `on_annex`                           | 国家被吞并时调用。`ROOT`为吞并方，`FROM`为被吞并方。内战结束也可能同时触发相关吞并逻辑。 |
| `on_civil_war_end_before_annexation` | 内战吞并结算前调用。                                                                     |
| `on_civil_war_end`                   | 内战结束时调用。`ROOT`为胜利方，`FROM`为被吞并方。                                       |
| `on_puppet`                          | 和会中建立傀儡国时调用。通常`ROOT`为被傀儡国家，`FROM`为宗主国。                         |
| `on_force_government`                | 强制政府变化时调用。                                                                     |
| `on_liberate`                        | 解放国家时调用。                                                                         |
| `on_release_as_free`                 | 以自由国家形式释放时调用。                                                               |
| `on_release_as_puppet`               | 以傀儡国形式释放时调用。                                                                 |

#### 阵营
阵营类 on actions 处理阵营创建、邀请、加入、领导权转移和离开。

| On action                      | 说明                                                                           |
|--------------------------------|--------------------------------------------------------------------------------|
| `on_create_faction`            | 阵营创建时调用。原版说明中`FROM`为加入新阵营的国家。                           |
| `on_faction_formed`            | 新阵营形成时调用。                                                             |
| `on_offer_join_faction`        | 邀请国家加入阵营时调用。`FROM`为被邀请国家。                                   |
| `on_join_faction`              | 国家通过加入请求等方式加入阵营时调用。**该项不会由`add_to_faction`效果触发**。 |
| `on_assume_faction_leadership` | 国家取得阵营领导权时调用。                                                     |
| `on_leave_faction`             | 国家离开阵营时调用。`ROOT`为离开阵营的国家，`FROM`为阵营领袖。                 |

#### 自治
自治类 on actions 用于宗主国与附属国关系的变化。

| On action                          | 说明                       |
|------------------------------------|----------------------------|
| `on_subject_annexed`               | 附属国被吞并时调用。       |
| `on_subject_free`                  | 附属国脱离附属状态时调用。 |
| `on_subject_autonomy_level_change` | 附属国自治等级变化时调用。 |

#### 流亡政府
流亡政府类 on actions 与政府流亡、东道国变化和复国相关。

| On action                           | 说明                                 |
|-------------------------------------|--------------------------------------|
| `on_government_exiled`              | 政府流亡时调用。                     |
| `on_host_changed_from_capitulation` | 因投降导致流亡政府东道国变化时调用。 |
| `on_exile_government_reinstated`    | 流亡政府恢复时调用。                 |

#### 地区
地区类 on actions 用于地图地区控制权变化。

| On action                  | 说明                                                                             |
|----------------------------|----------------------------------------------------------------------------------|
| `on_state_control_changed` | 地区控制者变化时调用。`ROOT`为新控制者，`FROM`为旧控制者，`FROM.FROM`为地区 ID。 |

#### 战争目标
战争目标类 on actions 用于正当化进度和战争目标过期。

| On action                     | 说明                                                                                                         |
|-------------------------------|--------------------------------------------------------------------------------------------------------------|
| `on_justifying_wargoal_pulse` | 正当化战争目标期间每日调用。原版注释提醒该项触发频率高，应设置不触发事件的权重或限制条件。`FROM`为目标国家。 |
| `on_wargoal_expire`           | 战争目标过期时调用。                                                                                         |

#### 将领
将领类 on actions 用于陆军将领创建、日常检查、战斗结果、升级和晋升。

| On action                                   | 说明                                                                 |
|---------------------------------------------|----------------------------------------------------------------------|
| `on_unit_leader_created`                    | 单位领袖创建时调用。                                                 |
| `on_army_leader_daily`                      | 陆军将领每日调用。`FROM`为所属国家。                                 |
| `on_army_leader_won_combat`                 | 陆军将领赢得战斗时调用。`FROM`为所属国家。                           |
| `on_army_leader_lost_combat`                | 陆军将领输掉战斗时调用。`FROM`为所属国家。                           |
| `on_unit_leader_level_up`                   | 单位领袖升级时调用。                                                 |
| `on_army_leader_promoted`                   | 陆军将领晋升时调用。                                                 |
| `on_unit_leader_promote_from_ranks_veteran` | 老练单位晋升出将领时调用。原版说明中当前作用域为将领，`FROM`为单位。 |
| `on_unit_leader_promote_from_ranks_green`   | 新兵单位晋升出将领时调用。原版说明中当前作用域为将领，`FROM`为单位。 |

#### 王牌飞行员
王牌飞行员类 on actions 用于王牌产生、击杀、事故死亡以及王牌之间互相击杀。

| On action                     | 说明                                                               |
|-------------------------------|--------------------------------------------------------------------|
| `on_ace_promoted`             | 王牌飞行员产生时调用。`FROM`为王牌。                               |
| `on_ace_killed`               | 本方王牌被无名飞行员击落时调用。`FROM`为王牌。                     |
| `on_ace_killed_on_accident`   | 本方王牌因事故死亡时调用。`FROM`为王牌。                           |
| `on_non_ace_killed_other_ace` | 本方无名飞行员击落敌方王牌时调用。`FROM`为敌方王牌。               |
| `on_ace_killed_by_ace`        | 本方王牌被敌方王牌击落时调用。`FROM`为本方王牌，`PREV`为敌方王牌。 |
| `on_ace_killed_other_ace`     | 本方王牌击落敌方王牌时调用。`FROM`为本方王牌，`PREV`为敌方王牌。   |
| `on_aces_killed_each_other`   | 两名王牌互相击落时调用。原版说明该项会触发两次，每名王牌各一次。   |

#### 特工、行动与破译
以下 on actions 属于 La Résistance 相关系统，覆盖情报行动、特工状态和密码破译。

| On action                                | 说明                           |
|------------------------------------------|--------------------------------|
| `on_operation_completed`                 | 情报行动完成时调用。           |
| `on_operative_detected_during_operation` | 特工在行动中被发现时调用。     |
| `on_operative_on_mission_spotted`        | 执行任务中的特工被发现时调用。 |
| `on_operative_captured`                  | 特工被捕时调用。               |
| `on_operative_created`                   | 特工创建时调用。               |
| `on_operative_death`                     | 特工死亡时调用。               |
| `on_operative_recruited`                 | 特工招募完成时调用。           |
| `on_fully_decrypted_cipher`              | 完全破译密码时调用。           |
| `on_activated_active_decryption_bonuses` | 启用主动破译加成时调用。       |

#### 军事工业组织
军事工业组织类 on actions 用于 MIO 规模、设计团队、制造商分配以及科技研究状态。

| On action                                   | 说明                                 |
|---------------------------------------------|--------------------------------------|
| `on_mio_size_increased`                     | 军事工业组织规模提升时调用。         |
| `on_mio_design_team_assigned_to_tech`       | MIO 设计团队被分配到科技时调用。     |
| `on_mio_design_team_assigned_to_variant`    | MIO 设计团队被分配到装备型号时调用。 |
| `on_mio_industrial_manufacturer_assigned`   | 工业制造商被分配时调用。             |
| `on_mio_tech_research_cancelled`            | MIO 相关科技研究取消时调用。         |
| `on_mio_tech_research_completed`            | MIO 相关科技研究完成时调用。         |
| `on_mio_industrial_manufacturer_unassigned` | 工业制造商被取消分配时调用。         |

### 项目
较新版本中存在与特殊项目相关的 on action。

| On action               | 说明                                                   |
|-------------------------|--------------------------------------------------------|
| `on_project_completion` | 项目完成时调用。可用于特殊项目完成后的事件或奖励逻辑。 |