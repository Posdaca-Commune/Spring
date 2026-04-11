# 音乐&电台
游戏内的音乐&电台文件位于`music`文件夹内，包含了游戏中所有的电台音乐，音乐文件格式为`.ogg`。<br>
音乐文件，音乐定义文件与电台定义文件必须位于同一文件夹内。
## 音乐定义文件
音乐定义文件储存为`.asset`。<br>
以下为一个音乐定义文件示例：
```paradox_script
music = {
    name = "xxx"
    file = "xxx.ogg"
    volume = *
}
```
- `name = "xxx"`定义了音乐的名称，游戏内通过该名称调用音乐，同时使用其作为本地化键值。
- `file = "xxx.ogg"`定义了音乐文件的路径，路径相对于`music`文件夹。
- `volume = *`定义了音乐的音量，取值范围为0-1。
> *tips: 音乐名称的本地化键值最多支持63个字符(characters)。*
## 电台定义文件
电台定义文件储存为`.txt`。<br>
以下为一个电台定义文件示例：
```paradox_script
music_station = "xxx"
music = {
    song = "xxx"
    chance = {
        modifier = {
            factor = 1
        }
    }
}
```
- `music_station = "xxx"`定义了电台的名称，游戏内通过该名称调用电台，同时使用其作为本地化键值。
- `song = "xxx"`定义了电台中包含的音乐，取值为音乐定义文件中定义的音乐名称。
- `chance = {}`定义了电台中包含的音乐的播放概率。`factor`为概率系数；`add`用于增加概率；`base`则完全替换概率。
## GUI中的电台
想要让电台出现在游戏界面中，需要在`interface`文件夹中新建`xxx.gui`文件，并添加如下内容：
```paradox_script
guiTypes = {
	containerWindowType = {
		name = "xxx_faceplate"
		position = { x =0 y=0 }
		size = { width = 590 height = 46 }

		iconType ={
			name ="musicplayer_header_bg"
			spriteType = "GFX_musicplayer_header_bg"
			position = { x= 0 y = 0 }
			alwaystransparent = yes
		}

		instantTextboxType = {
			name = "track_name"
			position = { x = 72 y = 20 }
			font = "hoi_20b"
			text = "Roger Pontare - Nar vindarna viskar mitt namn"
			maxWidth = 450
			maxHeight = 25
			format = center
		}

		instantTextboxType = {
			name = "track_elapsed"
			position = { x = 124 y = 30 }
			font = "hoi_18b"
			text = "00:00"
			maxWidth = 50
			maxHeight = 25
			format = center
		}

		instantTextboxType = {
			name = "track_duration"
			position = { x = 420 y = 30 }
			font = "hoi_18b"
			text = "02:58"
			maxWidth = 50
			maxHeight = 25
			format = center
		}

		buttonType = {
			name = "prev_button"
			position = { x = 220 y = 20 }
			quadTextureSprite ="GFX_musicplayer_previous_button"
			buttonFont = "Main_14_black"
			Orientation = "LOWER_LEFT"
			clicksound = click_close
			pdx_tooltip = "MUSICPLAYER_PREV"
		}

		buttonType = {
			name = "play_button"
			position = { x = 263 y = 20 }
			quadTextureSprite ="GFX_musicplayer_play_pause_button"
			buttonFont = "Main_14_black"
			Orientation = "LOWER_LEFT"
			clicksound = click_close
		}

		buttonType = {
			name = "next_button"
			position = { x = 336 y = 20 }
			quadTextureSprite ="GFX_musicplayer_next_button"
			buttonFont = "Main_14_black"
			Orientation = "LOWER_LEFT"
			clicksound = click_close
			pdx_tooltip = "MUSICPLAYER_NEXT"
		}

		extendedScrollbarType = {
			name = "volume_slider"
			position = { x = 100 y = 45}
			size = { width = 75 height = 18 }
			tileSize = { width = 12 height = 12}
			maxValue =100
			minValue =0
			stepSize =1
			startValue = 50
			horizontal = yes
			orientation = lower_left
			origo = lower_left
			setTrackFrameOnChange = yes

			slider = {
				name = "Slider"	
				quadTextureSprite = "GFX_scroll_drager"
				position = { x=0 y = 1 }
				pdx_tooltip = "MUSICPLAYER_ADJUST_VOL"
			}

			track = {
				name = "Track"
				quadTextureSprite = "GFX_volume_track"
				position = { x=0 y = 3 }
				alwaystransparent = yes
				pdx_tooltip = "MUSICPLAYER_ADJUST_VOL"
			}
		}

		buttonType = {
			name = "shuffle_button"
			position = { x = 425 y = 20 }
			quadTextureSprite ="GFX_toggle_shuffle_buttons"
			buttonFont = "Main_14_black"
			Orientation = "LOWER_LEFT"
			clicksound = click_close
		}
	}

	containerWindowType={
		name = "<MUSIC STATION>_stations_entry"
		size = { width = 162 height = 130 }
		
		checkBoxType = {
			name = "select_station_button"
			position = { x = 0 y = 0 }
			quadTextureSprite = "<SPRITE>"
			clicksound = decisions_ui_button
		}
	}
}
```
其中，`name = "xxx_faceplate"`中的`xxx`需要与电台定义文件中`music_station = "xxx"`的`xxx`保持一致。
> *tips: 关于GUI的更多内容可以查看`gui.md`文件。*