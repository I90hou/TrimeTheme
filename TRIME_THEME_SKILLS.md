# TRIME 主题文件规范与语法参考（TRIME Theme Skills）

> 本文档基于 TRIME `config_version: "3.0"` 主题文件的完整结构和已验证的实践经验编写，涵盖所有必需字段、颜色系统、键盘布局、悬浮键盘、工具栏及常见陷阱。

---

## 1. 文件基本信息

### 1.1 文件头

```yaml
# SPDX-FileCopyrightText: 2015 - 2024 Rime community
#
# SPDX-License-Identifier: GPL-3.0-or-later

# Trime custom style settings
# encoding: utf-8
```

### 1.2 顶层元数据

```yaml
config_version: "3.0"
name: 主题中文名／English Name          # 方案名称，TRIME 中显示的名称
author: TRIME Theme                      # 作者信息
```

- `name`：方案名称，支持 `中文／English` 格式
- `author`：可加引号也可不加（如 `"Chh"` 或 `TRIME Theme`）

---

## 2. 键盘高度 (`height`)

使用 YAML 锚点 (`&anchor`) 定义各键盘高度，后续通过别名 (`*anchor`) 引用。

```yaml
height:
  1: &jpgd1 30     # 表情键盘
  2: &jpgd2 24     # 颜文字键盘1
  3: &jpgd3 24     # 颜文字键盘2
  4: &jpgd4 48     # 主键盘
  5: &jpgd5 39.5   # 符号键盘
  6: &hgap 4       # 键盘横缝大小
  7: &sgap 12      # 键盘竖缝大小
```

---

## 3. 圆角 (`round_corner`)

```yaml
round_corner:
  1: &round1 6     # 按键圆角半径
  2: &round2 0     # 候选窗口圆角
  3: &round3 12    # 回车键圆角
```

---

## 4. 界面风格与功能开关 (`style`)

这是最大的固定参数段，所有新主题均保持一致，不需要修改。

| 参数 | 值 | 说明 |
|------|-----|------|
| `auto_caps` | `false` | 自动句首大写 |
| `candidate_font` | `han.ttf` | 候选字体 |
| `candidate_padding` | `5` | 候选项内边距 |
| `candidate_spacing` | `0.0` | 候选分割线间距 |
| `candidate_text_size` | `23` | 候选字号 |
| `candidate_text_vertical_bias` | `1.0` | 候选文本垂直偏移（范围 0.0~1.0） |
| `candidate_view_height` | `28` | 候选区高度 |
| `comment_font` | `comment.ttf` | 编码提示字体 |
| `comment_height` | `12` | 编码提示区高度 |
| `comment_position` | `right` | 编码提示布局位置：`right` / `top` / `overlay` |
| `comment_vertical_bias` | `0.0` | 编码提示垂直偏移（overlay 模式） |
| `comment_text_size` | `10` | 编码提示字号 |
| `hanb_font` | `hanb.ttf` | 扩充字体 |
| `horizontal_gap` | `*hgap` | 键水平间距 |
| `key_font` | `symbol.ttf` | 键盘字体 |
| `key_height` | `*jpgd4` | 键高 |
| `key_long_text_size` | `16` | 长标签字号 |
| `key_text_size` | `24` | 键字号 |
| `key_width` | `10.0` | 键宽（屏幕宽百分比） |
| `label_text_size` | `22` | 标签字号 |
| `label_font` | `label.ttf` | 标签字体 |
| `latin_font` | `latin.ttf` | 西文字体 |
| `keyboard_height` | `225` | 锁定键盘高度（防闪烁） |
| `keyboard_height_land` | `200` | 横屏键盘高度 |
| `popup_font` | `latin.ttf` | 按键提示字体 |
| `popup_width` | `38` | 按键提示宽度 |
| `popup_height` | `48` | 按键提示高度 |
| `popup_bottom_margin` | `68` | 按键提示底边距 |
| `popup_key_height` | `48` | 按键提示内键高度 |
| `popup_text_size` | `23` | 按键提示字号 |
| `reset_ascii_mode_on_focus_change` | `false` | 焦点切换时重置 ASCII 模式 |
| `round_corner` | `*round1` | 按键圆角半径 |
| `shadow_radius` | `0.0` | 按键阴影半径（TRIME 不支持，仅占位） |
| `symbol_font` | `symbol.ttf` | 符号字体 |
| `symbol_text_size` | `10` | 符号字号 |
| `text_font` | `latin.ttf` | 编码字体 |
| `vertical_gap` | `*sgap` | 键盘行距 |
| `enter_label_mode` | `0` | Enter 键标签模式 |
| `enter_labels` | (见下方) | Enter 键文本映射 |

```yaml
  enter_labels:
    go: 前往
    done: 完成
    next: 下个
    pre: 上个
    search: 搜索
    send: 发送
    default: Enter
```

---

## 5. 预编辑区 (`preedit`)

```yaml
preedit:
  horizontal_padding: 8
  top_end_radius: 4
  foreground:
    font_size: 16
```

---

## 6. 候选窗口 (`window`)

```yaml
window:
  insets:
    vertical: 4
    horizontal: 4
  item_padding:
    horizontal: 4
  foreground:
    label_font_size: 20
    text_font_size: 20
    comment_font_size: 16
```

---

## 7. 回退颜色 (`fallback_colors`)

**必须保留**，防止其他主题通过 `__include` 引用时加载失败。

```yaml
fallback_colors:
  candidate_text_color: text_color
```

---

## 8. 颜色变量定义 (`colors`)

定义 8 个 YAML 锚点颜色变量，供图案/图片引用（一般不需修改）。

```yaml
colors:
  1: &color1 0xff000000
  2: &color2 0xffffffff
  3: &color3 0xffe1e3e7
  4: &color4 0xffacb2c2
  5: &color5 0xff131313
  6: &color6 0xff3266a0
  7: &color7 0x00
  8: &color8 0xff838383
```

---

## 9. 配色方案 (`preset_color_schemes`) — 核心可定制区域

每个主题需定义**一对**配色方案：一个日间（浅色）和一个夜间（深色），通过 `dark_scheme` 关联。

### 9.1 颜色格式

**格式**：`0xAARRGGBB`（8 位十六进制）
- `AA`：Alpha 通道（`ff` = 不透明，`00` = 全透明）
- `RR`：红色通道
- `GG`：绿色通道
- `BB`：蓝色通道

示例：`0xff3D4F5F` = 不透明深蓝灰色

### 9.2 配色方案结构模板

```yaml
preset_color_schemes:
  THEME_NAME:                          # 日间方案标识符（大写，无空格）
    name: 主题中文名／English Name       # TRIME 中显示名
    author: TRIME Theme
    dark_scheme: THEME_NAME_DARK        # 关联的夜间方案标识符
    # --- 颜色字段（见 9.3）---
    ...

  THEME_NAME_DARK:                      # 夜间方案
    name: THEME_NAME_DARK／主题中文黑
    author: TRIME Theme
    # 注意：夜间方案不需要 dark_scheme 字段
    # --- 颜色字段（见 9.3）---
    ...
```

**命名约定**：
- 日间方案标识符：大写字母 + 下划线（如 `SAKURA`、`OCEAN_MIST`）
- 夜间方案标识符：日间方案名 + `_DARK`（如 `SAKURA_DARK`）
- `name` 字段：中文名 + `／` + 英文名（如 `樱粉／Sakura Pink`）
- 夜间方案 `name` 用 `／中文名 黑` 格式

### 9.3 完整颜色字段清单

#### 9.3.1 基础颜色（19 个，Day & Night 均需定义）

| 字段 | 说明 | 典型 Day 值模式 | 典型 Night 值模式 |
|------|------|----------------|------------------|
| `text_color` | 编码区文字颜色 | 深色（与背景对比） | 浅色 |
| `back_color` | 候选区背景色 | 浅色/柔和色 | 深色 |
| `text_back_color` | 编码区背景色（悬浮窗背景） | 通常与 `back_color` 相同 | 通常与 `back_color` 相同 |
| `border_color` | 边框颜色 | 介于 back 和 keyboard 之间 | 介于 back 和 keyboard 之间 |
| `candidate_separator_color` | 候选分割线颜色 | `0x00000000`（透明=隐藏） | `0x00000000` |
| `candidate_text_color` | 候选文字颜色 | 通常与 `text_color` 相同 | 通常与 `text_color` 相同 |
| `comment_text_color` | 编码提示文字颜色 | 低对比度灰色 | 低对比度灰色 |
| `label_color` | 标签/序号颜色 | 通常与 `comment_text_color` 相同 | 通常与 `comment_text_color` 相同 |
| `hilited_text_color` | 高亮编码文字颜色 | **主题强调色** | **主题强调色（稍亮）** |
| `hilited_back_color` | 高亮编码背景色 | `0x00000000`（透明） | `0x00000000` |
| `hilited_candidate_text_color` | 高亮候选文字颜色 | 白色 `0xffFFFFFF` | 白色 `0xffFFFFFF` |
| `hilited_candidate_back_color` | 高亮候选背景色 | **主题强调色** | **主题强调色（稍亮）** |
| `hilited_comment_text_color` | 高亮注释文字颜色 | 白色 `0xffFFFFFF` | 白色 `0xffFFFFFF` |
| `hilited_key_back_color` | 高亮按键背景色 | **主题强调色** | **主题强调色（稍亮）** |
| `hilited_key_text_color` | 高亮按键文字颜色 | 白色 `0xffFFFFFF` | 白色 `0xffFFFFFF` |
| `hilited_key_symbol_color` | 高亮按键符号色 | 白色 `0xffFFFFFF` | 白色 `0xffFFFFFF` |
| `hilited_off_key_back_color` | 非高亮非当前按键背景 | 浅于 `key_back_color` | 略深于 `key_back_color` |
| `hilited_off_key_text_color` | 非高亮非当前按键文字 | 通常与 `text_color` 相同 | 通常与 `text_color` 相同 |
| `key_back_color` | 普通按键背景 | 白色/极浅色 | 深灰色 |
| `key_text_color` | 普通按键文字 | 深色 | 浅色/白色 |
| `key_symbol_color` | 按键符号颜色 | 通常与 `comment_text_color` 相同 | 通常与 `comment_text_color` 相同 |
| `keyboard_back_color` | 键盘区背景色（按键间隙） | 略深于 `key_back_color` | 最深色 |
| `off_key_back_color` | 非当前按键背景 | 通常与 `key_back_color` 相同 | 通常与 `key_back_color` 相同 |
| `off_key_text_color` | 非当前按键文字 | 通常与 `key_text_color` 相同 | 通常与 `key_text_color` 相同 |
| `preview_back_color` | 按键预览背景 | 深色（文字的反色） | 浅色（文字的反色） |
| `preview_text_color` | 按键预览文字 | 白色 | 深色（背景的反色） |
| `shadow_color` | 阴影颜色 | `0x00000000`（TRIME 不支持阴影） | `0x00000000` |

#### 9.3.2 键盘布局引用颜色（18 个，b/t 成对）

以下颜色在 `preset_keyboards` 中的按键定义里通过 `key_back_color: bh1` 等方式引用。命名规则：`b` 前缀 = 背景色（background），`t` 前缀 = 文字色（text）。

| 字段 | 说明 | 引用位置 |
|------|------|----------|
| `bgn` / `tgn` | 功能键背景/文字（数字键、切换键） | 123、EN、更多 等键 |
| `benter` / `tenter` | 回车键背景/文字 | Return 键 |
| `bkg` / `tkg` | 空格键背景/文字 | space 键 |
| `baoe` / `taoe` | 元音键背景/文字（高亮行按键） | 部分主题中 a/o/e 行 |
| `bbs` / `tbs` | 退格/Shift 键背景/文字 | BackSpace、Shift 键 |
| `bh1` / `th1` | 第 1 行按键背景/文字 | q, w, e, r, t, y, u, i, o, p |
| `bh2` / `th2` | 第 2 行按键背景/文字 | a, s, d, f, g, h, j, k, l |
| `bh3` / `th3` | 第 3 行按键背景/文字 | z, x, c, v, b, n, m |
| `bh4` / `th4` | 第 4 行按键背景/文字 | 逗号键、EN键 |

**典型配色策略**：
- Day 模式：b* 用浅色系/白色，t* 用深色文字
- Night 模式：b* 用深灰色系，t* 用浅色/白色
- `benter`/`baoe` 用主题强调色，`tenter`/`taoe` 用白色

---

## 10. 悬浮键盘 (`liquid_keyboard`)

> **注意**：此段内部**不支持 YAML 变量引用或 fallback 机制**，所有参数直接写值。缺少参数时自动从 `style` 中加载。

### 10.1 基本参数

```yaml
liquid_keyboard:
  author: "TRIME Theme"
  key_text_size: 20
  row: 6               # 竖屏每屏最多显示行数
  row_land: 5           # 横屏每屏最多显示行数
  key_height: 40
  key_height_land: 40
  single_width: 60      # SINGLE 类型按键宽度
  vertical_gap: 8
  margin_x: 5           # 左右间隙的 1/2
```

### 10.2 固定按键条

```yaml
  fixed_key_bar:
    position: bottom    # top | bottom | left | right
    keys:
      - liquid_keyboard_exit
      - space1
      - BackSpace
      - Return2
      - clipboard_window
      - liquid_keyboard_tabs
```

### 10.3 Tab 列表

```yaml
  keyboards: [ascii, cn, list, unit, math, tabs, emoji_smiley, emoji_gesture, emoji_people, emoji_symbol, emoji_heart, emoji_plant, emoji_animal, emoji_food, emoji_travel]
```

### 10.4 各分类按键定义

每个 tab 为一个条目，类型分为两种：

**TABS 类型**（tab 切换器）：
```yaml
  tabs:
    name: 更多
    type: TABS
```

**SINGLE 类型**（单页符号面板）：
```yaml
  cn:
    type: SINGLE
    name: 中文
    keys:  # 列表格式（混合书写）
      - ，
      - 。
      - ？
      ...
```

### 10.5 关键注意事项：中文引号

**[!] 严重陷阱**：`cn`（中文符号）面板中，第 297-298 行（列表中的 `"` 和 `"`）必须使用 **Unicode 中文弯引号**：

| 字符 | Unicode | 说明 |
|------|---------|------|
| `"` | `U+201C` | LEFT DOUBLE QUOTATION MARK（左双引号） |
| `"` | `U+201D` | RIGHT DOUBLE QUOTATION MARK（右双引号） |
| `'` | `U+2018` | LEFT SINGLE QUOTATION MARK（左单引号） |

**绝对不能**使用 ASCII 双引号 `"`（`U+0022`），因为 `"` 在 YAML 中是字符串界定符。在列表项 `- "` 中出现未闭合的 `"` 会导致 YAML 解析失败，TRIME 无法加载主题文件。

**检查方法**：用十六进制查看器确认第 297 行末字符是 `0x201C`，第 298 行末字符是 `0x201D`。

---

## 11. 工具栏 (`tool_bar`)

```yaml
tool_bar:
  button_spacing: 5
  button_font: iconfont.ttf
  back_style: "ic@arrow-left"

  primary_button:
    background:
      type: circle            # circle | rectangle
      corner_radius: 10
      normal: 0x00
      highlight: hilited_candidate_button_color
      vertical_inset: 4
      horizontal_inset: 4
    foreground:
      style: "ic@dots_horizontal"    # 以 ic@ 开头表示内置图标
      normal: candidate_text_color
      padding: 10
    action: menu_keyboard
    long_press_action: Settings

  hide_button: &hide_button
    foreground:
      style: "ic@keyboard_close"
      normal: candidate_text_color
    action: Hide

  emoji_button: &emoji_button
    foreground:
      style: "ic@emoticon"
    action: liquid_keyboard_emoji

  clipboard_button: &clipboard_button
    foreground:
      style: "ic@clipboard"
    action: clipboard_window

  edit_button: &edit_button
    foreground:
      style: "ic@cursor_text"
    action: Keyboard_editor

  ascii_mode_button: &ascii_mode_button
    foreground:
      option_styles: ["中", "En"]
      font_size: 18
      padding: 10
    action: Mode_switch

  full_shape_button: &full_shape_button
    foreground:
      option_styles: ["ic@moon_full", "ic@moon_new"]
    action: Zenkaku_Hankaku

  buttons: [ *hide_button, *emoji_button, *clipboard_button, *edit_button, *ascii_mode_button, *full_shape_button ]
```

工具栏按钮按从右向左排列。

---

## 12. 键盘布局 (`preset_keyboards`)

包含三种布局：

### 12.1 `default` — 中文布局

```yaml
preset_keyboards:
  default:
    author: "TRIME Theme"
    name: 中文布局
    width: 10
    ascii_mode: 0
    keys:
      - {click: q, long_click: 1, swipe_down: 1, swipe_up: 1, key_back_color: bh1, key_text_color: th1}
      # ... 5行 QWERTY 布局
```

按键属性说明：
- `click`：点击输出
- `long_click`：长按输出
- `swipe_down` / `swipe_up`：滑动输出
- `width`：按键宽度（总宽度为 100，如 `width: 15` 占 15%）
- `key_back_color`：引用配色方案中的 `bh1`~`bh4`、`bgn`、`benter`、`bkg`、`bbs` 等
- `key_text_color`：引用 `th1`~`th4`、`tgn`、`tenter`、`tkg`、`tbs` 等
- `composing`：输入中行为（如 `delimiter`、`Return1`）
- `label`：覆盖显示文本
- `label_symbol`：符号标签
- `popup`：长按弹出菜单
- `hilited_key_back_color`：高亮时背景色
- `double_click`：双击行为

### 12.2 `letter` — ASCII 布局

```yaml
  letter:
    author: "TRIME Theme"
    name: ASCII布局
    width: 10
    ascii_mode: 1
    keys: ...
```

与 `default` 几乎相同，差异：
- `ascii_mode: 1`（强制西文模式）
- Enter 键无 `popup` 属性
- Shift 键无 `label_symbol` 和 `double_click`
- 逗号键 click 为 `.`（英文句点）
- EN 键替换为返回中文键盘按键

### 12.3 `number` — 数字符号布局

5 列布局，每列 20% 宽度：运算符 | 数字 | 数字 | 数字 | 功能键

---

## 13. 按键定义 (`preset_keys`)

定义所有功能键的行为，分 6 类：

### 13.1 基础编辑键

```yaml
  Shift_L: {label: Shift, preview: '⇪', functional: false, send: Shift_L}
  Shift_L3: {label: Shift, preview: '⇪', functional: false, send: Shift_L, shift_lock: click}
  Return: { label: enter_labels, preview: '↩', functional: false, send: Return }
  Return1: {label: Enter, preview: '↩', functional: false, send: Return}
  Return2: {label: 回车, send: Return }
  Hide: {label: 隐藏, send: BACK}
  BackSpace: {label: 退格, preview: '⇦', repeatable: true, functional: false, send: BackSpace}
  BackSpace2: {label: 退格, preview: '⇦', repeatable: true, functional: false, slide_delete: true, send: BackSpace}
  space: {repeatable: false, preview: ' ', functional: false, slide_cursor: true, label: '_______', send: space}
  space1: {repeatable: false, label: '空格', functional: false, send: space}
  Escape: {label: 取消, functional: false, send: Escape}
  Clear: {label: 清空, functional: false, send: Escape}
```

注意：`default` 布局使用 `BackSpace2`（带 `slide_delete`），`letter` 布局使用 `BackSpace`。

### 13.2 光标与导航

```yaml
  Left: {label: '←', send: Left, repeatable: true, functional: false}
  Right: {label: '→', send: Right, repeatable: true, functional: false}
```

### 13.3 剪贴板

```yaml
  select_all: {label: 全选, functional: false, send: Control+a}
  cut: {label: 剪切, functional: false, send: Control+x}
  copy: {label: 复制, functional: false, send: Control+c}
  paste: {label: 粘贴, functional: false, send: Control+v}
  paste_clip: {label: 粘贴, send: function, command: clipboard}
```

### 13.4 键盘切换

```yaml
  Keyboard_default: { label: 返回, functional: false, send: Eisu_toggle, select: .default }
  Keyboard_number: { label: 123, functional: false, send: Eisu_toggle, select: number }
  Keyboard_editor: { label: 编辑, functional: false, send: Eisu_toggle, select: number }
  Keyboard_defaulten: { label: EN, functional: false, send: Eisu_toggle, select: letter }
```

### 13.5 悬浮键盘

```yaml
  liquid_keyboard_exit: {label: 返回, send: function, command: liquid_keyboard, option: "-1"}
  liquid_keyboard_switch: { label: 更多, send: function, command: liquid_keyboard, option: "ASCII" }
  liquid_keyboard_tabs: { label: 更多, send: function, command: liquid_keyboard, option: "更多" }
  liquid_keyboard_emoji: { label: '☻', send: function, command: liquid_keyboard, option: "笑脸" }
```

### 13.6 菜单、输入状态与系统

```yaml
  menu_keyboard: { label: 菜单, send: function, command: menu_keyboard }
  clipboard_window: { label: "剪贴", send: function, command: "clipboard_window", option: '0' }
  Mode_switch: {toggle: ascii_mode, functional: false, send: Mode_switch, states: [ 中文, 西文 ]}
  Zenkaku_Hankaku: {toggle: full_shape, send: Mode_switch, states: [ 半角, 全角 ]}
  Schema_switchcn: {label: 中文, send: Control+Shift+6, functional: false}
  Theme_settings: {label: 主题, send: SETTINGS, option: "theme"}
  Settings: {label: 设置, functional: false, send: SETTINGS}
```

---

## 14. 完整文件结构一览

```
1.   文件头（SPDX、编码声明）
2.   config_version, name, author
3.   height（7 个锚点）
4.   round_corner（3 个锚点）
5.   style（所有界面参数 + enter_labels）
6.   preedit
7.   window
8.   fallback_colors
9.   colors（8 个颜色锚点）
10.  preset_color_schemes（配色方案对）
     └── 日间方案  →  37 个颜色字段（含 18 个 b/t 引用色）
     └── 夜间方案  →  37 个颜色字段（不含 dark_scheme）
     #---------配色结束---------#
11.  liquid_keyboard（悬浮键盘完整定义）
12.  tool_bar（工具栏按钮）
13.  preset_keyboards（default, letter, number）
14.  preset_keys（全部功能键 30+ 条）
```

---

## 15. 新建主题的标准工作流

### 15.1 推荐方法：从已验证模板复制

**永远不要从零创建。** 始终从一个已知可在 TRIME 中正常工作的 `.trime.yaml` 文件复制（如 `ocean_mist.trime.yaml`），然后替换配色方案。

这样能确保 `liquid_keyboard` 的 `cn` 面板中中文引号等特殊字符正确，避免 YAML 解析错误。

### 15.2 操作步骤

1. 复制一个已验证工作的 `.trime.yaml`（如 `ocean_mist.trime.yaml`）
2. 修改顶层 `name` 和 `author`
3. 全局替换日间方案标识符（如 `OCEAN` → 新方案名）
4. 全局替换夜间方案标识符（如 `OCEAN_DARK` → 新方案名_DARK）
5. 修改日间方案内的 `name` 和所有颜色值
6. 修改夜间方案内的 `name` 和所有颜色值
7. 确保夜间方案**不包含** `dark_scheme` 字段
8. 另存为新文件名（`新名称.trime.yaml`）

### 15.3 颜色设计原则

- **强调色一致性**：`hilited_*` 系列、`benter`、`baoe` 使用同一色系
- **透明度**：阴影用 `0x00000000`，分割线用 `0x00000000`
- **Day/Night 反转**：
  - Day：浅背景 + 深文字 + 较深键盘背景
  - Night：深背景 + 浅文字 + 最深键盘背景
- **Night 预览色反转**：`preview_back_color` 用浅色，`preview_text_color` 用深色

---

## 16. 常见陷阱与调试

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| TRIME 完全无法加载主题 | YAML 解析错误 | 检查 `cn` 面板第 297-298 行中文引号是否为 U+201C/U+201D |
| 日夜间切换无效 | `dark_scheme` 字段值不匹配 | 确保日间方案的 `dark_scheme` 值与夜间方案标识符完全一致 |
| 键盘颜色未变化 | `preset_keyboards` 中 `key_back_color`/`key_text_color` 引用错误 | 确保引用的是配色方案中定义的 b*/t* 键名 |
| `name` 中的 `"` 导致解析失败 | 使用 ASCII `"` 包裹含中文的 name | 可为 name 加引号或去掉引号 |

---

## 17. 文件编码

- 文件编码：**UTF-8 without BOM**（推荐）或 **UTF-8 with BOM**
- 所有非 ASCII 字符（中文、emoji）直接以 UTF-8 编码写入
- `liquid_keyboard` 中的 emoji 键值直接使用 Unicode 字符

---

*文档版本：1.0 | 适用 TRIME config_version "3.0"*
