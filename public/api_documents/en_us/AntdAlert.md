

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- message (a list of or a singular dash component, string or number; optional):
    主要提示信息内容.

- description (a list of or a singular dash component, string or number; optional):
    额外提示信息内容.

- type (a value equal to: 'success', 'info', 'warning', 'error'; default 'info'):
    提示信息类型，可选项有`'success'`、`'info'`、`'warning'`、`'error'`
    默认值：`'info'`.

- showIcon (boolean; default False):
    是否显示额外图标  默认值：`False`.

- icon (a list of or a singular dash component, string or number; optional):
    组件型，当`showIcon=True`时，用于自定义图标元素.

- closable (boolean; default False):
    是否可关闭  默认值：`False`.

- messageRenderMode (a value equal to: 'default', 'loop-text', 'marquee'; default 'default'):
    渲染模式，可选项有`'default'`、`'loop-text'`、`'marquee'`  默认值：`'default'`.

- action (a list of or a singular dash component, string or number; optional):
    组件型，定义右上角额外操作区元素.

- banner (boolean; default False):
    是否用作顶部公告  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.