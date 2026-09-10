# Rime Configurations

Rime 输入法的个人配置仓库。目前仅在 macOS 上使用。

## 目录结构

本 Git 仓库的结构应当形如：

```
.
├── custom_dicts/        # 自定义词库
├── lua
|   └── custom/          # 自定义 Lua 脚本目录
├── .gitignore
├── README.md
├── custom_phrase.txt    # 自定义短语
└── *.custom.yaml        # 用于覆盖上游方案的自定义配置

```

本仓库需要直接被安装到 `~/Library/Rime` 目录下，完成配置时， `~/Library/Rime` 应当形如：

```
~/Library/Rime/
├── .git/                 # 本仓库的版本控制
├── .gitignore            # 白名单模式，只追踪自定义文件
│
├── *.custom.yaml         # 📝 自定义补丁配置，由本仓库追踪
├── custom_phrase.txt     # 📝 自定义短语，由本仓库追踪
├── README.md             # 📝 本文档，由本仓库追踪
│
├── *.schema.yaml         # 📦 上游输入方案，通过 plum 安装
├── *.dict.yaml           # 📦 上游词典，通过 plum 安装
├── cn_dicts/             # 📦 拼音词库
├── en_dicts/             # 📦 混合词库
├── lua
|   ├── *.lua             # 📦 上游 Lua 脚本，通过 plum 安装
|   └── custom/           # 📝 自定义 Lua 脚本，由本仓库追踪
├── opencc/               # 📦 OpenCC 简繁转换
│
├── plum/                 # 🔧 包管理器
├── build/                # ⚙️ 部署产物
├── *.userdb/             # 👤 用户数据
├── user.yaml             # 👤 运行时状态
└── installation.yaml     # 👤 安装信息
```

> 📝 = 本仓库追踪的自定义文件 | 📦 = plum 安装的第三方包 | 👤 = 本地数据

## 上游输入方案

| 方案 | 上游 |
|------|------|
| 朙月拼音 | [rime/rime-luna-pinyin](https://github.com/rime/rime-luna-pinyin) |
| 雾凇拼音 | [iDvel/rime-ice](https://github.com/iDvel/rime-ice) |

## 使用方式

### 全新安装

如果已经安装完成 Rime 输入法，则跳过该部分，直接看下一节。

如果想要重新安装 Rime 输入法的配置，在安装之前，注意先备份原有的 `*.userdb/` 目录。

```bash
# 安装鼠鬚管发行版
brew install --cask squirrel
# 安装 plum 包管理器
cd ~/Library/Rime
curl -fsSL https://raw.githubusercontent.com/rime/plum/master/rime-install | bash
# 使用 plum 安装上游方案
cd ~/Library/Rime
bash plum/rime-install
bash plum/rime-install iDvel/rime-ice
# 重新部署
"/Library/Input Methods/Squirrel.app/Contents/MacOS/Squirrel" --reload
```

### 设置 git 仓库

```bash
cd ~/Library/Rime
git init
git remote add origin <repository-url>
git pull -u origin main
```

### 同步配置

```bash
git pull
"/Library/Input Methods/Squirrel.app/Contents/MacOS/Squirrel" --reload
```

## 日常维护

### 修改配置

直接编辑文件，然后提交。

### 添加新的自定义 Lua

复制原始 Lua 到 custom 目录，在此基础上修改。

然后在对应的 `.custom.yaml` 中修改引用。

### 更新第三方包

```bash
cd ~/Library/Rime/plum
# 拉取 plum 本身的更新
git pull
cd ..
# 使用 plum 安装最新的上游方案
bash plum/rime-install
bash plum/rime-install iDvel/rime-ice
```

## 配置清单

| 文件 | 所属 | 用途 | 
|------|------|------|
| `default.custom.yaml` | 全局 | 方案列表；热键；符号映射 |
| `luna_pinyin_simp.custom.yaml` | 朙月拼音 | 模糊音 |
| `rime_ice.custom.yaml` | 雾凇拼音 | 开关配置；lua；模糊音 |
| `squirrel.custom.yaml` | 鼠鬚管界面 | 配色方案 |
| `custom_phrase.txt` | 全局 | 自定义短语 |

自定义词库：
| 文件 | 用途 |
|------|------|
| `latex_symbols.txt` | 常用 LaTeX 符号 |
自定义 Lua：

| 文件 | 用途 |
|------|------|
| `date_traslator.lua` | 在原版 lua 中删除了一些快捷输入方式 |
