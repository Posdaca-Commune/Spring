# 背景（backgrounds）
此处控制游戏主页面的动态背景，对加载页面的背景无效。
## 文件夹结构格式
游戏内背景文件位于`gfx/loadingscreens`文件夹中。  
为了让背景能出现在选择页面，需要添加一张当前图片名称后添加`_small`的缩略图。
## 内容格式
以下是一个背景条目的示例：
```paradox_script
# 背景图像名称
load_0 = {
    # 可选条目
    dlc_allowed = "No Compromise, No Surrender" # 支持该背景的DLC
    locale = "simp_chinese" # 支持该背景的语言环境
    gfx = GFX_frontend_bg_basic # 覆盖的GFX标签
}
```
- `<NAME>`：背景图像的名称。
- `dlc_allowed = *`：支持该背景的DLC，游戏当前的背景由最新的DLC指定。
- `locale = *`：支持该背景的语言环境，当指定`locale`时会覆盖`dlc_allowed = *`指定的默认背景。
- `gfx = *`：覆盖的对应的GFX标签。