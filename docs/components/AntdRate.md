# AntdRate

## 简介源码：`views/AntdRate/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdRate 评分'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRate 评分', level=2),
        fac.AntdParagraph('用于为用户提供美观的星级打分功能。'),
    ]

```

## 示例源码（demos）

### `views/AntdRate/demos/basic_callbacks.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdRate(id='rate-demo', count=10, allowHalf=True, defaultValue=1),
        fac.AntdParagraph(id='rate-demo-output'),
    ]

    return demo_contents


@app.callback(
    Output('rate-demo-output', 'children'), Input('rate-demo', 'value')
)
def rate_demo(value):
    return f'value: {value}'


code_string = [
    {
        'code': """
fac.AntdRate(
    id='rate-demo',
    count=10,
    allowHalf=True,
    defaultValue=1
),

fac.AntdParagraph(
    id='rate-demo-output'
)

...

@app.callback(
    Output('rate-demo-output', 'children'),
    Input('rate-demo', 'value')
)
def rate_demo(value):

    return f'value: {value}'
"""
    }
]

```

### `views/AntdRate/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [fac.AntdRate(), fac.AntdRate(count=10, defaultValue=5)],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [fac.AntdRate(), fac.AntdRate(count=10, defaultValue=5)],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdRate/demos/clear.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSpace(
                [
                    fac.AntdRate(allowClear=True, defaultValue=3),
                    fac.AntdText('allowClear：True'),
                ]
            ),
            fac.AntdSpace(
                [
                    fac.AntdRate(allowClear=False, defaultValue=3),
                    fac.AntdText('allowClear：False'),
                ]
            ),
        ],
        direction='vertical',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=True, defaultValue=3),
                fac.AntdText('allowClear：True'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=False, defaultValue=3),
                fac.AntdText('allowClear：False'),
            ]
        ),
    ],
    direction='vertical',
)
"""
    }
]

```

### `views/AntdRate/demos/half_star.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdRate(allowHalf=True, defaultValue=3.5)

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdRate(allowHalf=True, defaultValue=3.5)
"""
    }
]

```

### `views/AntdRate/demos/read_only_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdRate(
        count=10, defaultValue=7.5, allowHalf=True, disabled=True
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdRate(
    count=10, defaultValue=7.5, allowHalf=True, disabled=True
)
"""
    }
]

```

### `views/AntdRate/demos/star_tooltips.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdRate(
        count=10, tooltips=[f'等级{i + 1}' for i in range(10)]
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdRate(
    count=10, tooltips=[f'等级{i + 1}' for i in range(10)]
)
"""
    }
]

```
