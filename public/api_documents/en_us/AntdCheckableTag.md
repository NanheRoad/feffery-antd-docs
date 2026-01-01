

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- content (a list of or a singular dash component, string or number; optional):
    组件型，标签内容.

- checkedContent (a list of or a singular dash component, string or number; optional):
    组件型，选择状态下的标签内容.

- unCheckedContent (a list of or a singular dash component, string or number; optional):
    组件型，未选择状态下的标签内容.

- checked (boolean; default False):
    监听或设置当前标签的选择状态  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.