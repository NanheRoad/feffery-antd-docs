# AntdBadge

## 简介源码：`views/AntdBadge/intro.py`
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
                {'title': 'AntdBadge 徽标数'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdBadge 徽标数', level=2),
        fac.AntdParagraph(
            '一般出现在通知图标或头像的右上角，用于显示需要处理的消息条数，通过醒目视觉形式吸引用户处理。'
        ),
    ]

```

## 示例源码（demos）

### `views/AntdBadge/demos/basic_usage.py`
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
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=56,
                overflowCount=50,
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    shape='square',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                dot=True,
            ),
            fac.AntdBadge(
                fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
                count=6,
            ),
            fac.AntdBadge(
                fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
                count=56,
                overflowCount=50,
            ),
            fac.AntdBadge(
                fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
                dot=True,
            ),
            fac.AntdBadge(
                fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
                dot=True,
                offset=[-8, 6],
            ),
        ],
        size=20,
        wrap=True,
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
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdIcon(icon='fc-advertising', style={'fontSize': '40px'}),
            dot=True,
            offset=[-8, 6],
        ),
    ],
    size=20,
    wrap=True,
)
"""
    }
]

```

### `views/AntdBadge/demos/color.py`
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
                color='#1890ff',
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=56,
                overflowCount=50,
                color='#1890ff',
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    shape='square',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                dot=True,
                color='#1890ff',
            ),
        ],
        wrap=True,
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
            color='#1890ff',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
            color='#1890ff',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
            color='#1890ff',
        ),
    ],
    wrap=True,
    size=20,
)
"""
    }
]

```

### `views/AntdBadge/demos/dynamic_number_change.py`
```python
import random
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdButton(
                '计数随机递增', id='badge-demo-generate', type='primary'
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                id='badge-demo-1',
                count=6,
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                id='badge-demo-2',
                count=0,
                dot=True,
            ),
        ],
        size=20,
    )

    return demo_contents


@app.callback(
    [Output('badge-demo-1', 'count'), Output('badge-demo-2', 'count')],
    Input('badge-demo-generate', 'nClicks'),
    [State('badge-demo-1', 'count'), State('badge-demo-2', 'count')],
    prevent_initial_call=True,
)
def badge_callback_demo(nClicks, count1, count2):
    return count1 + random.randint(1, 10), count2 + random.randint(1, 10)


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdButton(
            '计数随机递增', id='badge-demo-generate', type='primary'
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            id='badge-demo-1',
            count=6,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            id='badge-demo-2',
            count=0,
            dot=True,
        ),
    ],
    size=20,
)

...

@app.callback(
    [Output('badge-demo-1', 'count'), Output('badge-demo-2', 'count')],
    Input('badge-demo-generate', 'nClicks'),
    [State('badge-demo-1', 'count'), State('badge-demo-2', 'count')],
    prevent_initial_call=True,
)
def badge_callback_demo(nClicks, count1, count2):
    return count1 + random.randint(1, 10), count2 + random.randint(1, 10)
"""
    }
]

```

### `views/AntdBadge/demos/just_badge.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdBadge(count=8),
            fac.AntdBadge(count=101),
            fac.AntdBadge(count=101, size='small'),
            fac.AntdBadge(dot=True, status='success'),
            fac.AntdBadge(dot=True, status='error'),
            fac.AntdBadge(dot=True, status='default'),
            fac.AntdBadge(dot=True, status='processing'),
            fac.AntdBadge(dot=True, status='warning'),
        ],
        size=20,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdBadge(count=8),
        fac.AntdBadge(count=101),
        fac.AntdBadge(count=101, size='small'),
        fac.AntdBadge(dot=True, status='success'),
        fac.AntdBadge(dot=True, status='error'),
        fac.AntdBadge(dot=True, status='default'),
        fac.AntdBadge(dot=True, status='processing'),
        fac.AntdBadge(dot=True, status='warning'),
    ],
    size=20,
)
"""
    }
]

```

### `views/AntdBadge/demos/sizes.py`
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
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=6,
                size='small',
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=56,
                overflowCount=50,
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                count=56,
                overflowCount=50,
                size='small',
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    shape='square',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                dot=True,
            ),
            fac.AntdBadge(
                fac.AntdAvatar(
                    mode='image',
                    shape='square',
                    src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
                ),
                dot=True,
                size='small',
            ),
        ],
        wrap=True,
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
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=6,
            size='small',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            count=56,
            overflowCount=50,
            size='small',
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
        ),
        fac.AntdBadge(
            fac.AntdAvatar(
                mode='image',
                shape='square',
                src='/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
            ),
            dot=True,
            size='small',
        ),
    ],
    wrap=True,
    size=20,
)
"""
    }
]

```
