---
title: draw.io 帮助手册
date: 2021-06-21 23:17:50
typora-root-url: ..\..
Tag: draw
categories: wiki
---

cmd instead of ctrl, option instead of alt for macOS
## LABELS / 标签
| Double click   | Insert text or add an edge label / 插入文本或添加边缘标签    |
| -------------- | ------------------------------------------------------------ |
| Shift+Enter    | New Line in Formatted Labels / 格式化标签中的新行            |
| Enter          | New Paragraph in Formatted Labels / 格式化标签中的新段落     |
| F2 / Enter     | Start Editing Label of Selected Cell / 开始编辑所选单元格的标签 |
| F2 / Tab / Esc | Stop Editing and Apply Value / 停止编辑和应用值              |
| Ctrl+B / I     | Toggle Bold/Italic on Selected Text / 在所选文本上切换粗体/斜体 |
| Ctrl+U         | Toggle Underline on Selected Text / 在所选文本上切换下划线   |
| Ctrl+. / ,     | Superscript/Subscript on Selected Text / 所选文本上的上标/下标 |



## SELECTION / 选择
| (Shift+)Tab        | Select Next / Previous / 选择下一个/上一个 |
| ------------------ | ------------------------------------------ |
| Alt+(Shift+)Tab    | Select Child / Parent / 选择子项 / 父项    |
| Shift+Drag         | Add to Selection / 添加到选择              |
| Alt+Shift+Drag     | Remove from Selection / 从选择中删除       |
| Ctrl+(Shift+)A     | Select All / None / 选择全部/无            |
| Ctrl+Shift+I / E   | Select Vertices / Edges / 选择顶点/边      |
| Ctrl / Shift+Click | Toggle Selection State / 切换选择状态      |
| Alt+Click          | Select Cell Below / 选择下面的单元格       |



## TOOLS / 工具
| Ctrl+Shift+L | Toggle Layers Window / 层窗口开关   |
| ------------ | ----------------------------------- |
| Ctrl+Shift+O | Toggle Outline Window / 缩略图开关  |
| Ctrl+M       | Edit Metadata / 编辑元数据          |
| Ctrl+Shift+P | Toggle Format Panel / 切换格式面板  |
| Ctrl+Shift+M | Edit Vertex Geometry / 编辑顶点几何 |
| Rightclick   | Context Menu / 上下文菜单           |
| Ctrl+Click   | Context Menu / 上下文菜单           |
| F1           | About / 关于                        |



## CURSOR / PAGE KEYS / 光标 / 页面键
| Cursor             | Scroll / Move cell (pt) / 滚动/移动单元格 (pt)               |
| ------------------ | ------------------------------------------------------------ |
| Shift+Cursor       | Move cell (grid) or page / 移动单元格（网格）或页面          |
| Ctrl+Cursor        | Resize cell (pt) or select page / 调整单元格大小 (pt) 或选择页面 |
| Ctrl+Shift+Cursor  | Resize cell (grid size) / 调整单元格大小（网格大小）         |
| Alt+Shift+Cursor   | Clone and connect / 克隆并连接                               |
| Alt+Cursor         | Scroll Page / 滚动页面                                       |
| Ctrl+Shift+Pg Up   | Previous Page / 上一页                                       |
| Ctrl+Shift+Pg Down | Next Page / 下一页                                           |



## CANVAS / 画布
| Ctrl+X               | Cut                                                    |
| -------------------- | ------------------------------------------------------ |
| Ctrl+C               | Copy                                                   |
| Ctrl+V               | Paste                                                  |
| Ctrl+G               | Group / 组合                                           |
| Ctrl+Shift+U         | Ungroup / 取消组合                                     |
| Ctrl+L / Alt+Shift+L | Lock/Unlock / Edit Link / 锁定/解锁/编辑链接           |
| Ctrl+Enter / D       | Duplicate / 复制                                       |
| Backspace or Delete  | Delete Selected Cells / 删除选定的单元格               |
| Ctrl / Shift+Delete  | ...with Connections / Labels / ...带有连接/标签        |
| Ctrl+R               | Turn / Rotate 90° Clockwise / 顺时针旋转/旋转 90°      |
| Shift+Resize（拖动） | Maintain Proportions / 保持比例                        |
| Ctrl / Meta+Resize   | Centered / Group Resize / 居中/组调整大小              |
| Ctrl+Home            | Collapse Container / 折叠容器                          |
| Ctrl+End             | Expand Container / 展开容器                            |
| Ctrl+Shift+Home      | Exit Group / 退出组                                    |
| Ctrl+Shift+End       | Enter Group / 进入群组                                 |
| Ctrl+Shift+F / B     | Bring to Front / Send to Back / 放在前面/放在后面      |
| Ctrl+F               | Find/Replace / 查找/替换                               |
| Alt+Shift+C / T      | Clear Waypoints / Edit Tooltip / 清除航点/编辑工具提示 |
| Ctrl+Shift+Y         | Autosize / 自动尺寸                                    |
| Ctrl / Shift+Drag    | Clone cell/Disconnect edge / 克隆单元格/断开边缘       |
| Alt+Connect（连接）  | Connect to a Fixed Point / 连接到固定点                |



## VIEW / 视口
| Alt+Mouse wheel          | Canvas Zoom In/Out / 画布放大/缩小             |
| ------------------------ | ---------------------------------------------- |
| Ctrl+Shift+Mouse wheel   | Canvas Zoom In/Out / 画布放大/缩小             |
| Ctrl+Mouse wheel         | Screen Zoom In/Out (Mac) / 屏幕放大/缩小 (Mac) |
| Mouse wheel（鼠标滚动）  | Canvas Vertical Scroll / 画布垂直滚动          |
| Shift+Mouse wheel        | Canvas Horizontal Scroll / 画布水平滚动        |
| Space / Right mouse Drag | Pan Canvas / 抓手                              |
| Ctrl+Shift+Drag          | Create / Remove Space / 创建/删除空间          |
| Ctrl+Shift+Connect       | Disable Connections / 禁用连接                 |
| Shift+Home               | Home                                           |
| End                      | Refresh / 刷新                                 |
| Home                     | Reset View / 重置视图                          |
| Ctrl+Shift+H             | Fit Window / 适合窗口                          |
| Ctrl+J                   | Fit Page / 适合页面                            |
| Ctrl+Shift+J             | Fit Two Pages / 适合两页                       |
| Ctrl+0                   | Custom Zoom / 自定义缩放                       |
| Ctrl + (Numpad)          | Zoom In / 放大                                 |
| Ctrl - (Numpad)          | Zoom Out / 缩小                                |



## SIDEBAR / CONNECT / 侧边栏 / 连接

- **Alt+(Shift+)Drag from sidebar<br />**Disable replace, connect on drop (drop targets), Shift ignores current style<br />禁用替换，在放置时连接（放置目标），Shift 忽略当前样式

- **Alt+(Shift / Ctrl)+Click on a sidebar item(**单击侧边栏项目)**Inserts and connects the selected item (Shift ignores current style)<br />插入并连接所选项目（Shift 忽略当前样式）

- **Shift+Click on a sidebar item<br />**Replaces the selected item with the clicked one<br />项目用单击的项目替换所选项目

- **Click on a sidebar item<br />**Connects unconnected side of selected edge<br />连接所选边的未连接侧

- **Shift+Connect<br />**Connect to shape outline (ignore connection points)<br />连接到形状轮廓（忽略连接点）

<br />

## DOCUMENT / 文档

| Ctrl+S                 | Save                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Ctrl+Shift+S           | Save as / 另存为                                             |
| Ctrl+Z                 | Undo                                                         |
| Alt+Shift+A            | Connection Arrows / 连接箭头                                 |
| Alt+Shift+P            | Connection Points / 连接点                                   |
| Hold(长按) Alt         | Ignores handles under the mouse / 忽略鼠标下的手柄           |
| Ctrl+Shift+G           | Toggle grid / 切换网格                                       |
| Ctrl+P                 | Print / 打印                                                 |
| Ctrl+Y                 | Redo (Windows) / 重做                                        |
| Ctrl+Shift+Z           | Redo (Linux/Mac) / 重做                                      |
| Ctrl+Shift+X           | Insert Text / 插入文字                                       |
| Ctrl+K                 | Insert Rectangle / 插入矩形                                  |
| Ctrl+Shift+K           | Insert Ellipse / Toggle Shapes Panel / 插入椭圆/切换形状面板 |
| Esc                    | Cancel Action / 取消操作                                     |
| Alt+Drag / Drop(拖/放) | Force Rubberband / Ignore Group / 强制橡皮筋/忽略组          |



## STYLES / 样式
| Ctrl+Shift+R         | Clear Default Style / 清除默认样式    |
| -------------------- | ------------------------------------- |
| Ctrl+E               | Edit Style / 编辑样式                 |
| Ctrl+Shift+D         | Set as Default Style / 设置为默认样式 |
| Ctrl+Shift+C         | Copy Style / 复制样式                 |
| Ctrl+Shift+V         | Paste Style / 粘贴样式                |
| Alt+Shift+X / B      | Copy Size / Data / 复印尺寸/数据      |
| Ctrl+Alt+Shift+V / E | Paste Size / Data / 粘贴大小/数据     |

| Drag / 拖                          | Clear Default Style / 清除默认样式    |
| ---------------------------------- | ------------------------------------- |
| Tap and hold / 点住                | Edit Style / 编辑样式                 |
| Pinch / 捏                         | Set as Default Style / 设置为默认样式 |
| Tap selected cell / 点按所选单元格 | Copy Style / 复制样式                 |

