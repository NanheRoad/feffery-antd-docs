

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- active (boolean; default False):
    是否显示动画  默认值：`False`.

- shape (a value equal to: 'circle', 'square'; default 'circle'):
    头像占位图形状，可选项有`'circle'`、`'square'`  默认值：`'circle'`.

- size (number | a value equal to: 'large', 'small', 'default'; default 'default'):
    头像占位图尺寸，传入数值型表示像素尺寸，也可传入预设的尺寸规格，可选项有`'large'`、`'small'`、`'default'`
    默认值：`'default'`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.