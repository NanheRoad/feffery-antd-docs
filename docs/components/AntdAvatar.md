# AntdAvatar

## 简介源码：`views/AntdAvatar/intro.py`
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
                {'title': 'AntdAvatar 头像'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdAvatar 头像', level=2),
        fac.AntdParagraph('用于渲染图标、文字或图片形式的头像。'),
    ]

```

## 示例源码（demos）

### `views/AntdAvatar/demos/background.py`
```python
import feffery_antd_components as fac
import feffery_utils_components as fuc
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fuc.FefferyHexColorPicker(id='avatar-bg-color-input'),
            fac.AntdSpace(
                [
                    fac.AntdAvatar(id='avatar-bg-color-icon-demo'),
                    fac.AntdAvatar(
                        id='avatar-bg-color-text-demo', mode='text', text='F'
                    ),
                ]
            ),
        ],
        style={'width': '100%'},
    )

    return demo_contents


@app.callback(
    [
        Output('avatar-bg-color-icon-demo', 'style'),
        Output('avatar-bg-color-text-demo', 'style'),
    ],
    Input('avatar-bg-color-input', 'color'),
)
def avatar_bg_color_demo(color):
    return [{'background': color}] * 2


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(id='avatar-bg-color-input'),
        fac.AntdSpace(
            [
                fac.AntdAvatar(id='avatar-bg-color-icon-demo'),
                fac.AntdAvatar(
                    id='avatar-bg-color-text-demo', mode='text', text='F'
                ),
            ]
        ),
    ],
    style={'width': '100%'},
)

...

@app.callback(
    [
        Output('avatar-bg-color-icon-demo', 'style'),
        Output('avatar-bg-color-text-demo', 'style'),
    ],
    Input('avatar-bg-color-input', 'color'),
)
def avatar_bg_color_demo(color):
    return [{'background': color}] * 2
"""
    }
]

```

### `views/AntdAvatar/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdAvatar(),
            fac.AntdAvatar(mode='text', text='F'),
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
        ]
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdAvatar(),
        fac.AntdAvatar(mode='text', text='F'),
        fac.AntdAvatar(
            mode='image',
            src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
        ),
    ]
)
"""
    }
]

```

### `views/AntdAvatar/demos/responsive_sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAvatar(
        mode='image',
        src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
        size={'xs': 24, 'sm': 28, 'md': 32, 'lg': 36, 'xl': 40, 'xxl': 45},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdAvatar(
    mode='image',
    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    size={'xs': 24, 'sm': 28, 'md': 32, 'lg': 36, 'xl': 40, 'xxl': 45},
)
"""
    }
]

```

### `views/AntdAvatar/demos/sizes.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdAvatar(size='small'),
            fac.AntdAvatar(),
            fac.AntdAvatar(size='large'),
            fac.AntdAvatar(size=64),
        ],
        align='center',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdAvatar(size='small'),
        fac.AntdAvatar(),
        fac.AntdAvatar(size='large'),
        fac.AntdAvatar(size=64),
    ],
    align='center',
)
"""
    }
]

```

### `views/AntdAvatar/demos/square_shape.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdAvatar(
        mode='image',
        src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
        size='large',
        shape='square',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdAvatar(
    mode='image',
    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    size='large',
    shape='square',
)
"""
    }
]

```

### `views/AntdAvatar/demos/use_with_AntdBadge.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=6,
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    shape='square',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                dot=True,
            ),
        ],
        size=20,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
    ],
    size=20,
)
"""
    }
]

```

### `views/AntdAvatar/demos/use_with_AntdIcon.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdAvatar(icon=icon, style={'background': '#4551f5'})
            for icon in [
                'antd-user',
                'antd-team',
                'antd-github',
                'antd-fire',
                'antd-thunderbolt',
                'antd-robot',
            ]
        ],
        wrap=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdAvatar(icon=icon, style={'background': '#4551f5'})
        for icon in [
            'antd-user',
            'antd-team',
            'antd-github',
            'antd-fire',
            'antd-thunderbolt',
            'antd-robot',
        ]
    ],
    wrap=True,
)
"""
    }
]

```
