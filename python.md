# python 教学

[python3 cookbook 中文](https://python3-cookbook.readthedocs.io/zh_CN/latest/chapters/p01_data_structures_algorithms.html)

[python3 cookbook 英文](https://d.cxcore.net/Python/Python_Cookbook_3rd_Edition.pdf)

> python cookbook是本工具书，告诉你库使用的最佳实践的，刚开始接触库的时候可以参考用。它本身的内容组织就是针对一个问题一个解。**很适合缺少实践技能的人。** 

[Python-100-Days](https://github.com/jackfrued/Python-100-Days)

[Learn More Python 3 The Hard Way](https://learncodethehardway.org/more-python-book/)

学习 python 基础：

1. 建立 python 项目，项目 Debug。简单的代码版本控制。

2. 基础数据结构的使用（set，list，dict），循环，if...else 等控制。


进阶学习：

1. 如何查到自己记不住，不知道的东西。
2. 如何做 code snippet，做知识管理。
3. 如何写复杂的代码。

![python_big_picture](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/python_big_picture.png>)

## python 项目入门

1. 学习如何安装 python 解释器，并熟练设置 python 解释器。
2. 学习如何安装虚拟环境，并在虚拟环境中安装包。
3. 学习如何在 IDE 中设置 python 解释器。
4. 学习如何在 IDE 中 debug，进行代码跳转，代码阅读。

进行之前需要安装 [Pycharm-Community](https://www.jetbrains.com/pycharm/download/#section=windows)，[Git](https://git-scm.com/download/win)，[terminus](https://github.com/Eugeny/terminus/releases)，了解基础 linux 命令，例如 `cd ls mkdir` 等。

```bash
cd 文件夹名称
cd .. 返回上级文件夹
cd 回家目录 # $HOME
ls 显示当前文件夹内容
ls -lha 显示隐藏文件/夹
rm 文件名称 # 删除文件
rm -rf 文件夹 # 删除文件夹
```

命令行下的编辑器
```bash
vim abc.toml # 打开文件名称为 abc.toml 的文件，如果没有就创建一个空的。
按 I 进入 insert 模式，可以写东西。写好后按 Esc 进入命令模式。
进入命令模式后 按:x 保存并退出，按 :q! 不保存并退出。
```

![python_project_demo](http://wiki-picture.oss-cn-beijing.aliyuncs.com/python_proejct_demo.png)

![](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/%E8%A7%A3%E9%87%8A%E5%99%A8%E5%9B%BE.jpg>)

### python 解释器

[python 解释器](https://www.liaoxuefeng.com/wiki/1016959663602400/1016966024263840)：执行 `.py` 文件的东西。一般我们用 Cpython，也就是我们平时说的 3.6 python，3.7 python等。因为不同项目可能因为依赖问题需要使用不同版本的 python，例如有一些包需要 python < 3.6。[Pyenv](https://github.com/pyenv/pyenv) 可以方便的在**不同文件夹下**切换不同的 python 版本，但是大家普遍使用 windwos 可以使用 [pyenv-win](https://github.com/pyenv-win/pyenv-win) 项目。如果没有 python 版本控制的需求，可以直接安装一个 python3 就可以了。

-----

在 [terminus](https://github.com/Eugeny/terminus/releases) 中，配置 git-bash

**settings | shell | profile | git-bash**

![terminus_settings](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/terminus_settings.png>)

[pyenv-win 安装](https://github.com/pyenv-win/pyenv-win#installation)：打开 terminal，输入

```bash
git clone https://github.com/pyenv-win/pyenv-win.git $HOME/.pyenv
```

安装后，在环境变量处（**右键我的电脑 | 属性 | 高级系统设置 | 环境变量 | 用户环境变量 path **），添加：

- `%USERPROFILE%\.pyenv\pyenv-win\bin`
- `%USERPROFILE%\.pyenv\pyenv-win\shims`

位置在 `%USERPROFILE%\AppData\Local\Microsoft\WindowsApps` 之上。

![](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/pyenv_win_path.png>)

[pyenv  用法](https://github.com/pyenv-win/pyenv-win#usage)：

`pyenv install -l` 查看可以安装的版本

`pyenv install 3.7.4-amd64`  安装 64 位 3.7.4 python

（重要）安装好后在 $HOME 中 rehash，

```bash
cd # 回到家目录
pyenv rehash # 更新 pyenv 相关配置
```

> pyenv 会把 python 解释器安装在 $HOME/.pyenv/pyenv-win/versions 目录下

`pyenv version` 查看当前路径的 python 解释器。

`pyenv versions`  查看当前所有已安装的解释器。

`pyenv local 3.7.4-amd64` 在当前文件夹内指定 python 解释器为 3.7.4

`pyenv global 3.7.4-amd64` 指定全局  python 解释器为 3.7.4

### 包管理

[为什么要用 poetry 或者 pipenv 进行包管理？](https://realpython.com/pipenv-guide/#problems-that-pipenv-solves)

[poetry](https://github.com/sdispater/poetry): Poetry helps you declare, manage and install dependencies of Python projects, ensuring you have the **right stack** everywhere.

包管理，就是让项目中的所用到的依赖关系保持稳定，可复用。以前大家用过 pip virtualenv 等工具，poetry 和 pipenv 是建立在这些基础工具之上，让大家更方便的管理依赖关系。例如当我们想删除一个次项目不需要的包时，`poetry remove` 会删的更彻底，而 `pip uninstall` 会删不干净导致依赖关系破裂。

-----

[poetry 安装](https://poetry.eustace.io/docs/#installation)

用 pyenv 设置好 global python 后，

```bash
curl -sSL https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python
```

安装后，在环境变量处（**右键我的电脑 | 属性 | 高级系统设置 | 环境变量 | 用户环境变量 path **），添加：

- `%USERPROFILE%\.poetry\bin`

```bash
poetry --version
```

[用法](https://poetry.eustace.io/docs/cli/#commands)：

cd 进入到项目文件夹根目录，并输入 

```bash
poetry init
```

![](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/poetry_init.png>)

如果没有自动创建 `pyproject.toml` 文件，创建一个空 `pyproject.toml`，并将 `poetry init` 的结果粘贴到创建的 `pyproject.toml` 中。

指定当前文件夹下的 python

```bash
pyenv local 3.7.4-amd64
```

根据当前文件夹下的 python 解释器创建虚拟环境：

```bash
poetry install
```

安装包

```bash
poetry add 包名
```

删除包

```
poetry remove 包名
```

-----

### IDE

集成开发环境是用于提供程序**开发环境**的应用程序，一般包括代码编辑器、编译器、调试器和图形用户界面等工具。 **集成**了代码编写功能、分析功能、编译功能、调试功能等一体化的**开发**软件服务套。这里使用的是 pycharm。

[一份超超超级完整的PyCharm图解教程 - 胖虎的文章 - 知乎](https://zhuanlan.zhihu.com/p/87045701)

> pycharm 是最强 python ide，集成了很多开发必备的功能：代码结构的跳转，代码 lint，。年费在 100多刀左右。

ide 需要用户指定具体的 python 解释器。这样才能在对的地方运行代码。

**设置 ide 使用的 terminal 为 gitbash**

**File | Settings | 输入 terminal**

![](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/pycharm_gitbash.png>)

shell path 输入：`"c:\Program Files\Git\bin\sh.exe" --login`

--------------------------

### 实战：创建新项目

在 pycharm 中创建新项目:

**File | open | 选中 PycharmProjects 文件夹 | 左上角 new folder | 创建好后按 ok**

在新项目中按 alt + F12 呼出 terminal

```bash
pyenv local python版本(<3.8)
poetry init
poetry add pandas
# Creating virtualenv project-demo-py3.7 in C:\Users\zbjdonald\AppData\Local\pypoetry\Cache\virtualenvs
Using version ^0.25.3 for pandas
```

设置 python 解释器：

**File | Settings... | 搜索 interpreter | 选择 ADD** 
![settings1](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/settings_interpreter.png>)

![settings2](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/settings_inter_2.png>)

在地址栏输入上面拿到的`C:\Users\zbjdonald\AppData\Local\pypoetry\Cache\virtualenvs`

选中项目名称的文件夹例如（project-demo -py3.7），选中 `scripts` 中的 python 并确定。

![settings3](<http://wiki-picture.oss-cn-beijing.aliyuncs.com/settings_inter_3.png>)

设置好解释器后等待 index，index 好后解释器设置完毕，可以写代码了。

[Python requests deep dive - Anthony Shaw - Medium](https://medium.com/@anthonypjshaw/python-requests-deep-dive-a0a5c5c1e093)

