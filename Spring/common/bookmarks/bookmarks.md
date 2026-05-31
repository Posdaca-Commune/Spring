# 剧本（bookmark）
剧本定义了游戏设置界面中显示的起始剧本。它控制开始日期、向玩家高亮的国家、剧本面板中显示的文本，以及选择剧本时应用的任何效果。
## 文件夹结构格式
剧本文件位于`common/bookmarks`中。每一个`.txt`文件都可以包含一个或多个剧本定义。
## 内容格式
以下是一个剧本文件的示例：
```paradox_script
bookmarks = {
    # 每一个剧本都在一个bookmark = { ... }块中定义
    bookmark = {
        name = "SPRING_NAME" # 剧本名称
        desc = "SPRING_DESC" # 剧本描述
        date = 1936.1.1.12 # 剧本开始日期，格式为YYYY.MM.DD.HH
        picture = "GFX_select_date_1936" # 剧本的封面图片
        default_country = PRC # 默认国家
        default = yes # 是否是默认剧本
        # 展示的国家条目
        PRC = {
            history = "PRC_SPRING_DESC" # 国家的历史简介
            ideology = communism # 国家的意识形态
            ideas = {} # 国家的民族精神
            focuses = {} # 国家的国策
        }
        # 其他国家
        "---" = {
            history = OTHER_SPRING_DESC
        }

        effect = {
            randomize_weather = 12345
        }
    }
}
```
- `name = *`：剧本名称的本地化键。
- `desc = *`：剧本描述的本地化键。
- `date = *.*.*.*`：剧本的开始日期，格式为`YYYY.MM.DD.HH`。
- `picture = *`：剧本的封面图片。
- `default_country = *`：打开剧本时默认选中的国家。
  - `default = yes`：将该剧本标记为游戏设置界面中的默认剧本。
- `<TAG> = *`：在剧本界面中显示的国家条目，其中`<TAG>`是国家标签，`"---"`代表其他国家的通用条目。
- `history = *`：国家历史简介的本地化键。
- `ideology = *`：国家的意识形态。
- `ideas = { ... }`：国家的民族精神。
- `focuses = { ... }`：国家的国策。
- `available = { ... }`：国家条目的可见性条件。
- `minor = yes`：将国家标记为书签布局中的次要条目。