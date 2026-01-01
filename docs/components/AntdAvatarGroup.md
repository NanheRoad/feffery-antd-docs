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

## 示例源码（demos）

### `views/AntdAvatarGroup/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAvatarGroup(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAvatarGroup/demos/ellipsis.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAvatarGroup(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```

### `views/AntdAvatarGroup/demos/ellipsis_trigger.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAvatarGroup(
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

    return demo_contents


code_string = [
    {
        'code': """
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
"""
    }
]

```
