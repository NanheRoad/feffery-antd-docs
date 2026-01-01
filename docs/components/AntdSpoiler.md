# AntdSpoiler

## 简介源码：`views/AntdSpoiler/intro.py`
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
                {'title': 'AntdSpoiler 展开收起'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdSpoiler 展开收起', level=2),
        fac.AntdParagraph('用于实现对指定内容的展开收起效果。'),
    ]

```

## 示例源码（demos）

### `views/AntdSpoiler/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpoiler(
        fac.AntdParagraph('内容示例' * 100), maxHeight=70
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100), maxHeight=70
)
"""
    }
]

```

### `views/AntdSpoiler/demos/label_position.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdFlex(
        [
            fac.AntdSegmented(
                id='spolier-label-position-options',
                options=[
                    {'label': 'left', 'value': 'left'},
                    {'label': 'right', 'value': 'right'},
                ],
                defaultValue='left',
            ),
            fac.AntdSpoiler(
                fac.AntdParagraph('内容示例' * 100),
                id='spolier-label-position-demo',
                maxHeight=70,
            ),
        ],
        gap='small',
        align='flex-start',
        vertical=True,
    )

    return demo_contents


@app.callback(
    Output('spolier-label-position-demo', 'labelPosition'),
    Input('spolier-label-position-options', 'value'),
)
def update_spoiler_label_position(value):
    return value


code_string = [
    {
        'code': """
fac.AntdFlex(
    [
        fac.AntdSegmented(
            id='spolier-label-position-options',
            options=[
                {'label': 'left', 'value': 'left'},
                {'label': 'right', 'value': 'right'},
            ],
            defaultValue='left',
        ),
        fac.AntdSpoiler(
            fac.AntdParagraph('内容示例' * 100),
            id='spolier-label-position-demo',
            maxHeight=70,
        ),
    ],
    gap='small',
    align='flex-start',
    vertical=True,
)

...

@app.callback(
    Output('spolier-label-position-demo', 'labelPosition'),
    Input('spolier-label-position-options', 'value'),
)
def update_spoiler_label_position(value):
    return value
"""
    }
]

```

### `views/AntdSpoiler/demos/transition_duration.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpoiler(
        fac.AntdParagraph('内容示例' * 100),
        maxHeight=70,
        transitionDuration=0.5,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdSpoiler(
    fac.AntdParagraph('内容示例' * 100),
    maxHeight=70,
    transitionDuration=0.5,
)
"""
    }
]

```
