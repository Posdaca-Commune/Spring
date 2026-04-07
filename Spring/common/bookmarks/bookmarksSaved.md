# Bookmarks

## Overview

A bookmark defines a start scenario shown in the game setup screen. It controls the start date, the countries highlighted to the player, the text shown in the scenario panel, and any effects applied when the bookmark is selected.

Bookmark definitions are usually stored in:

```txt
common/bookmarks/*.txt
```

A bookmarks file uses this top-level structure:

```txt
bookmarks = {
    bookmark = {
        ...
    }
}
```

Each `bookmark = { ... }` block represents one selectable scenario.

---

## Structure

A bookmark usually contains:

- basic scenario fields such as `name`, `desc`, `date`, and `picture`
- one or more country entries such as `PRC = { ... }`
- an optional `"---"` entry for the general country selection entry
- an optional `effect = { ... }` block

Basic layout:

```txt
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

---

## Bookmark Fields

The following fields are used inside `bookmark = { ... }`.

### `name`

```txt
name = "SPRING_NAME"
```

Defines the localisation key used for the bookmark title.

### `desc`

```txt
desc = "SPRING_DESC"
```

Defines the localisation key used for the bookmark description.

### `date`

```txt
date = 1936.1.1.12
```

Defines the scenario start date in `YYYY.MM.DD.HH` format.

### `picture`

```txt
picture = "GFX_select_date_1936"
```

Defines the sprite used for the bookmark image. This sprite is usually provided through a `.gfx` definition in the `interface` folder.

### `default`

```txt
default = yes
```

Marks the bookmark as the default scenario in the game setup screen.

### `default_country`

```txt
default_country = PRC
```

Defines which country is selected by default when the bookmark is opened. This tag should also appear as a country entry inside the same bookmark.

### `effect`

```txt
effect = {
    randomize_weather = 12345
    set_global_flag = Qiuqi_is_pig
}
```

Runs effects when the bookmark is selected. This can be used for scenario-specific setup after history is loaded and before the game begins.

---

## Country Entries

Country entries are written directly inside the bookmark block by using a country tag as the key.

Example:

```txt
PRC = {
    history = "PRC_SPRING_DESC"
    ideology = communism
    ideas = {}
    focuses = {}
}
```

A bookmark may also contain:

```txt
"---" = {
    history = OTHER_SPRING_DESC
}
```

This entry represents the general "other countries" selection entry.

The same country can appear in more than one block if different conditions or display setups are needed.

---

## Country Entry Fields

The following fields are commonly used inside a country block such as `PRC = { ... }` or `QIU = { ... }`.

### `history`

```txt
history = "PRC_SPRING_DESC"
```

Defines the localisation key shown as the country description in the bookmark screen.

### `ideology`

```txt
ideology = communism
```

Defines the ideology group used for presentation in the scenario screen, including leader, icon, country name, and flag style.

### `ideas`

```txt
ideas = {
    IDEA_EXAMPLE_0
    IDEA_EXAMPLE_1
}
```

Lists the ideas shown in the country preview panel. This is display data for the bookmark screen and does not assign those ideas by itself.

### `focuses`

```txt
focuses = {
    FOCUS_EXAMPLE_0
    FOCUS_EXAMPLE_1
}
```

Lists the national focuses shown in the country preview panel.

### `available`

```txt
available = { has_dlc = "La Resistance" }
```

Adds a visibility condition for the country entry. This is often used for DLC checks or other scripted conditions.

### `minor`

```txt
minor = yes
```

Marks the country as a minor entry in the bookmark layout.

---

## Spring Template Reference

The following example reflects the structure used in `Spring/common/bookmarks/Spring.txt`:

```txt
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

---

## Notes

- A bookmark defines scenario presentation and selection data.
- Country history, state history, and other gameplay content should still be defined in their own files.
- The bookmark screen can display selected ideas, focuses, and country descriptions, but those entries are not a replacement for full gameplay setup.
- If a bookmark uses custom text or images, make sure the related localisation keys and interface resources are also present.