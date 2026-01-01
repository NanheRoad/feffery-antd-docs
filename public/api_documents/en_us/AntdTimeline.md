

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- items (list of dicts; required):
    必填，定义时间轴节点.

    `items` is a list of dicts with keys:

    - content (a list of or a singular dash component, string or number; optional):
        组件型，当前节点正文内容.

    - color (string; optional):
        当前节点颜色，可用于表达节点状态，常用方案有`'blue'`（进行中或默认状态）、`'green'`（已完成状态）、`'red'`（警告或错误状态）、`'grey'`（未完成或失效状态）.

    - icon (a list of or a singular dash component, string or number; optional):
        组件型，自定义作为图标的元素.

    - label (a list of or a singular dash component, string or number; optional):
        组件型，当前节点标签内容.

    - position (a value equal to: 'left', 'right'; optional):
        当前节点位置，可选项有`'left'`、`'right'`.

- mode (a value equal to: 'left', 'alternate', 'right'; default 'left'):
    时间轴与内容的相对位置，可选项有`'left'`、`'alternate'`、`'right'`.

- pending (a list of or a singular dash component, string or number; optional):
    组件型，设置时间轴末尾额外幽灵节点标题内容，默认不添加.

- pendingDot (a list of or a singular dash component, string or number; optional):
    组件型，自定义幽灵节点图标.

- reverse (boolean; default False):
    是否逆序排列时间轴  默认值：`False`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.