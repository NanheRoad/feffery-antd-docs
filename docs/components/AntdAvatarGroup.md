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
