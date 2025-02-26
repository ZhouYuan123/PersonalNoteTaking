# 1. IDE

## 1. 搜索

| 功能                   | Eclipse                                | IDEA              | Typora |      |
| ---------------------- | -------------------------------------- | ----------------- | ------ | ---- |
| 快速查找               | Ctrl + k                               |                   |        |      |
| 全局搜索               | Ctrl + h                               |                   |        |      |
| 查文件                 | Ctrl + shift + r 【不包括jar】         |                   |        |      |
| 历史打开文件           | Alt + F -->`Recent Files`              | Ctrl + E          |        |      |
| 查看class              | Ctrl + click [F3] 【Ctrl shift t [h]】 | Ctrl + N          |        |      |
| 查看被调用             | Ctrl + Alt + h [g]                     |                   |        |      |
| 回到上一个             | alt + left                             | alt + left        |        |      |
| 查看继承结构           | Ctrl + t [F4]                          | Ctrl +[shift +] H |        |      |
| 搜方法 [显示outline]   | Ctrl + o                               | Alt + 7           |        |      |
| 正向增量查找           | Ctrl + W                               |                   |        |      |
| 显示当前editor下拉列表 | Ctrl + E                               |                   |        |      |
| 切换已经打开的文件     | Ctrl + pg Up/pg Down                   |                   |        |      |
| 列出包含字符串的行     | Ctrl + Shift + U                       |                   |        |      |
|                        |                                        |                   |        |      |

## 2. 编辑

| 功能                        | Eclipse                              | IDEA             | PyCharm               | Typora        | VS                                   | VS code          |
| --------------------------- | ------------------------------------ | ---------------- | --------------------- | ------------- | ------------------------------------ | ---------------- |
| 快捷键设置                  | keys                                 | keymap           |                       |               |                                      |                  |
| 提示                        |                                      |                  |                       |               | ctrl + j                             |                  |
| 删除当前行                  | Ctrl + d                             | Ctrl + Y         | 只能 ctrl + x         | 只能 ctrl + x | ctrl + L                             | Ctrl + Shift + K |
| 复制并粘贴                  | Ctrl + alt + down [up]               | ctrl + d         | ctrl + d              |               | ctrl + d                             | alt + shift + ↓  |
| 竖向多选                    | alt + shift + a                      |                  |                       |               | alt + shif + 鼠标                    |                  |
| 递进式选择代                | Ctrl + w                             | alt + shift +  ↑ |                       |               |                                      |                  |
| 复制文件路径                | Ctrl + shift + C                     | /                |                       |               |                                      |                  |
| 历史选择粘贴                | Ctrl + Shift + V                     | Ctrl + Shift + V |                       | Win + V       |                                      |                  |
| 移动代码                    | alt + 方向箭                         |                  | ctrl + shift + 方向箭 |               |                                      |                  |
| 格式化代码                  | Ctrl + shift + f                     | ctrl + alt + L   | ctrl + alt + l        |               |                                      |                  |
| 补全定义变量                | ctrl + 2 + l <br />[Ctrl + 1+ enter] | alt + enter      |                       |               |                                      |                  |
| 补全代码                    | Alt + / (content assist)             | Ctrl + Shift + — |                       |               |                                      |                  |
| 插入自定义代码              | Alt + /                              | Ctrl + J         |                       |               |                                      |                  |
| 方法参数提示                | Alt + /                              | Ctrl + P         |                       |               |                                      |                  |
| 选择可重写方法              | Alt + / [alt shift s]                | Ctrl + O         |                       |               |                                      |                  |
| 打开方法实现处              |                                      | Ctrl + alt + b   |                       |               |                                      |                  |
| 显示文档内容                | F2                                   | Ctrl + Q         |                       |               |                                      |                  |
|                             |                                      |                  |                       |               |                                      |                  |
| 快速修复                    | Ctrl + 1                             | alt + enter      |                       |               |                                      |                  |
| 批量导包                    | Ctrl + shift + o                     |                  |                       |               |                                      |                  |
| 单行注释                    | Ctrl + /                             |                  |                       |               | Ctrl k-> Ctrl c<br />Ctrl k-> Ctrl u | ctrl + /         |
| 多行注释/取消               | Ctrl + shfit + / [\\]                |                  |                       |               |                                      | alt +  shift + a |
| 移动代码                    | alt + down [up]                      |                  |                       |               |                                      |                  |
| 切换到 [上]<br />下一行空位 | [Ctrl + ] shift + enter              |                  |                       |               |                                      |                  |
| 改名                        | alt + shift + r                      |                  |                       |               |                                      |                  |
| 大小写                      | Ctrl + shift + x [y]                 |                  |                       |               |                                      |                  |
| 自动生成方法                | alt + shift + s                      |                  |                       |               |                                      |                  |
| 显示文件属性                | alt + enter                          |                  |                       |               |                                      |                  |
| 关闭当前 [所有] 窗口        | Ctrl + [shift +] w                   | Ctrl F4          |                       |               |                                      |                  |
| 显示工具提示描述            | F2                                   |                  |                       |               |                                      |                  |

## 3. 视图

| 功能       | Eclipse  | PyCharm | Typora |      |
| ---------- | -------- | ------- | ------ | ---- |
| 最大化窗口 | Ctrl + m |         |        |      |

## 4. debug
| 功能       | Eclipse  | PyCharm | Typora | VS |
| ---------- | -------- | ------- | ------ | ---- |
| 显示变量的值 | Ctrl + shift + d |  |  | |
| 显示变量的值 | Ctrl + shift + i | | | |
| 执行选择表达式 | ctrl + u | | | |
| 运行至当前行 | Ctrl + R | | | |
| 启动到下个断点 | F8 | | | F5 |
| 逐过程 | F6 | | | F10 |
| 进入方法 | F5 | | | F11 |
| 跳出方法 | F7 | | | shift + F11 |
| 设置【去掉】断点 | Ctrl + shift + b |         |        | F9 |
| 开启【跳过】所有断点 | Ctrl + alt + b | | |  |
|忽略断点运行||||Ctrl + F5|
|查看选择类所有对象|ctrl + shift + n||||
|退出调试||||shift + F5|

## 5. PyCharm

| 功能           |                    |
| -------------- | ------------------ |
| Ctrl + Alt + L | 格式化             |
| Ctrl + F2      | 终止程序           |
| Shift + F8     | 跳出               |
| Shift + F9     | debug执行          |
| Shift + F10    | 执行脚本           |
| F7             | 进入               |
| F8             | 单步执行           |
| F9             | resume             |
| 打开设置       | Ctrl + Alt + S     |
| 快速复制       | Ctrl + D           |
| 移动当前行     | Alt + shift + 方向 |
| 运行代码       | Ctrl + shift + f10 |
| 重命名文件     | shift + f6         |
|                |                    |

# 2. Snipaste

F1: 截屏

F3: 固定

Esc: 取消固定

shift：切换RGB进制

c: 直接复制颜色

复制截屏：ctrl + c

# 3. xmind

enter: 同级。tab: 子级
