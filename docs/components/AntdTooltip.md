# AntdTooltip

## 简介源码：`views/AntdTooltip/intro.py`
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
                {'title': 'AntdTooltip 信息提示'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTooltip 信息提示', level=2),
        fac.AntdParagraph('用于为指定元素添加额外信息提示。'),
    ]

```

## 示例源码（demos）

### `views/AntdTooltip/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTooltip(
        fac.AntdButton('锚点元素'), title='信息提示示例'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例'
)
"""
    }
]

```

### `views/AntdTooltip/demos/color.py`
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
            fuc.FefferyHexColorPicker(
                id='tooltip-color-demo-input', showAlpha=True, color='#f6f7f866'
            ),
            fac.AntdTooltip(
                fac.AntdButton('锚点示例'),
                id='tooltip-color-demo',
                title='信息提示示例',
            ),
        ]
    )

    return demo_contents


@app.callback(
    [
        Output('tooltip-color-demo', 'color'),
        Output('tooltip-color-demo', 'title'),
    ],
    Input('tooltip-color-demo-input', 'color'),
)
def tooltip_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fuc.FefferyHexColorPicker(
            id='tooltip-color-demo-input', showAlpha=True, color='#f6f7f866'
        ),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-color-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    [
        Output('tooltip-color-demo', 'color'),
        Output('tooltip-color-demo', 'title'),
    ],
    Input('tooltip-color-demo-input', 'color'),
)
def tooltip_color_demo(color):
    return [
        color,
        fac.AntdParagraph(['当前color: ', fac.AntdText(color, copyable=True)]),
    ]
"""
    }
]

```

### `views/AntdTooltip/demos/control_open.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdSwitch(id='tooltip-open-switch', checked=False),
            fac.AntdTooltip(
                fac.AntdButton('锚点示例'),
                id='tooltip-open-demo',
                title='信息提示示例',
            ),
        ]
    )

    return demo_contents


@app.callback(
    Output('tooltip-open-demo', 'open'),
    Input('tooltip-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_tooltip_open(checked):
    return checked


code_string = [
    {
        'code': """
fac.AntdSpace(
    [
        fac.AntdSwitch(id='tooltip-open-switch', checked=False),
        fac.AntdTooltip(
            fac.AntdButton('锚点示例'),
            id='tooltip-open-demo',
            title='信息提示示例',
        ),
    ]
)

...

@app.callback(
    Output('tooltip-open-demo', 'open'),
    Input('tooltip-open-switch', 'checked'),
    prevent_initial_call=True,
)
def control_tooltip_open(checked):
    return checked
"""
    }
]

```

### `views/AntdTooltip/demos/custom_style.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTooltip(
        fac.AntdButton('锚点示例'),
        title='内容示例' * 50,
        styles={
            'root': {'width': 250},
            'body': {'maxHeight': 150, 'overflowY': 'auto'},
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTooltip(
    fac.AntdButton('锚点示例'),
    title='内容示例' * 50,
    styles={
        'root': {'width': 250},
        'body': {'maxHeight': 150, 'overflowY': 'auto'},
    },
)
"""
    }
]

```

### `views/AntdTooltip/demos/hide_arrow.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdTooltip(
        fac.AntdButton('锚点元素'), title='信息提示示例', arrow='hide'
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdTooltip(
    fac.AntdButton('锚点元素'), title='信息提示示例', arrow='hide'
)
"""
    }
]

```

### `views/AntdTooltip/demos/placement.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdSpace(
        [
            fac.AntdTooltip(
                fac.AntdButton(placement),
                title='信息提示示例',
                placement=placement,
            )
            for placement in [
                'top',
                'left',
                'right',
                'bottom',
                'topLeft',
                'topRight',
                'bottomLeft',
                'bottomRight',
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
        fac.AntdTooltip(
            fac.AntdButton(placement),
            title='信息提示示例',
            placement=placement,
        )
        for placement in [
            'top',
            'left',
            'right',
            'bottom',
            'topLeft',
            'topRight',
            'bottomLeft',
            'bottomRight',
        ]
    ],
    wrap=True,
)
"""
    }
]

```

### `views/AntdTooltip/demos/question_with_absolute_position.py`
```python
from dash import html
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = html.Div(
        [
            html.Span(
                fac.AntdTooltip(
                    fac.AntdButton('示例1', type='primary'), title='示例内容'
                ),
                style={'position': 'absolute', 'left': 15, 'bottom': 15},
            ),
            html.Span(
                fac.AntdTooltip(
                    fac.AntdButton('示例2', type='primary'), title='示例内容'
                ),
                style={'position': 'absolute', 'right': 15, 'top': 15},
            ),
            html.Span(
                fac.AntdTooltip(
                    fac.AntdButton('示例3', type='primary'), title='示例内容'
                ),
                style={'position': 'absolute', 'right': 15, 'bottom': 15},
            ),
        ],
        style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
    )

    return demo_contents


code_string = [
    {
        'code': """
html.Div(
    [
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例1', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'left': 15, 'bottom': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例2', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'top': 15},
        ),
        html.Span(
            fac.AntdTooltip(
                fac.AntdButton('示例3', type='primary'), title='示例内容'
            ),
            style={'position': 'absolute', 'right': 15, 'bottom': 15},
        ),
    ],
    style={'position': 'relative', 'height': 300, 'background': '#dee2e6'},
)
"""
    }
]

```
