# 本地化
游戏内支持的本地化语言共有以下几种：
- `l_english` 英语
- `l_simp_chinese` 简体中文
- `l_french` 法语
- `l_german` 德语
- `l_spanish` 西班牙语
- `l_braz_por` 葡萄牙语（巴西）
- `l_polish` 波兰语
- `l_russian` 俄语
- `l_japanese` 日语
## 文件夹结构格式
本地化文件位于`localisation`中**依据语言进行分类**的（例如`simp_chinese`）文件夹中。  
文件夹中也可建立新的文件夹以进一步细分。
## 文件格式
本地化文件遵循以下格式：
- 本地化文件储存为`.yml`。
- 文件命名末尾应包含本地化语言名称（例`test_l_simp_chinese.yml`）。
- 文件编码必须为`UTF-8 with BOM`。
## 内容格式
### 基础本地化内容格式
以下为一个基础本地化文件示例：
```paradox_localisation
l_simp_chinese:  
 library:0 "图书馆"
```
其中，`l_simp_chinese:`以语言名称作为文件开头；`library`是本地化键值；`0`是本地化版本号（可选，表示该条自创建以来被更改的次数）；`图书馆`是本地化内容。
### 本地化内容着色
着色内容以符号`§`开头，后面跟字母或数字；`§!`标记着色内容结束。  
以下为一个本地化示例：
```paradox_localisation
l_simp_chinese:
 angry: "§R红温§!"
```
其中，本地化输出时`红温`这部分本地化内容将被着色为<font color=#ff3232>红色</font>。<br>
以下是一个表格，列出了游戏本体的的着色符号及其对应RGB值：

| 符号 | 颜色                                            |
|----|-----------------------------------------------|
| §W | <font color=#ffffff>{ 255, 255, 255 }</font>  |
| §R | <font color=#ff3232>{ 255, 50, 50 }</font>    |
| §G | <font color=#009f03>{ 0, 159, 3 }</font>      |
| §B | <font color=#0000ff>{ 0, 0, 255 }</font>      |
| §Y | <font color=#ffbd00>{ 255, 189, 0 }</font>    |
| §C | <font color=#23ceff>{ 35, 206, 255 }</font>   |
| §L | <font color=#c3b091>{ 195, 176, 145 }</font>  |
| §O | <font color=#ff7019>{ 255, 122, 25 }</font>   |
| §b | <font color=#000000>{ 0, 0, 0 }</font>        |
| §g | <font color=#b0b0b0>{ 176, 176, 176 }</font>  |
| §0 | <font color=#cb00cb>{ 203, 203, 203 }</font>  |
| §1 | <font color=#8078d3>{ 128, 120, 211 }</font>  |
| §2 | <font color=#5170f3>{ 81, 122, 243 }</font>   |
| §3 | <font color=#518fdc>{ 81, 143, 220 }</font>   |
| §4 | <font color=#5abee7>{ 90, 190, 231 }</font>   |
| §5 | <font color=#3fb5c2>{ 63, 181, 194 }</font>   |
| §6 | <font color=#77ccba>{ 119, 204, 186 }</font>  |
| §7 | <font color=#99d199>{ 153, 209, 153 }</font>  |
| §8 | <font color=#cca333>{ 204, 163, 51 }</font>   |
| §9 | <font color=#fca97d>{ 252, 169, 125  }</font> |
| §t | <font color=#ff4c4d>{ 255, 76, 77 }</font>    |

关于本地化着色的更多信息，可参考[Wiki](https://hoi4.paradoxwikis.com/Localisation#Colouring_characters "点击跳转至页面")。
### 本地化内容嵌入图片
图片嵌入内容以符号`£`进行插入。  
以下为一个本地化示例：
```paradox_localisation
l_simp_chinese:
 happy: "高兴£GFX_happy_face£!"
```
其中，将会读取注册为为`GFX_happy_face`名称的图像在并在本地化内容中插入。