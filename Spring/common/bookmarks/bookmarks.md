# 剧本（bookmarks）
剧本定义了游戏设置界面中显示的起始剧本。它控制开始日期、向玩家高亮的国家、剧本面板中显示的文本，以及选择剧本时应用的任何效果。  
剧本定义通常存储在`common/bookmarks/*.txt`中。  
剧本文件的顶层结构如下：

```paradox_script
bookmarks = {
    bookmark = {
        #
    }
}
```

每个 `bookmark = { ... }` 块代表一个可选择的剧本。

## 结构

一个剧本通常包含：

- 基本剧本字段，如 `name`、`desc`、`date` 和 `picture`
- 一个或多个国家条目，如 `PRC = { ... }`
- 一个可选的 `"---"` 条目，用于通用国家选择项
- 一个可选的 `effect = { ... }` 块

基本布局：

```paradox_script
bookmarks = {
    bookmark = {
        name = "SPRING_NAME"
        desc = "SPRING_DESC"
        date = 1936.1.1.12
        picture = "GFX_select_date_1936"
        default_country = PRC
        default = yes

        PRC = {
            history = "PRC_SPRING_DESC"
            ideology = communism
        }

        "---" = {
            history = OTHER_SPRING_DESC
        }

        effect = {
            randomize_weather = 12345
        }
    }
}
```

## 剧本字段

以下字段用于 `bookmark = { ... }` 内部。

### `name`

```paradox_script
name = "SPRING_NAME"
```

定义用于剧本标题的本地化键。

### `desc`

```paradox_script
desc = "SPRING_DESC"
```

定义用于剧本描述的本地化键。

### `date`

```paradox_script
date = 1936.1.1.12
```

以 `YYYY.MM.DD.HH` 格式定义剧本开始日期。

### `picture`

```paradox_script
picture = "GFX_select_date_1936"
```

定义用于剧本图像的精灵。该精灵通常通过 `interface` 文件夹中的 `.gfx` 定义提供。

### `default`

```paradox_script
default = yes
```

将该剧本标记为游戏设置界面中的默认剧本。

### `default_country`

```paradox_script
default_country = PRC
```

定义打开剧本时默认选中的国家。该标签也应在同一剧本中作为国家条目出现。

### `effect`

```paradox_script
effect = {
    randomize_weather = 12345
    set_global_flag = Qiuqi_is_pig
}
```

在选择剧本时运行效果。可用于在历史加载完成后、游戏开始前进行剧本特定的设置。

## 国家条目

国家条目直接写在剧本块内部，使用国家标签作为键。

示例：

```paradox_script
PRC = {
    history = "PRC_SPRING_DESC"
    ideology = communism
    ideas = {}
    focuses = {}
}
```

剧本也可以包含：

```paradox_script
"---" = {
    history = OTHER_SPRING_DESC
}
```

该条目代表通用的"其他国家"选择项。

如果不同的条件或显示设置需要，同一国家可以出现在多个块中。

## 国家条目字段

以下字段通常用于国家块内部，如 `PRC = { ... }` 或 `QIU = { ... }`。

### `history`

```paradox_script
history = "PRC_SPRING_DESC"
```

定义在剧本界面中显示为国家描述的本地化键。

### `ideology`

```paradox_script
ideology = communism
```

定义用于剧本界面呈现的意识形态组，包括领导人、图标、国名和旗帜样式。

### `ideas`

```paradox_script
ideas = {
    IDEA_EXAMPLE_0
    IDEA_EXAMPLE_1
}
```

列出在国家预览面板中显示的国策理念。这是剧本界面的展示数据，本身不会分配这些理念。

### `focuses`

```paradox_script
focuses = {
    FOCUS_EXAMPLE_0
    FOCUS_EXAMPLE_1
}
```

列出在国家预览面板中显示的国家焦点。

### `available`

```paradox_script
available = { has_dlc = "La Resistance" }
```

为国家条目添加可见性条件。通常用于 DLC 检查或其他脚本化条件。

### `minor`

```paradox_script
minor = yes
```

将该国家标记为书签布局中的次要条目。

## Spring 模板参考

以下示例反映了 `Spring/common/bookmarks/Spring.txt` 中使用的结构：

```paradox_script
bookmarks = {
    bookmark = {
        name = "SPRING_NAME"
        desc = "SPRING_DESC"
        date = 1936.1.1.12
        picture = "GFX_select_date_1936"
        default_country = PRC
        default = yes

        PRC = {
            history = "PRC_SPRING_DESC"
            ideology = communism
            ideas = {}
            focuses = {}
        }

        "QIU" = {
            history = "QIU_SPRING_DESC"
            ideology = communism
            available = { has_dlc = "La Resistance" }
            new_content = yes
            minor = yes
            override_leader_portrait = BTA_Qiuqi
            focuses = {
                QIU_00_C1
                QIU_00_C2
            }
        }

        "---" = {
            history = OTHER_SPRING_DESC
        }

        effect = {
            randomize_weather = 12345
            set_global_flag = Qiuqi_is_pig
        }
    }
}
```

## 备注

- 剧本定义剧本的呈现和选择数据。
- 国家历史、省份历史和其他游戏内容仍应在其各自文件中定义。
- 剧本界面可以显示选定的理念、焦点和国家描述，但这些条目不能替代完整的游戏设置。
- 如果剧本使用自定义文本或图像，请确保相关的本地化键和界面资源也存在。