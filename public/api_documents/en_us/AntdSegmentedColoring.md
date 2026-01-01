

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- breakpoints (list of numbers; required):
    必填，监听或设置分段断点数组.

- colors (list of strings; required):
    必填，为各分段设置颜色，数组长度应为`breakpoints`长度减1.

- controls (boolean; default True):
    是否为各分段数值输入框添加增减按钮  默认值：`True`.

- keyboard (boolean; default True):
    是否可通过键盘上下方向键增减各分段数值输入框数值  默认值：`True`.

- min (number; optional):
    各分段数值输入框允许输入数值下限，默认无限制.

- max (number; optional):
    各分段数值输入框允许输入数值上限，默认无限制.

- step (number; default 0.01):
    各分段数值输入框数值调整步长  默认值：`0.01`.

- precision (number; default 2):
    各分段数值输入框数值精度  默认值：`2`.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- bordered (boolean; default True):
    是否显示边框，设置为`True`时等价于`variant='outlined'`  默认值：`True`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; optional):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- placeholder (string; optional):
    各分段数值输入框占位文字内容.

- readOnly (boolean; optional):
    是否渲染为只读状态  默认值：`False`.

- pureLegend (boolean; default False):
    是否开启纯图例模式  默认值：`False`.

- inputNumberStyle (dict; optional):
    各分段数值输入框统一css样式.

- colorBlockStyle (dict; optional):
    色块css样式.

- colorBlockPosition (a value equal to: 'left', 'right'; default 'right'):
    色块显示方位，可选项有`'left'`、`'right'`  默认值：`'right'`.

- colorBlockClickEvent (dict; optional):
    监听分段色块点击事件.

    `colorBlockClickEvent` is a dict with keys:

    - color (string; optional):
        被点击色块的颜色值.

    - range (list of numbers; optional):
        被点击色块对应范围值.

    - timestamp (number; optional):
        事件对应时间戳.

- pureLegendLabelStyle (dict; optional):
    当`pureLegend=True`时，设置各分段数值统一css样式.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.