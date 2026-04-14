# descriptor.mod文件

`descriptor.mod`文件中包含有Mod的各种信息，在创建Mod后自动创建，以下是一个示例：

```paradox_script
version = "0.0.1"
tags = {
    "Alternative History"
}
dependencies={
    "Spring"
}
name = "test"
supported_version = "1.17.*"
replace_path = common/bookmarks
picture = thumbnail.png
remote_file_id = *
```

其中各部分内容如下：

- `version = xxx` Mod版本。
- `name = xxx` Mod名称。
- `tags = { ... }` 包含创建Mod时勾选的标签，同时是Mod在Steam创意工坊上的标签。
- `dependencies={ ... }`Mod的前置Mod，名称为该Mod在描述文件中注册的`name`。
- `picture = <file>` Mod缩略图，同时是ModMod在Steam创意工坊上的封面。
- `replace_path = xxx` 包含Mod将要替换的文件夹。
- `supported_version = *` Mod所支持的游戏版本
- `remote_file_id = *` Mod在Steam创意工坊上的id，**上传之后自动生成，无需手动添加分配**。
