

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- content (a list of or a singular dash component, string or number; optional):
    组件型，标签内容.

- icon (a list of or a singular dash component, string or number; optional):
    组件型，标签前缀图标.

- color (string; optional):
    标签颜色，可使用内置的若干种颜色主题，也可使用任何合法的css颜色值.

- href (string; optional):
    标签点击跳转链接地址.

- target (string; default '_blank'):
    标签链接跳转行为.

- bordered (boolean; default True):
    是否渲染边框  默认值：`True`.

- closeIcon (boolean; default False):
    是否渲染关闭按钮  默认值：`False`.

- closeCounts (number; default 0):
    `closeIcon=True`时，监听关闭按钮累计点击次数  默认值：`0`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.