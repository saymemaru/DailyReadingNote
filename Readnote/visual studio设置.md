# visualstudio设置

## 开启内联参数名称/类型提示

启用后会在代码中显示灰色提示框，提示参数名称/类型

选项 -> 文本编辑器 -> C# -> 高级

![alt text](Assets/visualstudio设置_Assets/image-2.png)
![alt text](Assets/visualstudio设置_Assets/image.png)

## 修改 nuget 默认路径

节约C盘空间

1. 在 `C:\Program Files (x86)\NuGet\Config`目录中找到
2. 修改`Microsoft.VisualStudio.Offline.config`文件

```config
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="Microsoft Visual Studio Offline Packages"     value="E:\Program Files (x86)\Microsoft     SDKs\NuGetPackages\"/>
  </packageSources>
   <config> 
    <add key="globalPackagesFolder" value="D:\. nuget\packages" />
</config>
</configuration>
```

3. 将`C:\Users\{用户名}\.nuget\packages`的文件全部拷贝到`D:\.nuget\packages`
4. 使用 dotnet CLI`dotnet nuget locals all -l`检查路径是否生效
