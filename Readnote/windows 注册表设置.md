# Windows 注册表设置

## 注册表编辑器

``win + R`` 运行窗口中输入``regedit``

## 注册表文件.reg

创建空白文件，编辑完成后后缀改为.reg

### 添加程序到右键菜单

将指定路径下的程序添加到windows右键菜单，并且带有图标

```r
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\NotePad++]
@="Notepad++"
"Icon"="D:\\WorkTools\\Notepad++\\notepad++.exe,0"

[HKEY_CLASSES_ROOT\*\shell\NotePad++\Command]
@="D:\\WorkTools\\Notepad++\\notepad++.exe \"%1\""
```
