# AntdAvatarGroup

## 简介源码：`views/AntdAvatarGroup/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdAvatarGroup 头像组'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdAvatarGroup 头像组', level=2),
        fac.AntdParagraph('用于妥善展示一组头像。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdAvatarGroup(
    [
        fac.AntdAvatar(
            mode='text', text='F', style={'background': background}
        )
        for background in [
            '#d29200',
            '#ffb900',
            '#fff100',
            '#d83b01',
            '#ea4300',
            '#00188f',
            '#004b50',
        ]
    ]
)
```

### ellipsis

- 说明：演示 ellipsis 的用法。

#### 代码
```python
fac.AntdAvatarGroup(
    [
        fac.AntdAvatar(
            mode='text', text='F', style={'background': background}
        )
        for background in [
            '#d29200',
            '#ffb900',
            '#fff100',
            '#d83b01',
            '#ea4300',
            '#00188f',
            '#004b50',
        ]
    ],
    max={'count': 3},
)
```

### ellipsis_trigger

- 说明：演示 ellipsis_trigger 的用法。

#### 代码
```python
fac.AntdAvatarGroup(
    [
        fac.AntdAvatar(
            mode='text', text='F', style={'background': background}
        )
        for background in [
            '#d29200',
            '#ffb900',
            '#fff100',
            '#d83b01',
            '#ea4300',
            '#00188f',
            '#004b50',
        ]
    ],
    max={'count': 3, 'popover': {'trigger': 'click'}},
)
```

## API 参数说明



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
