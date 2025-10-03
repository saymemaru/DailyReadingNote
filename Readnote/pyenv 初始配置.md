# pyenv 初始配置

pyenv 用于快速在不同文件间切换 py 版本

## 配置

1.下载 `git clone https://github.com/pyenv-win/pyenv-win.git`

2.设置系统变量  

- 设置为安装位置
- path顺序需排在已安装python上方

```c
PYENV : E:\.pyenv\pyenv-win  
PYENV_HOME : E:\.pyenv\pyenv-win  
PYENV_ROOT : E:\.pyenv\pyenv-win

PATH :  
E:\.pyenv\pyenv-win\bin
E:\.pyenv\pyenv-win\shims
```

![alt text](<Assets/pyenv 初始配置_Assets/image.png>)

3.安装py

1. 将`python-3.10.3-amd64.exe`等安装包放入.`pyenv\pyenv-win\install_cache`文件夹
2. cmd 输入`pyenv install 3.10.3`安装目标版本

![alt text](<Assets/pyenv 初始配置_Assets/image-1.png>)

4.设置范围

- `pyenv global 3.10.3`将目标版本设置为全局
- `pyenv local 3.10.3` cmd 中 cd 到目标文件夹, 将目标文件夹环境设置为目标版本

## 使用

`pyenv versions`查询全部已安装的py版本

`pyenv version`查询当前文件夹py版本

`pyenv uninstall 3.10.3` 删除目标py版本

## 包管理

`pip config list`查询所有`pip.ini`pip配置文件

配置详见[pip 下载配置&测试]
