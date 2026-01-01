

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，定义徽标添加目标元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        控制根元素css样式.

    - indicator (dict; optional):
        控制徽标元素css样式.

- classNames (dict; optional):
    细分控制子元素css类.

    `classNames` is a dict with keys:

    - root (string; optional):
        控制根元素css类.

    - indicator (string; optional):
        控制徽标元素css类.

- color (string; optional):
    徽标颜色.

- count (number; optional):
    徽标显示的数字.

- dot (boolean; default False):
    是否用圆点代替数字显示  默认值：`False`.

- showZero (boolean; default False):
    当`count=0`时，是否强制显示数字  默认值：`False`.

- overflowCount (number; default 99):
    数字显示上限，超出会以显示`+`后缀  默认值：`99`.

- offset (list of numbers; optional):
    徽标在水平、竖直方向上的像素偏移，格式为`[水平偏移, 竖直偏移]`.

- status (a value equal to: 'success', 'processing', 'default', 'error', 'warning'; optional):
    徽标状态，可选项有`'success'`、`'processing'`、`'default'`、`'error'`、`'warning'`.

- text (string; optional):
    参数`status`有效时，设置徽标文本内容.

- title (string; optional):
    徽标鼠标悬停显示文字内容.

- size (a value equal to: 'default', 'small'; default 'default'):
    徽标尺寸规格，可选项有`'default'`、`'small'`.

- nClicks (number; default 0):
    监听徽标累计被点击次数  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.