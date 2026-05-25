# Rime Configurations

Rime 输入法的个人配置仓库。目前仅在 macOS 上使用。

有些配置文件并非完全由我编写，我会尽可能在文件头部注明原作者和来源。

## 目录结构

本 Git 仓库的结构应当形如：

```
.
├── *.custom.yaml        ← 用于覆盖上游方案的自定义配置
├── custom_phrase.txt    ← 自定义短语
├── lua
|   └── custom/          ← 自定义 Lua 脚本存放目录
├── README.md
└── .gitignore
```

本仓库需要直接被克隆到 `~/Library/Rime` 目录下，此时 `~/Library/Rime` 应当形如：

```
```

## 上游输入方案

| 方案 | 上游 |
|------|------|
| 朙月拼音 | [rime/rime-luna-pinyin](https://github.com/rime/rime-luna-pinyin) |
| 雾凇拼音 | [iDvel/rime-ice](https://github.com/iDvel/rime-ice) |

## 前置条件

- macOS 系统
- 已安装 [鼠鬚管](https://rime.im/download/)：`brew install --cask squirrel`

## 使用方式

### 全新安装

如果已经安装完成 Rime 输入法，则跳过该部分，直接看下一节。

```bash
# 安装鼠鬚管发行版
brew install --cask squirrel
# 安装基础包和雾凇拼音
cd ~/Library/Rime
bash plum/rime-install
bash plum/rime-install iDvel/rime-ice
# 重新部署
/Library/Input\ Methods/Squirrel.app/Contents/MacOS/Squirrel --reload
```

### 设置 git 仓库

```bash
git init
git remote add origin <repository-url>
git pull origin main
```

### 同步配置

```bash
git pull origin main
/Library/Input\ Methods/Squirrel.app/Contents/MacOS/Squirrel --reload
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

自定义 Lua：

| 文件 | 用途 |
|------|------|
| `date_traslator.lua` | 在原版 lua 中删除了一些快捷输入方式