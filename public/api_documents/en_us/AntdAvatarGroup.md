

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，传入组内各`AntdAvatar`组件.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- max (dict; optional):
    配置最多显示功能相关参数.

    `max` is a dict with keys:

    - count (number; optional):
        最多显示的头像个数，默认无限制.

    - style (dict; optional):
        头像省略部分css样式.

    - popover (dict; optional):
        展开层相关配置参数.

        `popover` is a dict with keys:

        - placement (a value equal to: 'top', 'bottom', 'right'; optional):
            超出`maxCount`数量限制之外的头像气泡卡片弹出方位，可选项有`'top'`、`'bottom'`、`'right'`
            默认值：`'top'`.

        - trigger (a value equal to: 'hover', 'click'; optional):
            超出`maxCount`数量限制之外的头像气泡卡片弹出触发方式，可选项有`'hover'`、`'click'`
            默认值：`'hover'`.

- size (dict; default 'default'):
    统一设置内部头像尺寸规格，传入数值型表示像素尺寸，传入字符型表示内置规格，可选项有`'large'`、`'small'`、`'default'`，支持响应式断点
    默认值：`'default'`.

    `size` is a number | a value equal to: 'large', 'small', 'default'
    | dict with keys:

    - xs (number; optional)

    - sm (number; optional)

    - md (number; optional)

    - lg (number; optional)

    - xl (number; optional)

    - xxl (number; optional)

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.