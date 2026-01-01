

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- offsetBottom (number; optional):
    触发固钉效果的视窗底部距离像素阈值.

- offsetTop (number; default 0):
    触发固钉效果的视窗顶部距离像素阈值  默认值：`0`.

- target (string; optional):
    滚动事件监听的特定目标容器id.

- affixed (boolean; optional):
    监听当前目标是否已触发固定.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.